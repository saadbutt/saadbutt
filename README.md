# Saad Rasool Butt

Backend engineer, eight years, mostly Go. I work on telematics — GPS ingest,
device protocols, and fleet data at volume.

Most of what I've built is private: client systems under NDA, internal
platforms, production backends that will never have a public URL. The
repositories below are the ones I can show. Each is a working system, built
around the parts that are genuinely hard rather than the parts that demo well.

### [device-gateway](https://github.com/saadbutt/device-gateway)

TCP ingest gateway for GPS and telemetry devices. Sliding-window replay
deduplication, mid-stream frame resync, half-open socket detection, and an
explicit backpressure policy instead of an unbounded queue. Go, zero
dependencies.

### [toolgate](https://github.com/saadbutt/toolgate)

A gate between an AI agent and the systems it can change. Deny-by-default
policy, scoped and expiring capability grants, frozen-argument confirmation,
budget ceilings, and a hash-chained audit log. Go, zero dependencies, with a
TypeScript port of the confirmation core that hashes byte-for-byte identically.

### [fleet-tracking-backend](https://github.com/saadbutt/fleet-tracking-backend)

Fleet tracking REST API. JWT auth, PostgreSQL with migrations, Redis caching,
Swagger docs, Docker Compose.

### [txParser](https://github.com/saadbutt/txParser)

Ethereum transaction parser with address subscriptions and block querying.

`device-gateway` and `toolgate` both run gofmt, vet, the full test suite and
the race detector in CI, and cross-compile for arm64 — the target they'd
actually ship to.

**Currently working on:** agent infrastructure, device and wire protocols,
Go backends.

**Available for contract work** — [Upwork](https://www.upwork.com/freelancers/~018ff43e3df3f94993)
