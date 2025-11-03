# AI Agent Chat Application

A production-ready web application powered by Azure AI Foundry's agent capabilities. This implementation builds on Microsoft's recommended architecture and patterns for deploying intelligent agents in Azure.

The application features an AI agent that leverages the Azure AI Agent service with Azure AI Search for knowledge retrieval from uploaded files, enabling contextual responses with citations. Comprehensive monitoring and tracing capabilities are integrated for observability and troubleshooting.

<div style="text-align:center;">

[**OVERVIEW**](#overview) \| [**GETTING STARTED**](#getting-started) \| [**LOCAL DEVELOPMENT**](#local-development) \| [**RESOURCE CLEAN-UP**](#resource-clean-up) \| [**GUIDANCE**](#guidance) \| [**TROUBLESHOOTING**](./docs/troubleshooting.md)

</div>

## Overview

This application deploys a web-based chat interface with an AI agent running in Azure Container Apps. Built on Microsoft's implementation patterns for Azure AI Foundry, it demonstrates best practices for deploying intelligent agents at scale.

The architecture creates an Azure AI Foundry project with integrated Azure AI services. Complete monitoring and tracing are configured for production visibility. For detailed resource information, see the [resources](#resources) section.

Instructions are provided for deployment through GitHub Codespaces, VS Code Dev Containers, and your local development environment.

<img width="822" height="991" alt="Screenshot 2025-10-31 at 5 03 30 PM" src="https://github.com/user-attachments/assets/4961baae-1f0f-4bd7-9630-750474f2daea" />
<img width="822" height="991" alt="Screenshot 2025-10-31 at 5 03 22 PM" src="https://github.com/user-attachments/assets/05193e5e-9cb0-4ea2-8faf-cd52ee79befb" />





### Architecture

![Architecture diagram showing that user input is provided to the Azure Container App, which contains the app code. With user identity and resource access through managed identity, the input is used to form a response. The input and the Azure monitor are able to use the Azure resources deployed in the solution: Application Insights, Azure AI Foundry Project, Azure AI Services, Storage account, Azure Container App, and Log Analytics Workspace.](docs/images/architecture.png)

The application runs in Azure Container Apps to process user input and generate responses. It leverages Azure AI Foundry projects and services, including model deployments and intelligent agents.

### Key Capabilities

- **Knowledge Retrieval**
  Intelligent agents use Azure AI Search to retrieve relevant information from uploaded files and documents.

- **Configurable AI Models**
  Deploy and customize AI models like gpt-4o-mini with adjustable capacity and knowledge retrieval methods.

- **Production Monitoring**
  Built-in Azure Monitor and Application Insights integration for comprehensive tracing, logging, and performance optimization.

- **Flexible Deployment**
  Support for GitHub Codespaces, VS Code Dev Containers, and local development environments.

- **Agent Evaluation**
  Tools for evaluating agent performance and quality metrics during development and CI/CD workflows.

- **Security Assessment**
  AI Red Teaming capabilities for automated safety and security scanning before production deployment.

## Getting Started

### Quick Start

1. Set up your Azure environment using:
   ```bash
   azd up
   ```
2. Select your Azure subscription and region when prompted
3. Wait for deployment to complete (5-20 minutes) — your web app URL will be provided

For detailed deployment options and troubleshooting, see the [deployment guide](./docs/deployment.md).

## Local Development

For customizing the agent and running locally:

- **[Local Development Guide](./docs/local_development.md)** - Set up your environment, customize the frontend and backend, modify agent behavior, and use evaluation tools to improve performance.

Key topics covered:
- Environment setup
- Running the development server
- Frontend and backend customization
- Agent configuration and tools
- Evaluation and testing


## Resource Clean-up

To prevent incurring unnecessary charges, it's important to clean up your Azure resources after completing your work with the application.

- **When to Clean Up:**
  - After you have finished testing or demonstrating the application.
  - If the application is no longer needed or you have transitioned to a different project or environment.
  - When you have completed development and are ready to decommission the application.

- **Deleting Resources:**
  To delete all associated resources and shut down the application, execute the following command:
  
    ```bash
    azd down
    ```

    Please note that this process may take up to 20 minutes to complete.

⚠️ Alternatively, you can delete the resource group directly from the Azure Portal to clean up resources.

## Guidance

### Costs

Pricing varies per region and usage, so it isn't possible to predict exact costs for your usage.
The majority of the Azure resources used in this infrastructure are on usage-based pricing tiers.

You can try the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator) for the resources:

- **Azure AI Foundry**: Free tier. [Pricing](https://azure.microsoft.com/pricing/details/ai-studio/)  
- **Azure Storage Account**: Standard tier, LRS. Pricing is based on storage and operations. [Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/)  
- **Azure AI Services**: S0 tier, defaults to gpt-4o-mini. Pricing is based on token count. [Pricing](https://azure.microsoft.com/pricing/details/cognitive-services/)  
- **Azure Container App**: Consumption tier with 0.5 CPU, 1GiB memory/storage. Pricing is based on resource allocation, and each month allows for a certain amount of free usage. [Pricing](https://azure.microsoft.com/pricing/details/container-apps/)  
- **Log analytics**: Pay-as-you-go tier. Costs based on data ingested. [Pricing](https://azure.microsoft.com/pricing/details/monitor/)  
- **Agent Evaluations**: Incurs the cost of your provided model deployment used for local evaluations.  
- **AI Red Teaming Agent**: Leverages Azure AI Risk and Safety Evaluations to assess attack success from the automated AI red teaming scan. Users are billed based on the consumption of Risk and Safety Evaluations as listed in [our Azure pricing page](https://azure.microsoft.com/pricing/details/ai-foundry/). Click on the tab labeled “Complete AI Toolchain” to view the pricing details.

⚠️ To avoid unnecessary costs, remember to take down your app if it's no longer in use,
either by deleting the resource group in the Portal or running `azd down`.

### Security guidelines

This implementation uses [Managed Identity](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/overview) for secure credential handling across development and production environments.

For your own repository, enable [GitHub secret scanning](https://docs.github.com/code-security/secret-scanning/about-secret-scanning) and consider these security measures:

- Enable [Microsoft Defender for Cloud](https://learn.microsoft.com/azure/defender-for-cloud/) for Azure resource protection
- Secure Azure Container Apps with a [firewall](https://learn.microsoft.com/azure/container-apps/waf-app-gateway) and/or [Virtual Network](https://learn.microsoft.com/azure/container-apps/networking)

> **Security Note** <br/>
This implementation demonstrates Azure AI capabilities. Before production deployment, ensure you have implemented appropriate security controls and follow your organization's security policies. For comprehensive best practices, see [Azure AI Foundry security guidance](https://learn.microsoft.com/en-us/azure/ai-foundry/).

### Resources

This template creates everything you need to get started with Azure AI Foundry:

| Resource | Description |
|----------|-------------|
| [Azure AI Project](https://learn.microsoft.com/azure/ai-studio/how-to/create-projects) | Provides a collaborative workspace for AI development with access to models, data, and compute resources |
| [Azure OpenAI Service](https://learn.microsoft.com/azure/ai-services/openai/) | Powers the AI agents for conversational AI and intelligent search capabilities. Default models deployed are gpt-4o-mini, but any Azure AI models can be specified per the [documentation](docs/deploy_customization.md#customizing-model-deployments) |
| [Azure Container Apps](https://learn.microsoft.com/azure/container-apps/) | Hosts and scales the web application with serverless containers |
| [Azure Container Registry](https://learn.microsoft.com/azure/container-registry/) | Stores and manages container images for secure deployment |
| [Storage Account](https://learn.microsoft.com/azure/storage/blobs/) | Provides blob storage for application data and file uploads |
| [AI Search Service](https://learn.microsoft.com/azure/search/) | *Optional* - Enables hybrid search capabilities combining semantic and vector search |
| [Application Insights](https://learn.microsoft.com/azure/azure-monitor/app/app-insights-overview) | *Optional* - Provides application performance monitoring, logging, and telemetry for debugging and optimization |
| [Log Analytics Workspace](https://learn.microsoft.com/azure/azure-monitor/logs/log-analytics-workspace-overview) | *Optional* - Collects and analyzes telemetry data for monitoring and troubleshooting |

## Troubleshooting

For solutions to common deployment, container app, and agent issues, see the [Troubleshooting Guide](./docs/troubleshooting.md).
