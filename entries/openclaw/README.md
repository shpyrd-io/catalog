# OpenClaw

The open-source assistant: one gateway that answers on WhatsApp,
Telegram, Discord, Slack and more, with a Control UI for chat, sessions,
channels and configuration. Skills, memory and sessions live on the
project's disk.

The first visit after the install is a short setup: where the model
comes from (OpenRouter, Anthropic, or any OpenAI-compatible server), the
key, and the model, chosen from what the provider offers for that key.
Then the address is the Control UI, with the platform's sign-in as the
only login.

Channels come after. In the Control UI's channel settings, or from a
shell on the project: `openclaw channels add --channel telegram --token
<token>`, `openclaw channels login` for WhatsApp's QR code.
