# AI Agent Skills and Directives

![Repo license](https://badgen.net/badge/license/Apache%202.0/blue)

A centralized repository of system rules, modular skills, and directives designed for Google Antigravity and agentic AI workflows.

---

## 📁 Repository Structure

```text
.
├── rules/                   # Universally active system rules
│   ├── matter-of-fact.md    # Enforces terse, high-signal, fluff-free responses
│   └── self-reviewer.md     # Enforces plan confirmation gates & no-guessing
├── skills/                  # Modular skill packages
│   ├── devrel/              # Developer advocacy and technical evangelism skills
│   │   ├── devrel-content-generator/# High-impact technical content generator for DevRel
│   │   └── devrel-content-reviewer/# Multi-modal review for developer advocacy content
│   └── retired/             # Deprecated or legacy skills
├── AGENTS.md                # System rules & skill installation protocols
├── CLAUDE.md                # Pointer to AGENTS.md
├── LICENSE                  # Apache 2.0 License
└── README.md
```

---

## ⚖️ System Rules

Rules in `rules/` are foundational behavioral directives that apply universally across **all** agent interactions:

| Rule | File | Purpose |
| :--- | :--- | :--- |
| **Matter-of-Fact** | [`rules/matter-of-fact.md`](./rules/matter-of-fact.md) | Enforces compact, concise, and terse communication by eliminating conversational "lyrics" (flattery, apologies, unrequested self-justifications, and pleasantry boilerplate). |
| **Self-Reviewer** | [`rules/self-reviewer.md`](./rules/self-reviewer.md) | Enforces operational safety via a Plan & Confirmation Gate (no workspace/data modifications prior to explicit user approval) and a No-Guessing Mandate (clarifying missing context or multiple options). |

---

## 🛠 Modular Skills

Skills in `skills/` are on-demand capabilities packaged with a `SKILL.md` instruction file containing YAML frontmatter:

| Skill | Bucket | Description |
| :--- | :--- | :--- |
| **`devrel-content-generator`** | `devrel` | Crafts energetic, tech-savvy conference proposals, blog outlines, video/podcast scripts, and Nano Banana 2 image prompts featuring Google Cloud platforms. |
| **`devrel-content-reviewer`** | `devrel` | Multi-modal review tool for developer advocacy content (text, images, videos, audio, web) enforcing grammar, pronoun consistency, logical flow, title clarity, audience depth, runnable code, and actionable conclusions. |

---

Antigravity and Gemini agents automatically discover and load rules and skills:

### 1. Workspace Scope (Project-Specific)

To make skills from this repository available within a specific project workspace:

**Option A: Reference via `skills.json` (Recommended)**  
Create or update `.agents/skills.json` in your project root:

```json
{
  "entries": [
    {
      "path": "/path/to/this-repo/skills/devrel"
    }
  ]
}
```

**Option B: Copy / Submodule into `.agents/skills/`**  
Follow the extraction protocols in [`AGENTS.md`](./AGENTS.md) to install individual skills:

```bash
# Using npx degit to install a single skill
npx degit <owner>/<repo>/skills/devrel/devrel-content-generator .agents/skills/devrel-content-generator
```

---

To make skills available machine-wide across all Antigravity sessions:

**Option A: Register in Global Config**  
Add the repository path to `~/.gemini/config/skills.json`:

```json
{
  "entries": [
    {
      "path": "/path/to/this-repo/skills/devrel",
      "include_only": ["devrel-content-generator", "devrel-content-reviewer"]
    }
  ]
}
```

```bash
mkdir -p ~/.gemini/config/skills
ln -s /path/to/this-repo/skills/devrel/devrel-content-generator ~/.gemini/config/skills/devrel-content-generator
```

---

## 🔌 Installing & Distributing via Plugins

### Why Use a Plugin?

- **Unified Distribution**: Packages rules (`rules/`), skills (`skills/`), lifecycle hooks (`hooks.json`), and MCP servers (`mcp_config.json`) into a single shareable bundle.
- **Easy Toggling**: Plugins can be enabled or disabled cleanly via configuration without moving files.
- **Namespacing**: Avoids naming collisions across team configurations.

### Plugin Layout

To package this repository or a subset as a plugin, add a `plugin.json` at the root of the plugin directory:

```text
my-custom-plugin/
├── plugin.json         # Required plugin manifest
├── rules/
│   ├── matter-of-fact.md
│   └── self-reviewer.md
├── skills/             # Bundled skills
│   ├── devrel-content-generator/
│   └── devrel-content-reviewer/
└── mcp_config.json     # Optional MCP server definitions
```

Sample `plugin.json`:

```json
{
}
```

### Registering the Plugin

- **Workspace Level**: Place in `.agents/plugins/my-custom-plugin` or declare in `.agents/plugins.json`:

  ```json
  {
    "entries": [
      { "path": "/path/to/my-custom-plugin" }
    ]
  }
  ```

- **Global Level**: Place in `~/.gemini/config/plugins/my-custom-plugin` or declare in `~/.gemini/config/plugins.json`.

---

## 📜 Contributing & Adding New Skills

When adding new skills to this repository:

1. Refer to [`AGENTS.md`](./AGENTS.md) for category bucket assignments (`devrel/`, `engineering/`, `in-progress/`, etc.).
2. Follow single-skill extraction guidelines when importing from external repositories.
3. Verify that `SKILL.md` contains valid YAML frontmatter (`name` and `description`).
