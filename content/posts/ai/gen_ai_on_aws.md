+++
date = '2025-08-04T12:44:47+10:00'
draft = false
title = '🔮 AWS Services for Generative AI'
tags = ['LLM', 'AI', 'Design Patterns']
+++

LLM design patterns are reusable strategies for building robust, efficient, and scalable AI applications. They help developers structure retrieval, reading, rewriting, memory, agent, and orchestration workflows for large language models. These patterns improve performance, maintainability accuracy, cost and security.

## Introduction

Here we explore how to leverage Gen AI on AWS. We cover key concepts, model types, prompt engineering, embeddings, RAG, vector stores, and design patterns for building effective AI solutions.

---

## AWS Services list

### Foundation Models & Model Access

- **Amazon Bedrock**
  - Fully managed service for accessing foundation models (FMs) by Amazon and leading third-party providers e.g. Titan (AWS), Claude (Anthropic), Command R (Cohere), LLaMA 2 (Meta), Jurassic (AI21), Mistral, Stable Diffusion (Stability AI)
  - Bedrock does support text, image generation, embeddings, and more—video, audio (through Data Automation), and multimodal embeddings.
  - Agents are supported.
  - Provides unified API, model evaluation, orchestration and guardrails for responsible AI.

- **Amazon SageMaker JumpStart**
  - SageMaker JumpStart provides a catalog of pre-trained models, including foundation models (FMs) and end-to-end machine learning solutions, enabling rapid experimentation, deployment, and fine-tuning.
  - It integrates seamlessly with SageMaker Studio, allowing for easy workflow management and accelerated ML development.
  - Enables rapid experimentation, deployment, and fine-tuning of FMs.
  - Integrates with SageMaker Studio for easy workflow management.

- **Amazon Titan**
  - Amazon’s own family of foundation models for text, embeddings, and image generation.
  - Available via Amazon Bedrock.
  - Designed for enterprise security, privacy, and responsible AI.

### Application-Specific AI

- **Amazon Q**
  - Generative AI-powered assistant for business applications and developer productivity.
  - Integrates with AWS services, business data, and code repositories.
  - Supports natural language querying, code generation, and business insights.

- **Amazon CodeWhisperer**
  - AI-powered code completion and generation (now part of Amazon Q Developer).
  - Supports multiple programming languages and IDEs.
  - Provides security scanning and code reference tracing.

- **Amazon Lex**
  - Conversational AI for building chatbots and voice assistants.
  - Supports multi-turn conversations, context management, and speech recognition.
  - Integrates with AWS Lambda and other AWS services.

- **Amazon Polly**
  - Text-to-speech service with neural and standard voices.
  - Supports real-time and batch synthesis, multiple languages, and voice customization.
  - Used for IVR, accessibility, media, and more.

- **Amazon Transcribe**
  - Automatic speech recognition (ASR) for audio/video transcription.
  - Supports custom vocabularies, speaker identification, and real-time streaming.
  - Integrates with other AWS AI services for analytics and search.

- **Amazon QuickSight (Generative BI)**
  - Business intelligence service with generative AI features.
  - Enables natural language querying and automated insights in dashboards.
  - Supports data storytelling and conversational analytics.

### Content Generation & Processing

- **Amazon Textract**
  - AI-powered extraction of text, tables, and forms from documents.
  - Supports structured and unstructured data, handwriting, and multi-page files.
  - Integrates with workflow automation and document management.

- **Amazon Comprehend**
  - Natural language processing (NLP) for text analysis.
  - Detects sentiment, entities, key phrases, topics, and language.
  - Supports custom entity and classification models.

- **Amazon Translate**
  - Neural machine translation for real-time and batch text translation.
  - Supports dozens of languages and domain adaptation.
  - Integrates with other AWS services for multilingual applications.

- **Amazon Rekognition**
  - Computer vision for image and video analysis.
  - Detects objects, scenes, faces, text, and unsafe content.
  - Supports facial comparison, celebrity recognition, and PPE detection.

### Vector Store & Retrieval

- **Amazon OpenSearch Service**
  - Managed search and analytics engine with vector database capabilities.
  - Supports similarity search for retrieval-augmented generation (RAG) use cases.
  - Scalable, integrates with Bedrock and SageMaker.

- **Amazon Kendra**
  - Intelligent enterprise search powered by machine learning.
  - Supports natural language queries, semantic search, and document ranking.
  - Connects to multiple data sources (SharePoint, S3, databases, etc.).

- **PostgreSQL (pgvector on RDS)**
  - Managed PostgreSQL with pgvector extension for vector similarity search.
  - Enables storage and retrieval of embeddings for RAG and semantic search.
  - Integrates with SageMaker and Bedrock pipelines.

### Development & Infrastructure

- **Amazon SageMaker**
  - End-to-end machine learning platform for building, training, and deploying models.
  - Supports distributed training, hyperparameter tuning, and MLOps.
  - Integrates with Bedrock, JumpStart, and custom model workflows.

- **AWS Trainium**
  - Custom silicon accelerators optimized for training large language models.
  - High performance and cost efficiency for deep learning workloads.
  - Available via SageMaker and EC2.

- **AWS Inferentia**
  - Custom silicon accelerators for high-throughput inference of deep learning models.
  - Reduces inference latency and cost for production workloads.
  - Available via SageMaker and EC2.

- **Amazon EC2 & SageMaker (P4, P5 instances)**
  - GPU-accelerated instances for large-scale AI training and inference.
  - P4/P5 instances support the latest NVIDIA GPUs for LLMs and generative models.
  - Used for custom model development, fine-tuning, and high-throughput inference.

### Specialized Solutions

- **Amazon Personalize**
  - Real-time personalization and recommendation engine.
  - Uses user behavior and item metadata for tailored experiences.
  - Integrates with websites, apps, and marketing platforms.

- **Amazon Forecast**
  - Time series forecasting using machine learning.
  - Automates data preparation, model selection, and evaluation.
  - Used for demand planning, inventory, and financial forecasting.

- **Amazon DevOps Guru**
  - AI-powered monitoring and anomaly detection for applications.
  - Identifies operational issues, root causes, and remediation steps.
  - Integrates with AWS CloudWatch and other AWS services.

- **Amazon Fraud Detector**
  - Machine learning-based fraud detection for online transactions.
  - Supports real-time scoring and custom fraud detection models.
  - Integrates with payment, account, and identity workflows.

- **Amazon Lookout Suite**
  - AI-powered monitoring for equipment (Lookout for Equipment), metrics (Lookout for Metrics), and vision (Lookout for Vision).
  - Detects anomalies, quality issues, and predictive maintenance needs.
  - Integrates with industrial IoT and business analytics.

### Healthcare AI

- **AWS HealthScribe**
  - Generative AI-powered medical transcription and clinical note generation.
  - Converts doctor-patient conversations into structured clinical documentation.
  - Supports compliance, privacy, and integration with healthcare systems.

## Key Concepts
- Foundation Models (FMs): Pre-trained models like GPT, BERT, and DALL-E that consists of billions of parameters (aka weights) trained on vast datasets.
- Pre training: Training on large datasets to learn general patterns. Foundational models trained on large diverse datasets over a period of weeks or months using large cluster of CPUs/GPUs/TPUs.
- Fine tuning: Adapting pre-trained models to specific tasks using smaller, task-specific datasets.
