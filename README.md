# Growth OS for Claude Cowork — Quick Start

Build your AI-powered business workspace in one session. This plugin walks you through a guided setup that creates your core documents, scaffolds your folder structure, and delivers a personalized morning routine, so you can start using Claude as a daily business tool immediately.

## What It Does

The Quick Start creates a complete Growth OS for Claude Cowork workspace with:

- **Offers document** — your products, pricing, and positioning
- **Persona document** — your ideal customer with pain/pleasure quote tables
- **Morning routine** — a personalized daily briefing you trigger by saying "good morning"
- **CLAUDE.md** — the operational guide that ties everything together

It crawls your website first to pre-fill as much as possible, then interviews you to refine and complete each document.

## How to Use

1. Install the plugin in Claude Cowork
2. Say "run the quick start" or type `/quick-start`
3. Answer the questions (name, business name, website URL)
4. Claude drafts your documents from your website, you confirm and adjust
5. When all three core documents and the morning routine are done, you're finished

The whole process takes 15-30 minutes.

## What's Required vs. Optional

**Required (Tier 1):** Offers, Persona, Morning Routine. Completing these means the Quick Start is done and your workspace is fully functional.

**Optional (Tier 2):** Business Info, Brand Voice, Brand Design, Content Rules. These enhance your workspace but aren't required. Say "enhance my workspace" any time to add them.

## Components

| Component | Type | Description |
|---|---|---|
| `/quick-start` | Command | Starts or resumes the guided setup |
| `quick-start` | Skill | The full setup playbook with 5 phases |

## Multi-Session Support

The Quick Start tracks progress in a `progress.md` file. If you close the session and come back later, Claude picks up exactly where you left off. No need to start over.

## Example Files

The plugin includes example documents from a fictional business called "Greenline Digital" so you can see what good output looks like before you start. These are reference only and won't appear in your workspace.
