[![Built with Eidos](https://img.shields.io/badge/built%20with-Eidos-0f9d8c?labelColor=1a1a2e)](https://github.com/Montanalabs/eidos-lang)

> **Eidos** — the injection-safe language. Here prompt injection isn't *detected*, it's
> *unrepresentable*: untrusted input must cross `extract<ClosedType>` before it can reach an
> effect. `check` proves it at compile time; the compiled binary re-clamps at run time.

# Webhook event router

Untrusted input is a webhook payload; it can only ever become one of a fixed set of commands,
never a tool argument. An injected instruction cannot be represented in the closed
type, so it is rejected — proven at compile time by `check`, and clamped again at run
time by the `extract` domain check.

- **Untrusted input:** `fetch<web>` — a webhook payload
- **Closed type:** `type EventType = Push | Issue | Release`, then `type Handling = Handle(EventType) | Drop` (a payload-carrying variant — the payload is closed too)
- **Sink / capability:** `grant route` → `route(handling)`
- **Consequence axes:** Trust

## Run the demo

```sh
examples/apps/webhook-router/demo.sh
```

The safe agent proves `SAFE`, runs on a benign input, and **rejects an injection
payload at the trust boundary (exit 3)**. The vulnerable version proves `UNSAFE` — it
never compiles to a runnable agent.

## Files

- `webhook-router_safe.eide` — the correct design.
- `webhook-router_unsafe.eide` — the tempting-but-wrong version (the negative example a model must learn to reject).
- `eidos.toml` — the project manifest (each app is a self-contained Eidos project).

---

<sub>Part of the <b><a href="https://github.com/Montanalabs/eidos-lang">Eidos</a></b> example corpus — 200 self-contained,
injection-safe projects. Built with Eidos, a language whose type system makes prompt injection
structurally impossible. Run <code>./demo.sh</code> with the Eidos toolchain on your PATH.</sub>
