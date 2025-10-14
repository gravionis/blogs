+++
date = '2025-08-04T12:44:47+10:00'
draft = false
title = 'n8n workflow automation'
tags = ['AI', 'n8n']
+++

N8n is an open-source workflow automation tool that enables users to connect various applications and services through a visual interface. It supports a wide range of integrations, including AI services, allowing users to create complex workflows that leverage artificial intelligence for tasks such as data processing, content generation, and decision-making.

## n8n: Workflow Automation Platform

n8n ("nodemation") is an open-source workflow automation tool that enables you to connect various services, APIs, and internal systems with minimal code. It provides a visual editor to design, automate, and orchestrate complex business processes, data flows, and integrations.

### Key Features
- **Visual Workflow Builder:** Drag-and-drop interface for creating workflows without deep programming knowledge.
- **Extensive Integrations:** Supports 350+ built-in integrations for popular apps, databases, and APIs.
- **Custom Code Support:** Allows JavaScript code nodes for advanced logic and custom integrations.
- **Self-Hosted or Cloud:** Can be deployed on your own infrastructure or used as a managed cloud service.
- **Event-Driven Automation:** Trigger workflows on schedules, webhooks, or events from connected systems.

### Typical Use Cases
- Data synchronization between SaaS tools
- Automated notifications and reporting
- ETL (Extract, Transform, Load) pipelines
- API orchestration and microservice automation
- Business process automation

### What Can n8n Do?

n8n is a powerful automation platform that enables you to:

- **Automate Repetitive Tasks:** Eliminate manual work by automating routine processes such as data entry, notifications, and report generation.
- **Integrate AI:** Connect to AI services (e.g., OpenAI, Hugging Face) for tasks like text generation, sentiment analysis, or image recognition within your workflows.
- **Integrate 3rd Party Services:** Seamlessly connect with hundreds of SaaS tools, APIs, and cloud services to synchronize data, trigger actions, or orchestrate multi-step processes.
- **Integrate Databases and File Handling:** Read from and write to SQL/NoSQL databases, manipulate files (CSV, Excel, PDF, etc.), and automate data pipelines.
- **Integrate Custom Code:** Use JavaScript code nodes to add custom logic, transform data, or call external APIs not natively supported.
- **Make Decisions:** Build workflows with conditional logic, branching, and loops to handle complex business rules and dynamic paths.
- **Human-in-the-Loop Feedback:** Pause workflows for manual review, approval, or input, enabling human intervention at critical steps before automation continues.

### What n8n Cannot Do

While n8n is a powerful automation tool, it has some limitations (which can be handled by 3rd party tools):

- **Limited Coding Integration:** You can add custom JavaScript code in code nodes, but you cannot build or run full applications, complex scripts, or use advanced programming libraries as you would in a traditional development environment.
- **Cannot Build Full Applications:** n8n is designed for workflow automation such as sending emails, updating db etc not for building web/mobile apps, user interfaces, or standalone software products.
- **Workflow Limited in Scale:** n8n is suitable for small to medium workflows. Large-scale, high-throughput, or highly parallel workflows may hit performance or reliability limits.
- **Limited Error Handling:** Error handling is basic—while you can catch and route errors, advanced retry logic, transaction management, or complex exception handling is limited.

### Deployment Options: Pros and Cons

| Option            | Pros                                                      | Cons                                                      |
|-------------------|-----------------------------------------------------------|-----------------------------------------------------------|
| Local             | Full control, no hosting cost, data stays on your machine | Limited accessibility, not always online, manual updates  |
| Cloud (n8n Cloud) | Easy setup, managed updates, accessible from anywhere     | Recurring cost, less control, data on third-party servers |
| VPS               | Flexible, scalable, remote access, more control than cloud| Requires server management, security/maintenance overhead |

### Quick Start with Docker

```shell
docker volume create n8n_data

docker run -it --rm \
 --name n8n \
 -p 5678:5678 \
 -e N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true \
 -e N8N_RUNNERS_ENABLED=true \
 -e NODE_TLS_REJECT_UNAUTHORIZED=0 \
 -v n8n_data:/home/node/.n8n \
 docker.n8n.io/n8nio/n8n
```

