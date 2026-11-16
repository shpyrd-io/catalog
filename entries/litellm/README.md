# LiteLLM

BerriAI's open-source gateway: one OpenAI-compatible address in front of
the model providers (OpenAI, Anthropic, Bedrock, Vertex, a local server
and many more). Virtual keys with budgets and limits, spend per key and
team, fallbacks between models, and an admin UI.

The install asks the admin user's name and password and creates a
Postgres database for the project: models, keys and spend live there.

After the install, set the project's access to **Named people**
(`shpyrd access set identified --project litellm`). LiteLLM authenticates
its own clients with a key sent as a bearer, and the platform passes a
bearer that is not its own on to the application only in that mode. The
project is then open to the internet, and LiteLLM's keys are what protect
it.

Then `/ui` is the admin UI: sign in with the user and password given at
the install, add the models with their provider keys, and create a
virtual key for each application. Applications call the project's
address as they would call OpenAI, with their virtual key.

Another project of the workspace calls LiteLLM at its public address,
not at `http://litellm.internal`.

LiteLLM asks for 4Gi of memory, which the entry sets. It is built from
[shpyrd-io/litellm](https://github.com/shpyrd-io/litellm): the official
image, with a Dockerfile because LiteLLM is published as an image and
its keys need a prefix the install cannot generate.
