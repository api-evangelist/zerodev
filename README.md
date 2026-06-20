# ZeroDev (zerodev)

ZeroDev is account-abstraction / smart-wallet infrastructure for EVM chains. It runs an ERC-4337 (and EIP-7702) bundler RPC and a paymaster RPC, both exposed as JSON-RPC over HTTPS, plus the Kernel smart-account SDK and a meta-aggregator (Smart Routing). Apps sponsor gas, let users pay gas in ERC-20s, and submit UserOperations through a single project-scoped RPC endpoint.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/zerodev/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/zerodev/refs/heads/main/apis.yml)

## Tags

- Account Abstraction
- Smart Wallets
- ERC-4337
- EIP-7702
- Paymaster
- Bundler
- JSON-RPC
- Web3

## Timestamps

- **Created:** 2026-06-20
- **Modified:** 2026-06-20

## Transport

ZeroDev's bundler and paymaster are **JSON-RPC 2.0 over HTTPS**, not REST. All calls are an HTTP `POST` of a `{"jsonrpc":"2.0","id":1,"method":"...","params":[...]}` envelope to a single project-scoped URL:

```
https://rpc.zerodev.app/api/v3/{projectId}/chain/{chainId}
```

Authentication is by **project ID embedded in the URL path** (no header key). The same URL serves both bundler and paymaster methods; append `?provider=ULTRA_RELAY` to route through ZeroDev UltraRelay.

## APIs

### ZeroDev Bundler RPC

ERC-4337 bundler exposed as JSON-RPC over HTTPS. A single POST to the project-scoped RPC URL carries methods eth_sendUserOperation, eth_estimateUserOperationGas, eth_getUserOperationByHash, eth_getUserOperationReceipt, eth_supportedEntryPoints, and eth_chainId for EntryPoint v0.6 and v0.7. Authentication is by project ID embedded in the URL path; append ?provider=ULTRA_RELAY to route through ZeroDev UltraRelay.

- **Human URL:** [https://docs.zerodev.app/meta-infra/rpcs](https://docs.zerodev.app/meta-infra/rpcs)
- **Base URL:** `https://rpc.zerodev.app/api/v3/{projectId}/chain/{chainId}`

#### Tags

- Bundler
- ERC-4337
- UserOperation
- JSON-RPC

#### Properties

- [Documentation](https://docs.zerodev.app/meta-infra/rpcs)
- [API Reference](https://docs.zerodev.app/meta-infra/rpcs)
- [OpenAPI](openapi/zerodev-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/zerodev.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/zerodev.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### ZeroDev Paymaster RPC

Verifying and ERC-20 paymaster exposed as JSON-RPC over the same project-scoped RPC URL. Methods include zd_sponsorUserOperation (ZeroDev sponsorship), pm_sponsorUserOperation (Pimlico-compatible sponsorship), the ERC-7677 pair pm_getPaymasterStubData / pm_getPaymasterData, and zd_getERC20PaymasterAddress for paying gas with ERC-20 tokens. Returns the signed paymaster fields the bundler needs.

- **Human URL:** [https://docs.zerodev.app/sdk/core-api/sponsor-gas](https://docs.zerodev.app/sdk/core-api/sponsor-gas)
- **Base URL:** `https://rpc.zerodev.app/api/v3/{projectId}/chain/{chainId}`

#### Tags

- Paymaster
- Gas Sponsorship
- ERC-7677
- JSON-RPC

#### Properties

- [Documentation](https://docs.zerodev.app/sdk/core-api/sponsor-gas)
- [API Reference](https://docs.zerodev.app/meta-infra/rpcs)
- [OpenAPI](openapi/zerodev-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/zerodev.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/zerodev.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### ZeroDev Kernel SDK

Kernel is ZeroDev's modular ERC-4337 and EIP-7702 smart-account implementation. The TypeScript Kernel SDK (built on viem / permissionless) builds and signs UserOperations, then drives the bundler and paymaster RPCs. Kernel v3 supports EIP-7702 delegation alongside classic 4337 deployment.

- **Human URL:** [https://docs.zerodev.app/sdk/getting-started/quickstart](https://docs.zerodev.app/sdk/getting-started/quickstart)
- **Base URL:** `https://rpc.zerodev.app/api/v3/{projectId}/chain/{chainId}`

#### Tags

- Kernel
- SDK
- Smart Account
- EIP-7702

#### Properties

- [Documentation](https://docs.zerodev.app/sdk/getting-started/quickstart)
- [Source Code](https://github.com/zerodevapp/sdk)
- [OpenAPI](openapi/zerodev-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/zerodev.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/zerodev.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### ZeroDev Meta-Aggregator (Smart Routing)

ZeroDev's meta-infrastructure aggregates underlying bundler and paymaster providers behind one project-scoped RPC, with Smart Routing that lets users deposit and have assets routed across chains. Provider selection is controlled with the ?provider query parameter (e.g. ULTRA_RELAY).

- **Human URL:** [https://docs.zerodev.app/sdk/infra/intro](https://docs.zerodev.app/sdk/infra/intro)
- **Base URL:** `https://rpc.zerodev.app/api/v3/{projectId}/chain/{chainId}`

#### Tags

- Meta-Aggregator
- Smart Routing
- Cross-Chain
- Intents

#### Properties

- [Documentation](https://docs.zerodev.app/sdk/infra/intro)
- [OpenAPI](openapi/zerodev-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/zerodev.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/zerodev.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [GitHub Organization](https://github.com/zerodevapp)
- [LinkedIn](https://www.linkedin.com/company/zerodev)
- [Website](https://zerodev.app)
- [Documentation](https://docs.zerodev.app)
- [Plans](plans/zerodev-plans-pricing.yml)
- [Rate Limits](rate-limits/zerodev-rate-limits.yml)
- [Fin Ops](finops/zerodev-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