### n8n User Interface Overview

n8n's UI is organized into three main sections:

#### 1. Workflows
- **Purpose:** Design, edit, and manage automation workflows.
- **Workflow Steps:**
  - **Trigger Node:** Defines how the workflow starts (see Trigger Types below).
  - **Processing Nodes:** Perform actions such as data transformation, API calls, database queries, or invoking AI services (e.g., send a prompt to OpenAI, analyze text, etc.).
  - **Conditional Logic:** Add IF/ELSE branches, loops, and switches to control workflow paths based on data or outcomes.
  - **Human-in-the-Loop:** Insert manual approval or input steps, pausing the workflow until a user provides feedback or confirmation.
  - **Notifications/Actions:** Send messages, emails, or trigger other systems as the final step or at any point in the workflow.
- **Example:** On chat message received → Analyze with AI → If flagged, request human review → Notify user of result.

#### 2. Credentials
- **Purpose:** Securely store and manage API keys, tokens, and connection details for third-party services, databases, and internal systems.
- **Features:**
  - Add, edit, and test credentials for each integration.
  - Credentials are referenced in workflow nodes for secure, reusable connections.

#### 3. Executions
- **Purpose:** Monitor, debug, and review workflow runs.
- **Features:**
  - View execution history, including success/failure status, input/output data, and error messages.
  - Replay or debug failed executions step-by-step.
---


These triggers allow n8n workflows to respond to a wide range of events, making automation flexible and responsive to business needs.

### Tip: Connecting to Ollama on Localhost from Docker
- **Ollama:** To connect n8n (running in Docker) to Ollama running on your local machine, set the base URL in your Ollama API credentials to: **http://host.docker.internal:11434/**

These triggers allow n8n workflows to respond to a wide range of events, making automation flexible and responsive to business needs.

### Credentials Node:
Credentials nodes in n8n securely store and manage authentication details for connecting to external services. Common credential types include:

- **Google Sheets:** Connects to Google Sheets for reading, writing, and updating spreadsheet data using OAuth2 authentication.
- **Gmail:** Allows sending and receiving emails through Gmail, requiring OAuth2 credentials.
- **Slack:** Integrates with Slack for sending messages, notifications, and interacting with channels or users via OAuth2 tokens.
- **GitHub:** Connects to GitHub for repository management, issue tracking, and workflow automation using personal access tokens or OAuth2.
- **MySQL/PostgreSQL:** Stores database connection details (host, port, user, password) for querying and updating SQL databases.
- **AWS:** Manages access keys and secrets for interacting with AWS services (S3, Lambda, etc.).
- **HTTP Basic Auth/API Key:** Stores username/password or API key for generic HTTP integrations.
- **OpenAI:** Stores API keys for connecting to OpenAI's GPT and other AI services.
- **Custom OAuth2:** Supports any service requiring OAuth2 authentication by configuring client ID, secret, and scopes.

Credentials are referenced by workflow nodes to enable secure, reusable, and centralized management of sensitive connection information. This ensures integrations are both secure and easy to update across multiple workflows.



## Node Types

n8n provides a variety of node types to build powerful, flexible workflows:

### AI
- **Purpose:** Build autonomous agents, summarize or search documents, generate content, classify data, and more using AI models and APIs (e.g., OpenAI, Ollama).
#### AI Agent Node:
AI Agent nodes in n8n enable workflows to interact with AI models and services for advanced automation and decision-making. Common use cases and features include:

- **Text Generation:** Use models like OpenAI GPT or Ollama to generate text, summaries, or responses based on workflow data.
- **Classification & Analysis:** Perform sentiment analysis, entity extraction, or content moderation using AI APIs.
- **Conversational Agents:** Integrate chatbots or virtual assistants that can respond to user queries or automate support tasks.
- **Image/Audio Processing:** Leverage AI for image recognition, transcription, or translation tasks.
- **Custom AI Workflows:** Chain AI steps with other workflow logic, such as routing results for human review or triggering follow-up actions.

