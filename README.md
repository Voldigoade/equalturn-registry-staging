# Equalturn registry staging

> **NON-PRODUCTION.** This repository exists to test Equalturn's standard-key TUF
> publication and Rust-client verification path. Its root, metadata, target and trust
> bootstrap are disposable interoperability fixtures. Nothing here is an authoritative
> Equalturn release or production trust anchor.

The staging repository is published at
<https://voldigoade.github.io/equalturn-registry-staging/>. Production publication is a
separate repository and remains uninitialized. Do not reuse the staging root or any
staging signer material in a production build.

## Current snapshot

- Source: `Voldigoade/equalturn` commit `f82da19e9225c87dbc2a81e79a0cc3307e787c7b`.
- Deterministic target: `registry-v3.json`, SHA-256
  `e6ccf57eca33951cd6b7a04e7e609f981c87c73298b7923b4d5a9a845caa02a0`.
- TUF repository root: version 1, SHA-256
  `719e372ecc71e8f509f5805889560382d3d599971b82947f9da825101f323144`.
- Metadata was generated with upstream `tuftool` 0.17.0 using ordinary RSA-PSS-SHA256
  TUF keys. Root, targets, snapshot and timestamp each have a separate 3072-bit key and
  a threshold of one. TUF role separation and expiration are exercised here; this
  single-maintainer staging setup is not a production custody model.
- Root expires 19 October 2027; targets and snapshot expire after 90 days; timestamp
  expires after 30 days. Clients must reject expired metadata.

The root fingerprint must be obtained independently from the published repository. It
is not safe to bootstrap trust by downloading `root.json` and its fingerprint from this
same endpoint. Equalturn's production client does not embed or trust this staging root.

## Signing and publication

Private staging keys are never committed. The one-time keys for this interoperability
snapshot are kept outside the repository during the signing operation and are not a
durable staging custody set. Do not treat this snapshot as maintainable after its
metadata expires. A future staging publication requires a new explicit signer and root
custody decision, followed by independent root distribution.

The former TUF-on-CI Sigstore/OIDC signer was removed from this staging repository
because it emitted draft TAP-18 keys that Equalturn's selected Rust TUF verifier does
not support. The old OIDC metadata and signatures remain in public Git history. The
remaining TUF-on-CI Pages workflow is manually dispatched after reviewed metadata is
committed. No scheduled or automatic signing workflow is enabled.

## Boundaries

- Staging metadata is only an interoperability fixture; it is never production trust.
- TUF proves that metadata and the target were authorized by the configured staging
  root. It does not establish that registry indicators are accurate or safe to enforce.
- The registry is research data, not executable policy. Equalturn has no AI enforcement
  connected to this target.
- Do not publish participant/session evidence, local paths, usernames, machine
  identifiers, production credentials, or private signing material here.

See the [Equalturn registry publication status](https://github.com/Voldigoade/equalturn/blob/main/docs/registry-publication-status.md)
and [registry trust design](https://github.com/Voldigoade/equalturn/blob/main/docs/registry-trust.md)
for implementation status and production gates.
