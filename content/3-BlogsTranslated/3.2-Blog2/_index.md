---
title: "Blog 2"
date: "2025-12-09"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Enhance LLM observability with Amazon Bedrock and Dynatrace

**Author:**

- Kristof Muhi, Principal Product Manager – Dynatrace
- Varun Jasti, Solutions Architect – AWS
- Shashiraj Jeripotula, Principal Partner Solutions Architect – AWS

_Date: March 27, 2025_

<style>
body { 
font-family: "Times New Roman", Times, serif; 
font-size: 13px;
}

h1 { 
font-size: 24px;
}

h2 { 
font-size: 18px;
}

h3 { 
font-size: 16px;
}

</style>

## Introduction

Organizations leveraging [Amazon Bedrock](https://aws.amazon.com/bedrock/) for their AI generation applications need to ensure reliable, secure, and responsible AI operations at scale. As these applications become an integral part of business processes, the deployment of comprehensive Large Language Model (LLM) observability becomes essential. Monitoring model performance, detecting hallucinations, prompt injection attacks, malicious language, and PII leaks, while also tracking latency, drift, data flow, and maintaining cost control, are some of the critical use cases. By implementing robust observability practices, teams can gain deep insights into their LLM application behavior, optimize resource usage, ensure consistent response quality, and maintain compliance with governance requirements.

[Dynatrace](https://www.dynatrace.com/) is an all-in-one observation platform that automatically collects production insights, tracing, logging, metrics, and real-time application data at scale. With its powerful AI engine ([Davis AI](https://www.dynatrace.com/platform/artificial-intelligence/)), Dynatrace alerts the team to production-level issues before they disrupt users, helps predict resource usage and costs, performance issues, and provides safeguards for data protection and compliance maintenance.

In this post, we explain how Dynatrace delivers end-to-end monitoring and visibility into AI-generated applications using Amazon Bedrock models that enable comprehensive LLM observation capabilities.

## LLM Observational Use Cases

Dynatrace assists with the following large-scale LLM observation and AI generation use cases.

### Complexity of Multi-Model Tracing

Multi-model tracing presents hidden complexities as interactions between models with different architectures, output formats, and latency profiles must be coherently correlated across the entire chain. When diverse models operate in a chain, errors can silently propagate through these heterogeneous systems, making root cause analysis particularly challenging without standardized telemetry that can efficiently connect the points between different inputs and outputs.

Dynatrace enables end-to-end tracing across different models, connecting the frontend and backend components of the application stack.

This multi-model tracing provides complete visibility and traceability of events, allowing you to understand what happened when an issue occurred or when an invalid response was sent to the client throughout the entire model chain.

### Predictive Operations of AI Workloads – Cost and Performance

Predictive operations leverage advanced analytics and machine learning to predict and optimize AI workload behavior before issues impact business operations, powered by Davis AI. This proactive approach transforms traditional monitoring into forward-looking operational intelligence for AI systems.

• **Cost Forecasting and Optimization:** Forecast token usage, API calls, and associated costs within Amazon Bedrock to enable better budget planning and resource allocation for the future. Efficient budget planning with accurate cost forecasting helps reduce operational costs through better resource planning and allocation.

• **Performance Downturn Prediction:** Identify early warning signs of potential model performance issues through pattern recognition.

• **Anomaly and Problem Detection:** Use Dynatrace's Davis AI Prediction to detect anomalous patterns in model behavior that may indicate emerging problems or peak usage in the architecture. This will minimize service and application downtime by addressing potential issues before they become critical.

### Barrier Analysis

Barrier analysis focuses on monitoring and enforcing safety boundaries around AI systems to ensure they operate within defined ethical, security, and performance parameters. This critical capability helps organizations maintain control over their AI applications while protecting against potential risks and abuse.

• Key components such as real-time detection of prompt injection attack attempts and security vulnerabilities protect your business and customer data. This allows organizations to monitor unauthorized PII exposures and leaks of sensitive data.

• Barriers allow you to monitor malicious and inappropriate language, harmful content, and other harmful material.
• Bias feedback with early threat detection. Allows for improved model reliability through consistent boundary enforcement and easy compliance.

• Barrier analysis protects AI applications by safeguarding brand reputation through preventing inappropriate feedback and queries.

### Data Governance, Compliance, and Auditing

In the context of applications built with LLM on Amazon Bedrock, governance, compliance, and auditing capabilities through observability ensure organizations maintain control, transparency, and accountability for their AI-generated applications while meeting regulatory requirements and industry standards.

Dynatrace helps track all inputs and outputs for a full audit trail. It allows you to query all data in real time and store it for future reference. It easily establishes and maintains a complete data stream from prompt to response across the entire pipeline and gathers all evidence for responsible AI practices and regulatory reporting such as [FIPS](https://www.nist.gov/standardsgov/compliance-faqs-federal-information-processing-standards-fips), [FedRAMP](https://www.fedramp.gov/) and [EU AI Act](https://artificialintelligenceact.eu/).

Dynatrace's model fingerprinting capability generates unique identifiers for LLM instances based on architecture, training data, and parameters, enabling accurate instance tracking for regulatory and audit compliance. Accurate tracking of model instances through model fingerprinting ensures compliance with regulatory and audit requirements.

### Dynatrace + LLM Observation Layers

LLM observation requires an expansive approach spanning multiple layers, from user-oriented applications to underlying infrastructure. Each layer plays a crucial role in understanding LLM performance, identifying bottlenecks, ensuring reliable operation, and detecting potential security risks. Dynatrace provides a unified end-to-end observation platform that can help organizations gain deep insights into each of these layers, enabling them to effectively monitor, optimize, troubleshoot, and secure their LLM-powered applications.

![Figure 1: Bedrock Observation Pipeline of a Travel Application Running on Kubernetes Using Dynatrace](https://d2908q01vomqb2.cloudfront.net/77de68daecd823babbb58edb1c8e14d7106e83bb/2025/03/27/Picture1-17.png)

_Figure 1: Bedrock Observation Pipeline of a Travel Application Running on Kubernetes Using Dynatrace_

In our example, the application runs in a Kubernetes cluster. [OpenLLMetry](https://github.com/traceloop/openllmetry) of [Traceloop](https://www.traceloop.com/) enhances LLM observation capabilities for Amazon Bedrock models by collecting specific KPIs about key AI. It enriches [OpenTelemetry](https://opentelemetry.io/) data and integrates seamlessly with Dynatrace. This provides a comprehensive view of LLM application performance in a production environment. Ultimately, it empowers businesses to optimize and scale their AI deployments efficiently.

![Figure 2: High-level overview of the different layers of AI-generated measurement devices for observational capabilities](https://d2908q01vomqb2.cloudfront.net/77de68daecd823babbb58edb1c8e14d7106e83bb/2025/03/26/bedrock-highscale-1.png)

_Figure 2: High-level overview of the different layers of AI-generated measurement devices for observational capabilities_

From the diagram above (Figure 2), Dynatrace provides end-to-end visibility of AI applications through the entire technology stack.

• **Application Layer:** Dynatrace monitors user-oriented applications interacting with LLM, tracking performance metrics, user experience, and usage patterns. Continuous data collection across the entire architecture (frontend, backend, AI generation stack) reveals real-time application behavior, while logging collects user interactions and application-specific errors for debugging. Visualization tools provide customizable dashboards to monitor key application metrics and identify trends or anomalies related to LLM integration.

• **Organization Layer – Monitoring the Performance of the Orchestration Framework:** These frameworks (e.g., [LangChain](https://www.langchain.com/), [LlamaIndex](https://www.llamaindex.ai/)) manage the workflow prompt and integration pipeline. Dynatrace observes these workflows, providing metrics on prompt engineering efficiency, chain performance, and caching. Its anomaly detection capabilities alert the team to potential issues and bottlenecks, ensuring the smooth operation of AI-driven processes.

• **Semantic Layer and Vector Databases:** Analyzes the meaning and content of LLM inputs and outputs. This involves understanding relationships between concepts, tracking sentiment, and identifying potential biases, inaccuracies, or anomalies along with performance bottlenecks in Retrieval Augmented Generation (RAG) architectures using vector databases (e.g., Pinecone, Milvus, Weaviate, Qdrant, Chroma). Dynatrace's extensibility allows for integration.
Compatible with semantic analytics tools. By gathering data from a vector database, Dynatrace can provide a unified view of LLM output, including sentiment analysis, topic modeling, and bias detection. This data can then be visualized and analyzed using Dynatrace's Metrics & Performance Analytics and Visualization capabilities.

• **Model Layer – Observing Model Providers and Platform Providers:** Dynatrace monitors token usage, stability, latency, throughput, resource consumption, and model drift within Amazon Bedrock. Metrics & Performance Analytics allows for deep dives into model performance, tracking metrics such as latency, throughput, and resource consumption. Model fingerprinting supports detailed versioning, while anomaly detection flags significant changes in performance or output quality—helping the team understand and optimize model behavior.

• **Infrastructure Layer:** Dynatrace's full-stack observation capabilities extend to computing resources (e.g., Amazon EC2, NVIDIA GPUs) and networks. It automatically collects CPU/GPU utilization, memory usage, and other critical statistics. Real-time anomaly detection with Davis AI helps teams quickly address hardware bottlenecks that could impact LLM performance.

"From initial model evaluation to production deployment, comprehensive monitoring is critical for generative AI systems. The integration between Dynatrace and Amazon Bedrock allows organizations to easily track key performance metrics and trace data, ensuring their AI applications remain optimized and operate reliably." – Denis Batalov, Tech Leader, ML & AI, AWS.

_"Generative AI is rapidly becoming the standard for customer experience, driving companies to deliver AI-native interactions at high speed. Simultaneously, we are witnessing an accelerated development of AI systems, leading to exponentially increasing capabilities. However, deploying these highly complex AI application stacks in production presents significant challenges. AI observational capabilities play a crucial role in ensuring reliable performance, enhancing customer satisfaction, and driving measurable ROI for the business."_ – Alois Reitbauer, VP, Chief Technology Strategist, Dynatrace

## Summary

In this blog post, we discussed how Dynatrace can deliver enhanced visibility into generative AI applications leveraging Amazon Bedrock.

Leveraging Dynatrace's capabilities, you can:

• **Maintain operational efficiency:** Monitor latency, resource usage, and costs to optimize performance and control expenses.

• **Accelerate the path to production:** Deploy reliable and secure AI applications faster with confidence.

• **Make data-driven decisions:** Leverage comprehensive data to inform model selection, fine-tuning, and risk mitigation strategies.

• **Improve application reliability:** Proactively identify and address performance bottlenecks and other issues before they impact users.

• **Enhance security:** Detect and mitigate security risks in real time, protecting your data and reputation.

• **Enhancing Governance and Compliance:** Maintain a clear data flow and ensure responsible AI practices that meet regulatory requirements and ethical standards.

For guidance on setting up Dynatrace's end-to-end instrumentation solution with Amazon Bedrock, please refer to the following Dynatrace blog post.

## Dynatrace – AWS Partner Spotlight

Dynatrace is an AWS Advanced Technology Partner and AWS Competency Partner providing intelligent software to simplify cloud complexity and accelerate digital transformation. With enhanced observational capabilities, AI, and full automation, our all-in-one platform provides answers—not just data—about application performance, underlying infrastructure, and the experience of all users.

[Contact Dynatrace](https://partnercentral.awspartner.com/PartnerConnect?id=001E000000texmiIAA&source=Blog&campaign=) | [Partner Overview](https://partners.amazonaws.com/partners/001E000000texmiIAA/Dynatrace) | [AWS Marketplace](https://aws.amazon.com/marketplace/seller-profile?id=1422b3b0-b081-4af9-9d2b-34e6eb924f05)

**TAGS:** [Amazon Bedrock](https://aws.amazon.com/blogs/apn/tag/amazon-bedrock/), [Artificial Intelligence](https://aws.amazon.com/blogs/apn/tag/artificial-intelligence/), [Machine Learning](https://aws.amazon.com/blogs/apn/tag/machine-learning/), [Observability](https://aws.amazon.com/blogs/apn/tag/observability/)
