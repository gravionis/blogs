+++
date = '2024-05-03T12:44:47+10:00'
draft = false
title = 'Python Async IO'
tags = ['Python', 'AsyncIO']
+++

Python’s asyncio is a concurrency framework built on the concept of single-threaded cooperative multitasking. Unlike traditional multithreading or multiprocessing, which rely on the operating system to preemptively switch tasks, asyncio schedules coroutines—special functions defined with async def—that explicitly yield control back to the event loop when they encounter an await statement.

The event loop is the core of asyncio. It continuously runs, monitoring and dispatching tasks, I/O operations, and timers. When a coroutine awaits an operation (e.g., network I/O, file access, a sleep delay), it tells the event loop, “I’m waiting, you can run something else.” This allows the loop to resume other coroutines without blocking the entire program.

Because everything happens in a single thread, asyncio avoids issues like race conditions and thread synchronization overhead—but it’s still highly concurrent for I/O-bound tasks. CPU-bound tasks, however, do not benefit directly from asyncio unless offloaded to a separate thread or process via run_in_executor().

Asyncio shines in applications like web servers, chat systems, and crawlers, where many tasks spend time waiting on I/O. By letting tasks cooperate instead of competing for CPU time, asyncio achieves high throughput and scalability with minimal resource usage.

### Core Concepts
async def and await

```python
import asyncio

async def greet():
    await asyncio.sleep(1)
    print("Hello")

asyncio.run(greet())
```
async def defines a coroutine.

await suspends the coroutine until the awaited task is done.

asyncio.run() starts the event loop and runs the coroutine.

### Scheduling Concurrent Tasks
asyncio.create_task()
Runs multiple coroutines concurrently (starts them immediately).

```python
async def say(msg, delay):
    await asyncio.sleep(delay)
    print(msg)

async def main():
    task1 = asyncio.create_task(say("first", 2))
    task2 = asyncio.create_task(say("second", 1))
    await task1
    await task2

asyncio.run(main())
```

### asyncio.gather()

Waits for many coroutines in parallel.

```python
async def main():
    await asyncio.gather(
        say("A", 2),
        say("B", 1),
    )
```

### Running Blocking Code
run_in_executor
When you have blocking code (time.sleep(), file I/O, DB), use this to run it in a thread or process:

```python
import time

def blocking_code():
    time.sleep(2)
    return "done"

async def main():
    loop = asyncio.get_running_loop()
    result = await loop.run_in_executor(None, blocking_code)
    print(result)

asyncio.run(main())
```

None means use default thread pool executor.

You can also use ThreadPoolExecutor() or ProcessPoolExecutor() explicitly.

### Queues and Coordination Primitives
asyncio.Queue
Allows coroutines to safely share data.

```python
async def producer(queue):
    for i in range(5):
        await queue.put(i)
        await asyncio.sleep(1)

async def consumer(queue):
    while True:
        item = await queue.get()
        print(f"Consumed {item}")
        queue.task_done()

async def main():
    queue = asyncio.Queue()
    await asyncio.gather(producer(queue), consumer(queue))

asyncio.run(main())
```

### Other Primitives:
- **asyncio.Event**	Signaling between tasks
- **asyncio.Lock**	Prevent race conditions
- **asyncio.Semaphore**	Limit concurrent access
- **asyncio.Condition**	Advanced coordination

