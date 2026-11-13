# Hermes Agent

Nous Research's open-source agent: a CLI, a web dashboard with chat, and
a gateway that answers on Telegram, Discord, Slack, WhatsApp and more.
Skills, memories and sessions live on the project's disk.

The first visit after the install is a short setup: where the model
comes from (OpenRouter, Anthropic, or any OpenAI-compatible server), the
key, and the model, chosen from what the provider offers for that key.
Then the address is the dashboard.

Channels come after. In the dashboard's Channels page, a bot token and
the people allowed; or from a shell on the project with
`hermes gateway setup`, which is also where WhatsApp's QR code is
scanned. Hermes wants a model with a context of 64,000 tokens or more.
