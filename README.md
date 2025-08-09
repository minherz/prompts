# Prompts

![Repo license](https://badgen.net/badge/license/Apache%202.0/blue)

_Prompts_ repository is a collection of prompts and configurations used with various GenAI tools.
Consult with [LICENSE](LICENSE) when copying files and using content of this repository.

## Repository structure

The repository contains the following components:

```text
/
├── ai_studio/              # Prompts and utilities for use with Google AI Studio
│
└── gemini_cli/             # Configurations, context files and prompts for use with Gemini CLI
```

### Google AI Studio

[Google AI Studio](https://aistudio.google.com/) is a web-based application giving easy access to a variety of Google's family of multimodal generative AI models.
It offers an unlimited free tier to the latest models with low rate call limit for testing purposes.
It requires to sign-in using a Google account (e.g. a personal Gmail account).

See details in [ai_studio/README](ai_studio/README.md).

### Gemini CLI

[Gemini CLI](https://cloud.google.com/gemini/docs/codeassist/gemini-cli) is a command line interface to the [open source](https://github.com/google-gemini/gemini-cli) AI agent.
Like AI Studio, it requires sign-in using a Google account.
Its free tier is limited to a certain amount of tokens per day (TODO: need to provide a reference to official documentation).

See details in [gemini_cli/README](gemini_cli/README.md).
