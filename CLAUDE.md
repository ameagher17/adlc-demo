# adlc-demo — repo guide for Claude

Agentforce Service Agent demo repo: Agentforce Service Agent (API name `AVA`) /
`AVA_Voice_Agent2` work for a generic customer org.

## Naming: never say "AVA" out loud

The agent's underlying Salesforce **API name is still literally `AVA`** (bot
developer name, `AVA_Voice_Agent2` bundle, and other metadata identifiers
throughout `salesforce/`) — that's a technical identifier and it is **not**
being renamed, because renaming it would break metadata cross-references and
deployability.

But the agent's **display/spoken name has been renamed to "Agentforce Service
Agent"** in the actual orgs. When talking to the user:

- **Never say "AVA"** in your responses. Refer to the agent as **"the
  Agentforce Service Agent"** (or "the voice agent" / "the chat agent" when
  disambiguating between `AVA` and `AVA_Voice_Agent2`).
- Same rule for **`AVA_Voice_Agent`** — the sibling voice agent living in the
  reference org `org2` (seeded to mirror `org1`'s dashboard numbers; see
  `context/CONTEXT.md`). Don't say "AVA_Voice_Agent" in your prose either —
  call it "the voice agent" (or disambiguate by org, e.g. "org2's voice
  agent") instead. Don't confuse it with `AVA_Voice_Agent2`, the one actively
  developed in `org1` and documented under `context/agent/`.
- It's fine to reference the literal string `AVA` or `AVA_Voice_Agent` when
  it's unavoidably part of a technical artifact you're quoting or
  instructing the user to use verbatim — a file path, a `--api-name` flag, a
  SOQL filter, a developer name in metadata. Don't editorialize those away;
  just don't use them as the agent's name in your own prose.

## Start here

- **[`context/CONTEXT.md`](context/CONTEXT.md)** — narrative summary of the org
  migration, dashboard seeding gotchas, the agent-renaming trap, the
  Troubleshooting subagent design, and the test suites.
- **`salesforce/`** — the full SFDX project. This is the live/working project;
  **edit here going forward**. Files under `context/` are quick-reference copies.

## Answering questions about the agents

- **"What does the Troubleshooting subagent do?"** → answer from
  **[`context/agent/TROUBLESHOOTING_SUBAGENT.md`](context/agent/TROUBLESHOOTING_SUBAGENT.md)**
  (the customer-facing flow: offer → reboot → one automatic retry → resolution
  check → escalate). `context/CONTEXT.md` §4 has the implementation-level
  detail; `context/agent/AVA_Voice_Agent2.agent` is the source of truth.
- Agent Script source of truth is
  `salesforce/force-app/main/default/aiAuthoringBundles/AVA_Voice_Agent2/AVA_Voice_Agent2.agent`
  (kept identical to `context/agent/AVA_Voice_Agent2.agent`) — if the two
  diverge, trust the `salesforce/` copy and re-sync the `context/` one.

## Never commit

`.sf/`, `.sfdx/`, and `salesforce/observability/.dcenv*` (Data Cloud
client-credential secrets) are gitignored on purpose.
