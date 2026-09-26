# blockchain-relayer-service

The VeriTrace gasless relayer and chain indexer:

- collects hashed shipment events and cold-chain incidents from Kafka;
- seals them into Merkle batches, with an IPFS manifest for each batch;
- commits the roots to the `SupplyChainTraceability` contract on Polygon Amoy from the platform wallet,
  so end users never hold keys or pay gas;
- serves inclusion proofs.

> **Status:** planned for milestone M2 (EP5). The design is final; implementation starts with
> `SCM-EP5-US02`.

## Design

| Topic | Reference |
| --- | --- |
| Batching, tree construction, manifest | [ADR-0014](https://github.com/veritrace-platform/veritrace/blob/main/docs/adr/0014-on-chain-commitments.md) |
| Job queue, nonce lock, speed-up, indexer | [ADR-0015](https://github.com/veritrace-platform/veritrace/blob/main/docs/adr/0015-gasless-relayer.md) |
| Contract interface | [smart-contract.md](https://github.com/veritrace-platform/veritrace/blob/main/docs/contracts/smart-contract.md) |
| Database (`veritrace_relayer`) | [data-model.md §5](https://github.com/veritrace-platform/veritrace/blob/main/docs/architecture/data-model.md#5-relayer-database-veritrace_relayer-schema-relayer-m2) |
| Proof API | [rest-api.md §3.4](https://github.com/veritrace-platform/veritrace/blob/main/docs/contracts/rest-api.md#34-blockchain-relayer-service-m2) |

## Service baseline

The service follows the same baseline as the other Go services
([ADR-0004](https://github.com/veritrace-platform/veritrace/blob/main/docs/adr/0004-go-service-baseline.md)).
Its skeleton is taken from `core-business-service`:

- `cmd/`, `internal/platform`, `internal/httpapi`, `migrations/`, `api/openapi.yaml`;
- `Makefile`, `Dockerfile`, CI, and Dependabot;
- API port `:8100`, admin port `:8101`.

## License

[MIT](LICENSE)
