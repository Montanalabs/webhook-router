#! VULNERABLE webhook-router — feeds the untrusted input straight to the tool with no extraction.
#! check -> UNSAFE: tainted data cannot reach a capability.
grant route

let payload = fetch<web>
privileged { route(payload) }  # tainted -> tool: REJECTED
