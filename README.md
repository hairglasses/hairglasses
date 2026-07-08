## Mitch Not Mitchell

Agent-infrastructure engineer in San Francisco. I build Go tooling for AI-agent runtimes: MCP servers, durable execution and crash recovery, multi-provider coding-agent orchestration, and the reliability primitives that keep long-running autonomous agents from falling over.

Most production repositories stay private — they carry workstation, account, tenant, or operational detail. What's public below is the real engineering, either as first-party libraries or as sanitized slices that show the patterns without exposing private systems. If you're reviewing from a résumé or LinkedIn, the [contribution graph](https://github.com/hairglasses) shows cadence; the repos below show the implementation.

### Start here

**[mcpkit](https://github.com/hairglasses-studio/mcpkit)** — production Go framework for building MCP servers. 72 packages, 85%+ coverage: typed tool contracts, middleware chains, RBAC + audit, FinOps/token budgeting, circuit breakers, gateway aggregation, workflow/saga engine, eval harness. Consumed as a dependency by the MCP servers below. *(This is the real framework — the earlier `open-mcpkit` was a stub; this replaces it.)*

### Standalone components — extracted from production agent infrastructure

Each is a self-contained, tested Go module carved out of a larger private control-plane, decoupled from its origin and published on its own.

| Repo | What it does |
| --- | --- |
| [durable-recovery](https://github.com/hairglasses-studio/durable-recovery) | Deterministic plan → bounded-executor crash recovery & power-loss resume, with a tamper-evident hash-chained decision journal + replay. |
| [hook-runner](https://github.com/hairglasses-studio/hook-runner) | Governed hook-execution engine for agent tool-use: declarative `hooks.yaml`, typed lifecycle events, sync/async with timeouts + budget gating. |
| [agentloop](https://github.com/hairglasses-studio/agentloop) | Perpetual autonomous-agent control loop — a guarded Plan→Execute→Evaluate→Improve FSM with a threshold-driven budget enforcer. |
| [leasequeue](https://github.com/hairglasses-studio/leasequeue) | Crash-safe two-phase lease protocol with fencing tokens and TTL reaping for coordinating work across unreliable workers. |
| [mcp-gateway](https://github.com/hairglasses-studio/mcp-gateway) | JSON-RPC reverse-proxy gateway for MCP servers: composable audit→auth→rate-limit→route middleware with per-provider circuit breakers. |
| [worktree-isolate](https://github.com/hairglasses-studio/worktree-isolate) | Git-worktree lifecycle for fleets of parallel agents: create/list/remove, squash-mergeback with conflict reporting, collision-free port/DB/tmp allocation. |
| [agent-consensus](https://github.com/hairglasses-studio/agent-consensus) | A "quorum before an agent acts" primitive: content-addressed proposals, leader election on duplicates, timeout/dissent escalation. |
| [agent-patterns](https://github.com/hairglasses-studio/agent-patterns) | Coordination primitives for multi-agent sessions: role orchestration, a durable message queue, hot/warm/cold shared memory. |
| [provider-quota](https://github.com/hairglasses-studio/provider-quota) | Parse LLM rate-limit headers (Anthropic/OpenAI/Google) into a normalized [0,1] headroom signal, with a sliding-window fallback. |
| [provider-shim](https://github.com/hairglasses-studio/provider-shim) | Normalize Claude/Codex/Gemini behind one Shim interface + Registry — capability-matrix strategy instead of switch-on-provider. |
| [browserctl](https://github.com/hairglasses-studio/browserctl) | Native Chrome DevTools Protocol reliability facade: endpoint canonicalization, wedge/drift detection, remote re-routing for long-lived automation. |
| [syspressure](https://github.com/hairglasses-studio/syspressure) | Cross-platform system-pressure classifier over load + memory + disk + goroutines, with a clean Linux/Darwin build-tag seam. |

### MCP servers (built on mcpkit)

- **[process-mcp](https://github.com/hairglasses-studio/process-mcp)** — OS process inspection and management.
- **[systemd-mcp](https://github.com/hairglasses-studio/systemd-mcp)** — systemd user/service control.
- **[tmux-mcp](https://github.com/hairglasses-studio/tmux-mcp)** — tmux session and pane control.
- **[dotfiles-mcp](https://github.com/hairglasses-studio/dotfiles-mcp)** — dotfiles management and sync.

### Agent tooling

- **[codexkit](https://github.com/hairglasses-studio/codexkit)** — fleet toolkit for agent repos: baseline validation, skill-surface sync, MCP/profile projection, workspace hygiene.
- **[glass](https://github.com/hairglasses-studio/glass)** — multi-provider TUI for coding agents (Claude/Codex/Gemini/Copilot).

### Sanitized slices of private systems

- **[open-ralphglasses](https://github.com/hairglasses/open-ralphglasses)** — public seed of a multi-provider agent control-plane: provider discovery, launch planning, hook review, loop planning, MCP-style tool contracts. (The components above were extracted from the private system this mirrors.)
- **[open-career-mcp](https://github.com/hairglasses/open-career-mcp)** — synthetic-data career-workflow MCP: résumé tailoring, opportunity review, interview prep, dry-run approval boundaries.
- **[open-workstation-mcp](https://github.com/hairglasses/open-workstation-mcp)** — Linux/Wayland workstation-automation patterns: synthetic readiness snapshots, dry-run focus/input plans, config-drift summaries.

### Focus areas

- Go frameworks for MCP servers and typed tool contracts
- Durable execution: checkpointing, crash recovery, power-loss resume, tamper-evident journaling
- Multi-provider agent orchestration across Claude, Codex, Gemini, and Copilot
- Reliability primitives for autonomous agents: leases, quorum, rate-limit headroom, circuit breakers
- Security-conscious publishing — sanitized fixtures, no tenant or credential data

### Note on private work

My highest-velocity work (agent runtimes, a fleet control-plane, a job-search platform) is private because it's entangled with operational and personal data. The repos here are the parts I could cleanly separate and stand behind on their own. Happy to walk through the private architecture in an interview.
