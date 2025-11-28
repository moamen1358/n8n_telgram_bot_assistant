# Ultimate AI Personal Assistant Workflow

This project implements a sophisticated **AI Agent Ecosystem** built on [n8n](https://n8n.io). It functions as a comprehensive personal assistant, orchestrating multiple specialized sub-agents to automate daily tasks ranging from email management to content creation.

## System Overview

The core of this system is the **Ultimate Personal Assistant** workflow, which serves as the central orchestration layer. Rather than executing all tasks monolithically, it analyzes natural language requests and intelligently delegates operations to specialized agents based on intent.

### Specialized Agents

The ecosystem consists of the following modular workflows:

1.  **Email Agent** (`My_Email.json`)
    *   **Function**: Drafts emails, sends correspondence, and summarizes inbox threads.
    *   **Example Usage**: "Draft an email to John regarding the Q3 meeting."

2.  **Calendar Agent** (`My_Calendar.json`)
    *   **Function**: Manages scheduling, checks availability, and modifies appointments.
    *   **Example Usage**: "Schedule a call with Sarah next Tuesday at 2 PM."

3.  **Contact Agent** (`My_Contact.json`)
    *   **Function**: Acts as a CRM interface to retrieve, update, or add contact details.
    *   **Integration**: Automatically invoked by Email and Calendar agents to resolve contact information.

4.  **Content Creator** (`My_content_creater.json`)
    *   **Function**: Generates blog posts, social media captions, and creative copy.
    *   **Example Usage**: "Write a LinkedIn post about the future of local AI."

5.  **Web Search** (Tavily Integration)
    *   **Function**: Performs live web searches to retrieve up-to-date information for query resolution or content enrichment.

## Operational Logic

The workflow follows a structured decision-making process:

1.  **Input Processing**: The user submits a request via the n8n Chat interface.
2.  **Intent Analysis**: The primary AI model (powered by Ollama/Llama 3) evaluates the request to determine the necessary actions.
    *   *Scenario*: "Send an email to Nate asking when he wants to leave."
3.  **Execution Chain**:
    *   The Assistant identifies a missing email address and invokes the **Contact Agent**.
    *   The **Contact Agent** retrieves the required email address.
    *   With all necessary information available, the Assistant invokes the **Email Agent**.
    *   The **Email Agent** drafts and sends the email.
4.  **Response**: The Assistant confirms the successful execution of the task to the user.

## Project Structure

```text
workflows/
├── Ultimate Personal Assistant.json  # Central Orchestrator
├── My_Email.json                     # Email Sub-workflow
├── My_Calendar.json                  # Calendar Sub-workflow
├── My_Contact.json                   # Contact Management Sub-workflow
└── My_content_creater.json           # Content Generation Sub-workflow
```

## Setup & Configuration

1.  **Import Workflows**:
    *   Import all JSON files from the `workflows/` directory into your n8n instance.
2.  **Credential Configuration**:
    *   Ensure **Ollama** credentials are correctly configured in n8n.
    *   Configure service-specific credentials (e.g., Gmail, Google Calendar, Tavily API) required by the sub-agents.
3.  **Execution**:
    *   Open the **Ultimate Personal Assistant** workflow.
    *   Select the **Chat** interface to begin interaction.

## AI Model Integration

This workflow is optimized for local Large Language Models (LLMs) via **Ollama** (e.g., Llama 3, Mistral, or Qwen), ensuring data privacy and low-latency performance.
