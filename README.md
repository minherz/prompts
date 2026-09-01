# AI Agent Skills and Directives

![Repo license](https://badgen.net/badge/license/Apache%202.0/blue)

A centralized repository of system rules, modular skills, and directives packaged as a native Antigravity plugin for agentic AI workflows.

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
│   ├── engineering/         # Software design, building, and deployment skills
│   ├── in-progress/         # Pre-release skills undergoing testing
│   └── retired/             # Deprecated or legacy skills
├── AGENTS.md                # System rules & skill installation protocols
├── CLAUDE.md                # Pointer to AGENTS.md
├── LICENSE                  # Apache 2.0 License
├── plugin.json              # Antigravity plugin package manifest
└── README.md
```

---

## ⚖️ System Rules

Rules in `rules/` are foundational behavioral directives that apply universally across **all** agent interactions:

| Rule | File | Version | Purpose |
| :--- | :--- | :--- | :--- |
| **Matter-of-Fact** | [`rules/matter-of-fact.md`](./rules/matter-of-fact.md) | `1.0.0` | Enforces compact, concise, and terse communication by eliminating conversational "lyrics" (flattery, apologies, unrequested self-justifications, and pleasantry boilerplate). |
| **Self-Reviewer** | [`rules/self-reviewer.md`](./rules/self-reviewer.md) | `1.0.0` | Enforces operational safety via a Plan & Confirmation Gate (no workspace/data modifications prior to explicit user approval) and a No-Guessing Mandate (clarifying missing context or multiple options). |

---

## 🛠 Modular Skills

Skills in `skills/` are on-demand capabilities packaged with a `SKILL.md` instruction file containing YAML frontmatter:

| Skill | Bucket | Version | Description |
| :--- | :--- | :--- | :--- |
| **`devrel-content-generator`** | `devrel` | `1.0.0` | Crafts energetic, tech-savvy conference proposals, blog outlines, video/podcast scripts, and Nano Banana 2 image prompts featuring Google Cloud platforms. |
| **`devrel-content-reviewer`** | `devrel` | `1.0.0` | Multi-modal review tool for developer advocacy content (text, images, videos, audio, web) enforcing grammar, pronoun consistency, logical flow, title clarity, audience depth, runnable code, and actionable conclusions. |

---

## 🔌 Installing as an Antigravity Plugin (Recommended)

This repository includes a root [`plugin.json`](./plugin.json) manifest, making it installable as a self-contained Antigravity plugin that bundles both rules and skills.

### Package Manifest (`plugin.json`)

```json
{
  "name": "leoy-skill-toolkit",
  "version": "1.0.0",
  "description": "Comprehensive skills and system rules for developer advocacy and engineering tasks.",
  "repository": "https://github.com/minherz/skills",
  "license": "Apache-2.0",
  "disabled": false
}
```

---

### Installation Options

#### Option A: Workspace Plugin via Git Submodule (Best for Teams)
In the root of your target project repository:

```bash
git submodule add https://github.com/minherz/skills.git .agents/plugins/leoy-skill-toolkit
```
*Team members automatically get the plugin and its updates when running `git submodule update --init`.*

#### Option B: Workspace Plugin via `.agents/plugins.json` (Local Clone Reference)
If you have cloned this repository locally (e.g., to `~/workdir/skills`), add it to your project's `.agents/plugins.json`:

```json
{
  "entries": [
    {
      "path": "~/workdir/skills"
    }
  ]
}
```

#### Option C: Machine-Wide Global Plugin (All Projects)
To make the rules and skills active across all Antigravity sessions on your machine:

1. Symlink or clone the repository to your global plugin directory:
   ```bash
   mkdir -p ~/.gemini/config/plugins
   ln -s ~/workdir/skills ~/.gemini/config/plugins/leoy-skill-toolkit
   ```
2. Or register it in `~/.gemini/config/plugins.json`:
   ```json
   {
     "entries": [
       {
         "path": "~/workdir/skills"
       }
     ]
   }
   ```

#### Option D: Standalone Extraction via `npx degit`
To pull a clean copy directly into your project's plugin folder without Git history:

```bash
npx degit minherz/skills .agents/plugins/leoy-skill-toolkit
```

---

## 📦 Installing Individual Skills (Alternative)

If you only need specific skills without installing the full plugin bundle:

### 1. Workspace Scope (`.agents/skills.json`)
```json
{
  "entries": [
    {
      "path": "~/workdir/skills/skills/devrel"
    }
  ]
}
```

### 2. Single Skill Extraction
```bash
npx degit minherz/skills/skills/devrel/devrel-content-generator .agents/skills/devrel-content-generator
```

---

## 📜 Contributing & Adding New Skills

When adding new skills to this repository:

1. Refer to [`AGENTS.md`](./AGENTS.md) for category bucket assignments (`devrel/`, `engineering/`, `in-progress/`, `retired/`).
2. Follow single-skill extraction guidelines when importing from external repositories.
3. Ensure `SKILL.md` contains valid YAML frontmatter with `name`, `version`, and `description`.
