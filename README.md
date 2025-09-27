
# Voice_AI_Agents

## Description
Voice_AI_Agents is a repository showcasing two voice-based AI projects built with real-time interaction capabilities. The system combines several core tools: **LiveKit** for managing voice sessions and agent orchestration, **Cartesia** for speech-to-text (STT) and text-to-speech (TTS), **Silero** for Voice Activity Detection (VAD) to detect when a user is speaking, and **Cerebras LLM (LLaMA 3.3-70B)** for natural language understanding and response generation. These tools work together to create domain-specific conversational agents for telecom customer support and sales interactions.

## Workflow
The workflow begins when a user speaks into the system. **Silero VAD** detects when speech starts and ends, and the audio is processed by **Cartesia** to transcribe it into text. The transcribed input is passed to the **Cerebras LLM**, which uses predefined context files (`telecom.json` or `products.json`) to generate accurate, context-aware responses. The output is then converted back to speech by **Cartesia TTS**, and **LiveKit** manages the overall session, including seamless transfers between specialized agents such as customer care, technical support, billing, sales, technical, or pricing agents. This creates smooth, natural, and multi-agent conversational experiences.

## Features
- **Real-Time Voice Interaction**: Low-latency speech-to-text and text-to-speech for natural conversations.
- **Multi-Agent System**: Specialized agents (Customer Care, Technical Support, Billing for Telecom; Sales, Technical, Pricing for Sales) with transfer capabilities.
- **Context-Driven Responses**: Agents use predefined context files (`telecom.json` for Telecom, `products.json` for Sales) to ensure accurate, non-hallucinated responses.
- **Modular Architecture**: Easily extensible with additional agents or integrations.
- **Logging**: Detailed logs for debugging and tracking agent transfers.

## Prerequisites
- **Python 3.8+**: Required for running both projects.
- **Git**: For cloning the repository.
- **API Keys**:
  - **Cartesia API Key**: For STT and TTS functionality (obtain from [Cartesia](https://cartesia.ai)).
  - **Cerebras API Key**: For LLM access (obtain from [Cerebras](https://www.cerebras.ai)).
- **Jupyter Environment**: Optional, for running the provided Jupyter-based interface.
- Internet access to download context files (`telecom.json`, `products.json`).

## Installation
1. **Clone the Repository**:
   ```
   git clone https://github.com/kalyani234/Voice_AI_Agents.git
   cd Voice_AI_Agents
   ```
2. **Create a Virtual Environment** (recommended):
   ```
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\\Scripts\\activate
   ```
3. **Install Dependencies**:
   ```
   pip install livekit-agents livekit-agents[cartesia,silero,openai]
   ```
4. **Set API Keys**:
   Replace placeholder API keys in the respective project scripts:
   ```
   CARTESIA_API_KEY = "your-cartesia-api-key"  # Replace with valid Cartesia key
   CEREBRAS_API_KEY = "your-cerebras-api-key"  # Replace with valid Cerebras key
   os.environ["CARTESIA_API_KEY"] = CARTESIA_API_KEY
   os.environ["CEREBRAS_API_KEY"] = CEREBRAS_API_KEY
   ```
   **Note**: Ensure API keys have sufficient credits to avoid 402 errors.

5. **Download Context Files**:
   Context files are automatically downloaded during execution:
   - Telecom: `telecom.json` (from [telecom](https://gist.githubusercontent.com/kalyani234/88f526a439b0e748b6f83e0a966ce75f/raw/telecom.json))
   - Sales: `products.json` (from [products](https://gist.githubusercontent.com/ShayneP/f373c26c5166d90446f2bc08baf9bf46/raw/products.json))
   Alternatively, manually place these files in the `context/` directory.

## Project Structure
```
Voice_AI_Agents/
├── context/                    # Directory for context files (telecom.json, products.json)
├── telecom_customer_support/    # Telecom Customer Support Agent
│   └── telecom_agent.py        # Main script for telecom multi-agent system
├── voice_sales_agent/          # Voice Sales Agent
│   └── sales_agent.py          # Main script for sales multi-agent system
├── telecom_agent_transfers.log # Log file for telecom agent interactions
├── agent_transfers.log         # Log file for sales agent interactions
├── requirements.txt            # Shared dependencies
└── README.md                   # This file
```

## Telecom Customer Support Agent
### Overview
This project implements a multi-agent system for telecom customer support, with three specialized agents:
- **Customer Care Agent**: Handles service upgrades, complaints, plan changes, new subscriptions, and general account management.
- **Technical Support Agent**: Addresses network issues, device setup, roaming, and outages.
- **Billing Agent**: Manages billing, payments, refunds, plans, and invoice queries.

### Usage
1. **Run the Telecom Agent**:
   ```
   python telecom_customer_support/telecom_agent.py
   ```
   Or, in a Jupyter environment, execute the notebook cells provided in the code.
2. **Interact with the Agent**:
   - Start with the Customer Care Agent.
   - Example queries:
     - "I want to change my plan" (handled by Customer Care Agent).
     - "My internet is slow" (transfers to Technical Support Agent).
     - "I need a refund" (transfers to Billing Agent).
3. **Check Logs**:
   View `telecom_agent_transfers.log` for transfer and error details.

### Context
The agent uses `telecom.json` for company information, including services, pricing, objection handlers, and support scenarios (e.g., `refund_request`, `invoice_query`, `complaint_handling`, `new_subscription`).

## Voice Sales Agent
### Overview
This project implements a multi-agent system for sales interactions, with three specialized agents:
- **Sales Agent**: Handles general sales inquiries and product information.
- **Technical Agent**: Answers technical details and specifications.
- **Pricing Agent**: Manages pricing, budgets, and discount-related queries.

### Usage
1. **Run the Sales Agent**:
   ```
   python voice_sales_agent/sales_agent.py
   ```
   Or, in a Jupyter environment, execute the notebook cells provided in the code.
2. **Interact with the Agent**:
   - Start with the Sales Agent.
   - Example queries:
     - "Tell me about your products" (handled by Sales Agent).
     - "How does it work?" (transfers to Technical Agent).
     - "How much is it?" (transfers to Pricing Agent).
3. **Check Logs**:
   View `agent_transfers.log` for transfer and error details.

### Context
The agent uses `products.json` for product details, ensuring accurate responses based on provided data.

## Troubleshooting
- **402 Errors**: Verify Cartesia API key has sufficient credits.
- **Context File Errors**: Ensure `telecom.json` or `products.json` is correctly downloaded to the `context` directory.
- **Agent Transfer Failures**: Check log files (`telecom_agent_transfers.log` or `agent_transfers.log`) for details.
- **Jupyter Issues**: Confirm the Jupyter URL (`https://jupyter-api-livekit.vercel.app/api/join-token`) is accessible.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details. (Create this file if needed.)

## Contact
For questions or support, create a GitHub issue or contact [kalyani234](https://github.com/kalyani234).

