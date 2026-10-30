# Medicai Agent Skills

Skills that teach AI coding assistants (Claude Code, Claude.ai, Cursor, Codex, GitHub Copilot, Gemini CLI, and anything else that reads the [Agent Skills](https://agentskills.io) format) how to build on [Medicai](https://www.medicai.io), the cloud medical imaging and documents platform.

One skill today:

| Skill | What it covers |
|---|---|
| `medicai-integration` | Login with Medicai and token handling, embedding the DICOM viewer (including a no-account demo viewer), uploading studies to the cloud PACS, cases and sharing (including patient access), cloud documents, webhooks, Medicai concepts, when a project needs more than the trial or the standard API offers, and a migration guide for integrations written against the pre-October-2026 routes |

The skill contains documentation and example code only: no scripts that run on install, no hooks, no telemetry, no credentials. Read `skills/medicai-integration/SKILL.md` to see exactly what an assistant is told.

## Install

**Claude Code** (this repository is also a plugin marketplace):

```
/plugin marketplace add Medicai-io/skills
/plugin install medicai@medicai
```

For a local checkout, `/plugin marketplace add /path/to/skills` works the same way.

**Claude.ai and Claude desktop**: zip the `skills/medicai-integration` folder and upload it under Settings > Capabilities > Skills (Team and Enterprise admins can publish it to the organization library).

**Cursor, Codex, Copilot, Gemini CLI, Windsurf, Cline and others**: the [skills.sh](https://skills.sh) CLI detects your agent and copies the skill into the folder it reads (`.agents/skills/`, `.claude/skills/`, and so on):

```
npx skills add Medicai-io/skills
```

Or copy `skills/medicai-integration` into your project's `.agents/skills/` folder by hand.

## Before you start building

You need a Medicai account and workspace; the 15-day trial (card at signup, nothing billed until it ends) starts at https://www.medicai.io/free-trial. Without an account, the skill can still embed Medicai's public demo viewer and the local-files viewer. Once you have a workspace, the skill tells you which credentials to collect and where to find them in the app, and asks you to have your app's origin whitelisted before embedding the authenticated viewer.

Prototypes run on synthetic or anonymized data. Real patient data belongs on a paid plan with the appropriate data-processing agreement; the skill reminds users of this once when it matters.

## Repository layout

```
.claude-plugin/
  plugin.json          plugin manifest (Claude Code)
  marketplace.json     lets this repo be added as a marketplace
skills/
  medicai-integration/
    SKILL.md           the entry point (router, rules, quickstart, pitfalls)
    references/        one file per flow, loaded on demand
    evals/             test cases in the `claude plugin eval` layout
CHANGELOG.md
LICENSE
```

## Testing

```
claude plugin validate --strict .
claude plugin eval ./skills/medicai-integration --allow-tools Write,Edit,Bash
```

The eval cases are realistic prompts (embed a study in a Next.js page, upload a CD folder to the PACS, share results with a patient, and view DICOM files in the browser without naming Medicai). Their graders check that the skill triggers without the brand name, that generated code uses workspace-scoped routes, keeps long-lived credentials server-side, sends the client header and numeric study ids, offers the no-account viewer first, and defaults patient sharing to password-protected links. Every API flow the skill documents was exercised against the live platform before release, except webhooks, which follow the published specification.

## Feedback and support

Found something the skill gets wrong, or an API behavior it does not cover? Open an issue in this repository. For account, plan, or origin-whitelisting requests, contact the Medicai team through the app or https://www.medicai.io.

## Versioning

The skill version lives in three places that must agree: `.claude-plugin/plugin.json`, the `metadata.version` field in `SKILL.md`, and `CHANGELOG.md`. Bump all three together.

## License

MIT. See `LICENSE`.
