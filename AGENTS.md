# Agent Directives

## 1. System Rules

Agents operating in this repository must strictly adhere to the foundational behavioral and operational rules located in the `rules/` directory:

- **[`rules/matter-of-fact.md`](./rules/matter-of-fact.md)**: Mandates compact, concise, terse, and high-signal communication. Strictly eliminates conversational "lyrics" (user flattery/praise, apologies/admissions of oversight, unrequested defenses of previous answers, and pleasantry boilerplate).
- **[`rules/self-reviewer.md`](./rules/self-reviewer.md)**: Governs execution safety. Enforces a strict Plan & Confirmation Gate (no state-modifying actions without explicit user approval) and a No-Guessing Mandate (prompting for clarification when context is incomplete or when multiple choices exist).

---

## 2. Skills Organization & Taxonomy

Modular skills in this repository are categorized into domain bucket folders under `skills/`:

- `devrel/`: Developer advocacy, content creation, technical evangelism, and community outreach.
- `engineering/`: Software architecture, implementation, build systems, and deployment.
- `in-progress/`: Pre-release skills undergoing active experimentation and testing.
- `retired/`: Deprecated or legacy skills preserved for reference.

---

## 3. Installing Skills from GitHub

When adding or installing a skill from an external GitHub repository into this workspace, follow these protocols:

### A. Bucket Selection
- Identify the appropriate category bucket (`devrel/`, `engineering/`, `in-progress/`) based on the skill's purpose.
- Target directory path: `skills/<bucket>/<skill-name>/`

### B. Single-Skill Extraction Mandate (No Whole-Repo Bloat)
- If the source GitHub repository contains multiple skills or is a monorepo, **DO NOT** clone the entire repository into the bucket.
- Extract **only** the target skill directory.

### C. Recommended Installation Commands

#### Option A: `npx degit` (Fastest for subdirectories)
```bash
npx degit <owner>/<repo>/path/to/skill-folder skills/<bucket>/<skill-name>
```

#### Option B: `curl` + `tar` (Zero-dependency extraction)
```bash
mkdir -p skills/<bucket>/<skill-name>
curl -sL "https://github.com/<owner>/<repo>/tarball/<branch>" \
  | tar -xz -C "skills/<bucket>/<skill-name>" --strip-components=<depth> --wildcards "*/path/to/skill-folder/*"
```

#### Option C: `git clone` or Git Submodule (For dedicated single-skill repos)
```bash
# Direct clone:
git clone https://github.com/<owner>/<repo>.git skills/<bucket>/<skill-name>

# Or as a submodule:
git submodule add https://github.com/<owner>/<repo>.git skills/<bucket>/<skill-name>
```

---

## 4. Post-Installation Verification & Integrity

After extracting or cloning a skill:

1. **Verify Location**: Ensure `SKILL.md` resides directly at `skills/<bucket>/<skill-name>/SKILL.md` (no extra nested directory layers).
2. **Validate YAML Frontmatter**: Confirm `SKILL.md` starts with valid YAML frontmatter containing `name` and `description` fields:
   ```markdown
   ---
   name: <skill-name>
   description: <Clear description of what the skill does and when to trigger it>
   ---
   ```
3. **Clean Up**: Remove any unnecessary temporary files or extraneous repository files.