### Action in an App
- **Purpose:** Perform actions in external apps or services such as Google Sheets, Telegram, Notion, Slack, GitHub, and more (e.g., create a row, send a message, update a record).

### Data Transformation
- **Purpose:** Manipulate, filter, map, or convert data between formats, clean up input, or enrich workflow data for downstream steps.

### Flow
- **Purpose:** Control the workflow logic by branching, merging, looping, or switching paths based on conditions or data (e.g., IF, Switch, Merge, Loop).

### Core
- **Purpose:** Run custom code, make HTTP requests, set webhooks, manage credentials, or perform other essential workflow operations (e.g., Code, HTTP Request, Webhook, Set, Wait).

### Trigger Node:
Trigger nodes are used to start workflows in n8n based on specific events or schedules. Common trigger types include:

- **Manual Trigger:** Start the workflow manually from the UI for testing or ad-hoc runs.
- **Scheduled Trigger:** Run workflows on a defined schedule (e.g., every hour, daily, cron expressions).
- **Webhook Trigger:** Start the workflow when an HTTP request is received at a unique URL endpoint.
- **Form Submission Trigger:** Initiate the workflow when a user submits a form (integrated with supported form services).
- **Chat Message Trigger:** Launch the workflow when a message is received in a connected chat platform (e.g., Slack, Discord, Telegram).
- **Email Trigger:** Start the workflow when a new email arrives in a monitored inbox.
- **File Trigger:** Run the workflow when a new file is added or modified in a connected storage service (e.g., Google Drive, Dropbox).
- **Database Trigger:** Initiate the workflow when a new record is created or updated in a database.
- **App Event Trigger:** Start the workflow on specific events from integrated apps (e.g., new row in Google Sheets, new issue in GitHub).

### Human in the Loop
- **Purpose:** Pause the workflow to wait for human approval, review, or input before continuing automation (e.g., manual approval, feedback collection).

## AI & Agentic Workflow Orchestrators – n8n Perspective
| Tool / Platform | Strengths (vs n8n) | Weaknesses (vs n8n) | Ideal Use Case |
|---|---|---|---|
| **LangGraph** | Graph-based orchestration for stateful, multi-agent AI; fine-grained control over memory and branching | Requires coding expertise; smaller ecosystem; fewer prebuilt integrations | Complex agent workflows, autonomous decision-making pipelines |
| **LangChain** | Tailored for LLMs, supports RAG and agent workflows | Primarily code-based; less focus on external service integration | Knowledge assistants, custom agent logic, RAG pipelines |
| **AutoGen (Microsoft)** | Multi-agent orchestration with role management; built-in memory & collaboration tools | Requires customization; more complex setup | Multi-agent research assistants, enterprise agent teams |
| **CrewAI** | Collaborative AI agents with task delegation and role-based interactions | Higher learning curve; resource-intensive setup | Multi-agent orchestration for complex autonomous tasks |
| **Dify** | Rapid prototyping of AI-powered applications; easy conversational agent creation | Less developer control; fewer integration options | Quick AI chatbots, document-QA, rapid AI prototypes |
| **Flowise / other no-code RAG builders** | Low barrier to entry; visual UI for AI workflows | Limited complex agent logic; less scalable | Small RAG prototypes, chatbot experiments |
| **Prefect** | Production-grade scheduling, retries, observability; can orchestrate agent tasks | Not AI/agent-native; code-first | Production orchestration of AI/ML pipelines |
| **Dagster** | Strong type-checking, observability, reproducible pipelines | Not AI/agent-native | ML pipelines, reproducible data/AI workflows |
| **Temporal** | Durable workflows; supports long-running agent processes | Requires more infra/engineering overhead | Long-running multi-step AI/business processes |
| **Ray / Ray Serve** | Scalable multi-agent compute; actor-based parallelism | Lower-level than workflow UIs; more infra complexity | High-scale agent fleets, reinforcement learning loops |
| **Pipedream / Make / Zapier** | Low-code SaaS integrations; fast workflow creation | Not agent-native; limited stateful multi-agent patterns | Quick automations, integrating AI agents with external services |
