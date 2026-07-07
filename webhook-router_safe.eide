#! Webhook event router — untrusted a webhook payload can only become one of a fixed set of commands, never a
#! tool argument. An injected instruction cannot be represented in the closed type, so
#! it is rejected at the trust boundary (and re-clamped at run time by extract). The
#! command carries a payload from its own closed set, so even that cannot be smuggled.
#! @requires route — the event router
#! @effect net — carries out the chosen command
#! @taint bridge — extract<Handling> turns the tainted input into a trusted command
grant route

type EventType = Push | Issue | Release
type Handling = Handle(EventType) | Drop

let payload = fetch<web>  # UNTRUSTED a webhook payload — tainted
quarantined { let handling = extract<Handling>(payload) }  # only a fixed Handling (payload too) crosses
privileged { route(handling) }  # act on the trusted command only
