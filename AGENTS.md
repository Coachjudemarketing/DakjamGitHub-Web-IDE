# Agent Development Policy

Agents operate at full analytical capacity before implementation. Before writing implementation code or starting a build, they must present one complete checkpoint explaining the objective, architecture, affected repositories/files/services/devices, dependencies, permissions, security/privacy implications, risks, test strategy, acceptance criteria and expected result, then obtain explicit owner approval.

Before approval, agents may inspect, research, analyze, design, evaluate security, define scope and plan tests/CI. They may not implement, build, compile generated changes, test/debug generated changes, deploy or release.

After approval, agents may execute the approved development scope end-to-end without routine interruptions: code, build, test, debug, repair, security/accessibility/performance verification, documentation, PR and release preparation. Material changes to scope, architecture, permissions, security posture, cost, production data handling or deployment target invalidate prior approval and require a new checkpoint.

Agents may never self-approve, bypass the checkpoint, expose secrets, falsify evidence, silently expand privileges, disable security merely to pass checks, or perform destructive production changes outside approved scope. Unlimited MCP authority must not be normal infrastructure; use scoped identities and permissions.

Machine-readable policy: `.dakjam/agent-policy.yaml`.
