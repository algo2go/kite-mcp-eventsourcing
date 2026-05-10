# kite-mcp-eventsourcing

[![Go Reference](https://pkg.go.dev/badge/github.com/algo2go/kite-mcp-eventsourcing.svg)](https://pkg.go.dev/github.com/algo2go/kite-mcp-eventsourcing)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Event sourcing primitives — domain event aggregate roots (alerts,
orders, positions, sessions), outbox pattern for at-least-once event
delivery, read-side projections, and event store contract.

Used by [`Sundeepg98/kite-mcp-server`](https://github.com/Sundeepg98/kite-mcp-server)
to back the kc/manager state machine + the kc/usecases CQRS write
side.

## Why a separate module?

Event sourcing is a foundational primitive — any algo2go consumer
needing the aggregate-root + outbox + projection pattern can adopt it
without depending on `kite-mcp-server`'s broker integration. Hosting
as its own module:

- Centralizes the EventStore + Aggregate + Projection contracts
- Lets event-payload schemas version independently
- Keeps the outbox runtime decoupled from any one broker

## Stability promise

**v0.x — unstable.** Pin `v0.1.0` deliberately.

## Install

```bash
go get github.com/algo2go/kite-mcp-eventsourcing@v0.1.0
```

## Public API

- `Aggregate` — base interface for event-sourced aggregates
- `AlertAggregate`, `OrderAggregate`, `PositionAggregate`,
  `SessionAggregate` — domain aggregate roots
- `Store` — event store with append + load
- `Projection` — read-side materialized view contract
- `Outbox` — at-least-once event delivery integration

## Dependencies

- `github.com/algo2go/kite-mcp-alerts` v0.1.0
- `github.com/algo2go/kite-mcp-broker` v0.1.0
- `github.com/algo2go/kite-mcp-domain` v0.1.0
- `github.com/google/uuid` — event/aggregate IDs
- `github.com/stretchr/testify` — test assertions

All algo2go deps published; no upstream `replace` directives needed.

## Reference consumer

[`Sundeepg98/kite-mcp-server`](https://github.com/Sundeepg98/kite-mcp-server)
— consumed across kc/eventing_service.go, kc/manager_init.go,
kc/manager_orders_fallback.go, kc/manager_reconstitution.go,
kc/manager_struct.go, kc/usecases/*, app/adapters.go, app/app.go,
app/wire.go, mcp/alert_history_tool_test.go,
mcp/order_history_tool_test.go, mcp/position_history_tool_test.go.

## License

MIT — see [LICENSE](LICENSE).

## Authors

Original design: [Sundeepg98](https://github.com/Sundeepg98) (Zerodha
Tech). Multi-module promotion (2026-05-10): algo2go contributors.
