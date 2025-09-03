+++
date = '2025-08-04T12:44:47+10:00'
draft = false
title = '🔮 AWS Services for Generative AI'
tags = ['LLM', 'AI', 'Design Patterns']
+++

LLM design patterns are reusable strategies for building robust, efficient, and scalable AI applications. They help developers structure retrieval, reading, rewriting, memory, agent, and orchestration workflows for large language models. These patterns improve performance, maintainability accuracy, cost and security.

## Table of Contents

## Introduction
Here we explore how to leverage Gen AI on AWS. We cover key concepts, model types, prompt engineering, embeddings, RAG, vector stores, and design patterns for building effective AI solutions.
---

Before we proceed setting the stage.
## Concepts 
## AWS Services list

| Category                        | Service Name                              | Description                                                                                   |
|----------------------------------|-------------------------------------------|----------------------------------------------------------------------------------------------|
| Foundation Models & Access       | Amazon Bedrock                            | Fully managed service providing API access to foundation models from Amazon and third parties.|
|                                  | Amazon SageMaker JumpStart                | Pre-trained models and solutions for ML, including generative AI models.                     |
|                                  | Amazon Titan                              | Amazon's family of foundation models (text, embeddings, image generation).                   |
| Application-Specific AI          | Amazon Q                                  | AI-powered assistant for business applications and code.                                      |
|                                  | Amazon CodeWhisperer                      | AI-powered code generation and suggestions (now part of Amazon Q Developer).                 |
|                                  | Amazon Lex                                | Conversational AI for building chatbots and voice applications.                              |
|                                  | Amazon Polly                              | Text-to-speech service with neural voices.                                                   |
|                                  | Amazon Transcribe                         | Automatic speech recognition with generative capabilities.                                   |
|                                  | Amazon QuickSight (Gen BI)                | Generative BI: Natural language queries and insights in business intelligence dashboards.     |
| Content Generation & Processing  | Amazon Textract                           | Extract text and data from documents with AI.                                                |
|                                  | Amazon Comprehend                         | Natural language processing and text analysis.                                               |
|                                  | Amazon Translate                          | Neural machine translation.                                                                  |
|                                  | Amazon Rekognition                        | Computer vision for image and video analysis.                                                |
| Vector Store & Retrieval         | Amazon OpenSearch Service                 | Managed search and vector database for retrieval-augmented generation (RAG) use cases.       |
|                                  | Amazon Kendra                             | Intelligent enterprise search and retrieval with AI.                                         |
|                                  | PostgreSQL (pgvector on RDS)              | Vector search extension for similarity search in PostgreSQL databases.                       |
| Development & Infrastructure     | Amazon SageMaker                          | Complete ML platform including tools for generative AI.                                      |
|                                  | AWS Trainium                              | Custom chips for training large language models.                                             |
|                                  | AWS Inferentia                            | Custom chips for running inference workloads.                                                |
|                                  | Amazon EC2 & SageMaker (P4, P5 instances) | GPU-accelerated SageMaker instances for training/inference of generative models.             |
| Specialized Solutions            | Amazon Personalize                        | ML service for personalized recommendations.                                                 |
|                                  | Amazon Forecast                           | Time series forecasting using machine learning.                                              |
|                                  | Amazon DevOps Guru                        | AI-powered application monitoring and anomaly detection.                                     |
|                                  | Amazon Fraud Detector                     | Machine learning fraud detection.                                                            |
|                                  | Amazon Lookout suite                      | AI-powered monitoring for equipment, metrics, and vision.                                    |
| Healthcare AI                    | AWS HealthScribe                          | Generative AI-powered medical transcription and clinical note generation.                    |

## Key Concepts
- Foundation Models (FMs): Pre-trained models like GPT, BERT, and DALL-E that consists of billions of parameters (aka weights) trained on vast datasets.
- Pre training: Training on large datasets to learn general patterns. Foundational models trained on large diverse datasets over a period of weeks or months using large cluster of CPUs/GPUs/TPUs.
- Fine tuning: Adapting pre-trained models to specific tasks using smaller, task-specific datasets.

