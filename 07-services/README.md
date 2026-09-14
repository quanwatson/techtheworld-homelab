# Service Lifecycle

Services here don't go straight from "idea" to "running forever." They move through three stages, mostly to force some discipline and partly to mimic how a real environment would actually treat a new service.

**Sandbox.** Free experimentation, low stakes, minimal dependencies. This is where I test new software, poke at an architecture idea, and break things on purpose to see what happens.

**Pre-production.** Once something survives the sandbox, it moves here and starts looking more like the real thing — closer to production topology, tighter security, monitoring and logging turned on, an actual backup strategy. This is where I do performance and security testing and see how it fails.

**Production-like.** The service now gets treated as if it mattered to someone besides me — change discipline, required monitoring and alerting, tested backup/restore, documentation that isn't optional. This is also where I find out if something can actually stay up for a while without me babysitting it.

A service only gets promoted to the next stage once its purpose is clear, its security boundaries are understood, monitoring and backups actually exist (not just planned), and I know how to roll it back if it goes wrong. Skipping that isn't saving time — it's just moving the risk to later, when it's harder to deal with.
