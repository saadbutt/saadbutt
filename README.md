# Saad Rasool Butt

AI agent and backend engineer. Eight years of backend work, plus a Master's in AI.

I build three kinds of systems. Permission layers that stop an agent's bad call
from becoming a bad outcome, instead of trusting the model to only ask for
things it should. Evaluation harnesses that prove a RAG or extraction pipeline
actually retrieves the right thing, instead of eyeballing output and nodding.
Generation pipelines that can't drift from a measured fact, instead of
shipping whatever the model's draft said. The business problem underneath all
three is the same: AI features demo well in a sales call and then fail
expensively once real traffic, real documents, and real users hit them. Each
repo below is one of those three, built for a real case rather than as a toy.

Most of what I've built is private: client systems under NDA, internal platforms,
production backends that will never have a public URL. The repositories below
are the ones I can show. Each is a working system with tests and CI, built
around the parts that are genuinely hard rather than the parts that demo well.

## AI agent infrastructure

### [toolgate](https://github.com/saadbutt/toolgate)

The permission layer for the "unvalidated input" and "no record" failures. A
gate between an AI agent and the systems it can change: deny-by-default policy,
scoped capability grants that expire, confirmation on anything consequential,
spend ceilings, and a hash-chained audit log you can verify. The demo is seven
scenarios, each one an attack and the guardrail that stops it — including the
one most "confirm before executing" implementations get wrong: if you re-ask
the model for arguments after approval, you approved a description and executed
something else.

Go, standard library only. A TypeScript port of the confirmation core hashes
byte-for-byte identically.

### [ragcheck](https://github.com/saadbutt/ragcheck)

The answer to "nobody counted the tokens," applied to RAG specifically. Measures
retrieval before you try to fix it: hit rate, MRR, precision and context cost
per chunking strategy, against one goldset. Prints the rank each question's
first correct chunk landed at and lists what the misses retrieved instead — an
average tells you something is wrong, the miss list tells you what.

### [brandkit](https://github.com/saadbutt/brandkit)

The answer to "output straight into a database." Measures a brand's existing
page, asks a model to assign roles and write copy, then forces that answer
through a closed schema where it loses every argument it has with a measured
fact. `verify` runs two different models over one source and exits non-zero if
the kits differ.

### [whatsapp-message-extractor](https://github.com/saadbutt/whatsapp-message-extractor)

A production LLM extraction pipeline with an eval harness attached, not a demo.
WhatsApp group messages to validated structured JSON across English, Gulf
Arabic and Arabizi. Closed schema, mock LLM and form API so it runs with no
key, 15/15 exact field match on the goldset.

## Backend systems

### [device-gateway](https://github.com/saadbutt/device-gateway)

TCP ingest gateway for GPS and telemetry devices. Sliding-window replay
deduplication, mid-stream frame resync, half-open socket detection, and an
explicit backpressure policy instead of an unbounded queue. Go, zero
dependencies. Real-time, high-volume device data is my day job, not something
I read about — I work full time on a telematics platform ingesting this kind
of traffic.

### [fleet-tracking-backend](https://github.com/saadbutt/fleet-tracking-backend)

Fleet tracking REST API. JWT auth, PostgreSQL with migrations, Redis caching,
Swagger docs, Docker Compose.

### [txParser](https://github.com/saadbutt/txParser)

Ethereum transaction parser with address subscriptions and block querying.

---

`toolgate` and `device-gateway` run gofmt, vet, the full test suite and the race
detector in CI, and cross-compile for arm64 — the target they'd actually ship
to. `ragcheck` and `brandkit` run on Python 3.9 through 3.13, and their CI
asserts the behaviour rather than just the tests: ragcheck gates the build on
retrieval quality, brandkit builds twice with two different models and fails if
the tokens differ.

**Where clients bring me in:** LLM features that have to work in production
(OpenAI and Claude APIs, tool calling, RAG, streaming, retries and fallback,
cost control), backend APIs in Python, Node, and Go, and the unglamorous parts
most job posts leave out — idempotency, retries, duplicate messages,
reconciliation, offline sync.

**Available for contract work:** [Upwork](https://www.upwork.com/freelancers/~018ff43e3df3f94993)
