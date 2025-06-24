+++
date = '2024-05-03T12:44:47+10:00'
draft = false
title = 'Python Async IO'
tags = ['Python', 'AsyncIO']
+++

Python Asyncio is a single-threaded concurrency framework using cooperative multitasking. It uses an event loop to schedule and switch between coroutines that voluntarily give up control via await.

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

