# PRAXO-CORE for Zig

Zig 0.17 implementation of the PRAXO-CORE AI agent framework contract. The normative contract is [`spec/`](spec/README.md); Go remains the reference implementation.

## At a glance

| Field | Value |
| --- | --- |
| Package | `praxo-core-zig` |
| Registry | Source |
| Build | Source build (see README) |
| Source version | `0.8.0` |
| Published version | not published |
| Source tag | `zig/v0.8.0` |
| Tutorial tag | `zig/tutorial/v0.1.0` |
| Examples tag | `zig/examples/v0.1.0` |
| Tier | Core |
| Contract | `SPEC_VERSION` `0.2.0` |
| Documentation | https://axisvela.github.io/praxo-core/languages/zig/ |
| License | MIT |

## Highlights

- OpenAI-compatible model: native
- Anthropic model: native
- Gemini model: native
- MCP client: native
- Harmovela sink: native
- OpenTelemetry sink: native (transport seam)
- Subagent delegation: native (synchronous seam)
- Retriever: native

## Quick start

This implementation is source-only. Follow the build instructions in [`language/zig/README.md`](language/zig/README.md).

## What's included

| Capability | Status | Detail |
| --- | --- | --- |
| OpenAI-compatible model | native | `openaicompat.Adapter` with `std.http`; SSE streaming reassembly |
| Anthropic model | native | `anthropic.Adapter`; injectable transport; `generateStream` reassembles Anthropic SSE |
| Gemini model | native | `gemini.Adapter`; injectable transport; `generateStream` reassembles Gemini SSE |
| MCP client | native | `mcp.Client`; stdio and curl-backed `HttpTransport` for Streamable HTTP 2025-03-26 |
| Harmovela sink | native | `harmovela` |
| OpenTelemetry sink | native (transport seam) | `otel.Sink`; caller supplies OTLP/HTTP transport |
| Subagent delegation | native (synchronous seam) | `delegation.subagentRun`; no asynchronous manager |
| Retriever | native | `retriever.Document`, `retriever.Retriever`, `retriever.retrieveDocuments` |

## Examples

Runnable examples live under [`language/zig/examples`](language/zig/examples).

| Example | What it shows |
| --- | --- |
| [advanced-delegation](language/zig/examples/advanced-delegation) | Application-level parent/child delegation plus six governance negative checks. |
| [checkpoint](language/zig/examples/checkpoint) | This example uses the Zig Core checkpoint allowlist for a registered payload round trip. |
| [consumer](language/zig/examples/consumer) | This starter uses the Zig Core agent loop with a deterministic model. It does not require a network connection, credentials, or a model service. |
| [event-sink](language/zig/examples/event-sink) | This example uses Zig Core sink composition to fan out events and filter the tool-only stream. |
| [hitl](language/zig/examples/hitl) | This example demonstrates a write tool that requires human approval: |
| [identity-policy](language/zig/examples/identity-policy) | This example binds a trusted principal to policy decisions and rejects missing, role-mismatched, and tenant-mismatched actions. |
| [live-model](language/zig/examples/live-model) | This example connects the Zig Core OpenAI-compatible adapter to an OpenAI-compatible endpoint and registers one low-risk `get_time` tool. |
| [mcp](language/zig/examples/mcp) | This example uses a caller-owned in-process transport with the Zig MCP client. |
| [provider-fallback](language/zig/examples/provider-fallback) | This example calls a fallback only after the primary fails and preserves the primary failure when both fail. |
| [representative-chain](language/zig/examples/representative-chain) | Deterministic representative chain covering MCP record, final-argument authorization, governed child delegation, OTel/Harmovela events, and an edited denial with zero effects. |
| [retry](language/zig/examples/retry) | This example retries a transient failure with a bounded attempt count and keeps the exhausted failure state. |
| [service](language/zig/examples/service) | This example defines a transport-neutral request handler with health, principal, and run cases. |
| [session-checkpoint](language/zig/examples/session-checkpoint) | This example saves a session checkpoint in memory, restores it between agent turns, and continues the conversation. The deterministic model returns `turn <request message count>`. |
| [streaming](language/zig/examples/streaming) | This example accumulates streamed chunks and checks that they reconstruct the final output. |
| [structured-output](language/zig/examples/structured-output) | This example validates a final JSON answer against a schema and rejects invalid output. |

## Scenario Tutorials

Scenario-oriented tutorials live under `language/zig/Tutorial`.

| Path | What it shows |
| --- | --- |
| [Tutorial](language/zig/Tutorial) | Bounded Zig examples built on the native Core. Each tutorial is a small, runnable slice with explicit non-goals and an application-owned boundary; none is a complete industry pr... |
| [drone-fleet-plan](language/zig/Tutorial/drone-fleet-plan) | A bounded first slice of TL-01, not an airspace or flight-control system. It reads fixed drone waypoint state, drafts a review-only waypoint plan and flags a conflict zone for a... |
| [gateway-health](language/zig/Tutorial/gateway-health) | A scoped edge tutorial over the native MIT Zig Core. It reads one fixed `gateway-100` health snapshot through an application-owned `GatewayAdapter` function table and drafts an... |

## Verify

Run the checks from `language/zig`:

```bash
mkdir -p build
zig build-exe src/conformance.zig -O ReleaseSafe -femit-bin=build/conformance
./build/conformance
zig test src/toolcall.zig
zig test src/jsonschema.zig
zig test src/plugin.zig
zig test src/pii_test.zig
zig test src/openaicompat_test.zig
zig test src/harmovela_test.zig
zig test src/otel_test.zig
zig test src/retriever_test.zig
zig test src/delegation_test.zig
python api-snapshot.py --check
```

This mirror contains the language source and the shared `spec/` vectors, so the implementation can be built and tested here. See [`language/zig/README.md`](language/zig/README.md) for the exact commands. The monorepo CI runs conformance, API snapshot, and native tests for this implementation.

## Community

- X: <https://x.com/axisvela>
- Weibo: <https://weibo.com/u/1936025761>
- LinkedIn: <https://www.linkedin.com/company/axisvela/>
- Facebook: <https://www.facebook.com/profile.php?id=61596905732406>
- YouTube: <https://www.youtube.com/@axisvela>
- Discord: <https://discord.com/channels/1575163993767809064/1575164343148875977>
- GitHub Discussions: <https://github.com/axisvela/praxo-core/discussions>
- GitHub Issues: <https://github.com/axisvela/praxo-core/issues>
- Documentation: <https://axisvela.github.io/praxo-core/>
- Architect: <https://axisvela.architect.pub>

## Repository layout

- `language/zig/` — implementation source, tests, API snapshot, and examples
- `spec/` — shared contract, vectors, and parity inventories
- `LICENSE` — MIT license

## Canonical source

- Canonical source: https://github.com/axisvela/praxo-core/tree/main/language/zig
- Registry introduction: `language/zig/REGISTRY.md`
- Machine-readable entry: `language/zig/llms.txt` and `language/zig/llms.md`
- Mirror repository: https://github.com/axisvela/praxo-core-zig
- Release index: https://axisvela.github.io/praxo-core/languages/registry-status/

This repository is a discovery mirror of the canonical Zig source. The monorepo remains the source of truth and the release workflow source.

PRAXO-CORE is not a hosted model, workflow engine, identity provider, or safety controller. Do not infer exactly-once execution, complete sandbox isolation, production security certification, live-provider behavior, or physical safety from this package.

MIT licensed.
