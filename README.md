# Agent Skills in Action (Official Repository)

Welcome to the official codebase for the Manning book **[Agent Skills in Action](link-to-manning-page-when-live)**. 

This repository is not a collection of monolithic, fragile Python scripts with hardcoded prompts. It is a strictly structured, enterprise-grade workspace demonstrating how to build portable, deterministic AI capabilities using the `SKILL.md` open standard. 

## The Mission
As the industry moves beyond weekend AI prototypes into production infrastructure, we can no longer rely on massive, unmaintainable system prompts. This book and this repository treat the "Agent Skill" as the fundamental unit of deployment: an isolated, versionable package that securely encapsulates an API tool, its exact operating procedure, and its execution boundaries.

## The "Laptop Test" Promise
Every skill directory in this repository is designed to pass **The Laptop Test**.
The logic is entirely decoupled from the environment. You can zip any `skills/` folder found in these chapters, drop it into your own local project, and run it securely—without altering a single line of the underlying code. 

## Repository Architecture
This project is organized by chapter. Within each chapter, you will find the isolated `skills/` directories containing the interface contracts (`SKILL.md`), the stateless execution logic (`scripts/`), and the necessary data schemas. 

* **Chapter 1 & 2:** Architecture foundations and the anatomy of `acme-refund-processor`.
* **Chapter 4:** Building remote execution boundaries using the Model Context Protocol (MCP).
* **Chapter 8:** Composing reusable domain packs for enterprise deployment.
*(Note: Code will be pushed iteratively as MEAP chapters are released).*

## Installing Skills Locally
This repository is fully compatible with the standard `skills` CLI package. Because our skills are categorized by chapter to follow the book's structure, you should use the `--skill` flag to extract the specific capability you are currently reading about.

For example, to install the Safe Refund Processor from Chapter 2 into your local agent (e.g., Cursor, Claude Code, or a custom runner), run:

```bash
npx skills add agentskills-io/agent-skills-in-action --skill safe-refund-processor
```
The CLI will locate the safe-refund-processor directory inside ch02_anatomy_of_a_skill/skills/, extract the SKILL.md and its execution scripts, and install them into your local .agents/skills/ workspace.

## Environment Setup & Configuration Injection
Because these skills enforce strict Separation of Concerns, they rely on **Configuration Injection**. No API keys or database URLs are hardcoded in this repository. 
Before running the local execution environments in Chapters 4+, you must copy the `.env.example` file to `.env` and provide your own credentials. The Host Agent runtime will securely inject these into the skills at execution time. 

## License
All open-standard skill structures and code examples are released under the [Apache 2.0 License](LICENSE), allowing you to freely integrate these architectural patterns directly into your enterprise systems.
