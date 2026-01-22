# WhatsApp Gemini Chatbot (n8n Workflow)

This project contains an n8n workflow that integrates WhatsApp with Google's Gemini AI to create a customizable chatbot. Users can interact with the Gemini model directly through WhatsApp.

## Description

This workflow enables a WhatsApp number to function as an AI chatbot powered by Google Gemini. It receives messages via a webhook, processes them, fetches configuration (system prompt/personality) from a Google Sheet, queries the Gemini model, and sends the response back to WhatsApp.

## Features

- **WhatsApp Integration:** Seamless communication via WhatsApp. Uses **WAHA (WhatsApp HTTP API)** for integration, providing a simpler alternative to the official WhatsApp Business API.
- **Google Gemini Power:** Uses the `gemini-2.5-flash` model for intelligent responses.
- **Custom Personality:** The chatbot's personality (System Prompt) is configurable via a Google Sheet.

## Prerequisites

To use this workflow, you need:

1. **n8n Instance:** Self-hosted or cloud version.
2. **Google Gemini API Key:** To authenticate with Google's AI services.
3. **Google Cloud Service Account:** Currently used for authenticating with Google Sheets.
4. **Google Sheet:** Used to store configuration (specifically the `SystemPrompt` Key).
5. **WhatsApp API Service:** A service that exposes a webhook and an API to send messages (e.g., WAHA, whatsapp-web.js). The workflow assumes an API running on port 3001 locally or accessible via network.

## Workflow Overview

The workflow consists of the following nodes:
1. **Webhook:** Receives incoming WhatsApp messages.
2. **Filter:** Ensures the message is not from the bot itself.
3. **Google Sheets:** Fetches the `SystemPrompt` to define the AI's behavior.
4. **Google Gemini:** Sends the user's message and system prompt to the AI model.
5. **HTTP Request:** Sends the generated response back to the user via the WhatsApp API.

## Usage

1. Import the `n8n_Gemini_Chatbot_Workflow.json` file into your n8n instance.
2. Configure the credentials for:
   - Google Sheets (Service Account)
   - Google Gemini API
   - HTTP Header Auth (if required by your WhatsApp API)
3. Update the **HTTP Request** node URL to point to your WhatsApp API endpoint.
4. Set up your Google Sheet with a `Key` column containing "SystemPrompt" and a `Value` column with your desired persona.

## Current Limitations

- **No Interaction History:** The bot currently treats every message as a new, isolated interaction. It does not possess memory of previous messages in the conversation.
- **Single Turn:** Context is not maintained across multiple messages.
- **Authentication:** Currently relies on Service Account credentials for Google Sheets.

## Roadmap / Next Steps

- [ ] **Add Database:** Implement a database connection to store conversation history, enabling memory and context retention for the chatbot.
- [ ] **Security Upgrade:** Migrate Google Sheets authentication from "Service Account" to "OAuth2" for better security practices.
- [ ] **Enhanced Personality:** Develop more detailed and dynamic personality configurations.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
