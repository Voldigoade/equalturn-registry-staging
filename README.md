# Equalturn registry staging

> **NON-PRODUCTION.** This repository exists to test Equalturn's standard-key TUF publication and Rust-client verification path. Its root, metadata, target, and bootstrap are disposable interoperability fixtures. Nothing here is an authoritative Equalturn release or production trust anchor.

The staging repository is published at <https://voldigoade.github.io/equalturn-registry-staging/>. Production publication is a separate repository and remains uninitialized. Do not reuse the staging root or staging signer material in a production build.

## Current snapshot

- Source: `Voldigoade/equalturn` commit `f82da19e9225c87dbc2a81e79a0cc3307e787c7b`.
- Deterministic target: `registry-v3.json`, SHA-256 `e6ccf57eca33951cd6b7a04e7e609f981c87c73298b7923b4d5a9a845caa02a0`.
- TUF repository root: version 1, SHA-256 `719e372ecc71e8f509f5805889560382d3d599971b82947f9da825101f323144`.
- Metadata was generated with upstream `tuftool` 0.17.0 using ordinary RSA-PSS-SHA256 TUF keys. Root, targets, snapshot, and timestamp each have a separate 3072-bit key and threshold one. This single-maintainer staging setup is not a production custody model.
- Root expires 19 October 2027; targets and snapshot expire after 90 days; timestamp expires after 30 days. Clients must reject expired metadata.

The root fingerprint must be obtained independently from the published repository. It is not safe to bootstrap trust by downloading `root.json` and its fingerprint from this same endpoint. Equalturn's production client does not embed or trust this staging root.

## Signing and publication

Private staging keys are not committed and are not a durable staging custody set. The current signed snapshot is for interoperability testing; it must not be treated as maintainable after its metadata expires. Any future staging refresh requires a new explicit signer and custody decision, an independently distributed root if the root changes, and successful verification with Equalturn's Rust client.

The former staging root used Sigstore/OIDC TAP-18 keys that `sigstore-tuf` 0.15.0 cannot parse. The user explicitly approved replacing only these non-production signatures with standard TUF keys; the old root and signatures remain public history. The later TUF-on-CI v0.21.0 publication attempt failed because its metadata builder expected the `x-tuf-on-ci-expiry-period` extension absent from the standard-key metadata (run [39331918162](https://github.com/Voldigoade/equalturn-registry-staging/actions/runs/39331918162)). TUF-on-CI's signing and publication workflow is not used for this snapshot.

GitHub Pages is deployed by `.github/workflows/publish.yml`. The build job checks out the fixed `static-tuf-publish` branch and packages its signed files; the deployment job only publishes the artifact. The workflow has no signing key or metadata mutation authority. After deployment, a TUF-on-CI Python-client smoke check tests the public metadata/target chain without comparing to the old `publish` branch. Equalturn's separate live smoke uses the pinned standard-key root and is the authoritative client interoperability check. Staging metadata changes must be created and independently verified before they are pushed to the publication branch.

## Boundaries

- Staging metadata is only an interoperability fixture; it is never production trust.
- TUF proves metadata and target bytes were authorized by the configured staging root. It does not establish that registry indicators are accurate or safe to enforce.
- The registry is research data, not executable policy. Equalturn has no AI enforcement connected to this target.
- Do not publish participant/session evidence, local paths, usernames, machine identifiers, production credentials, or private signing material here.

See the [Equalturn registry publication status](https://github.com/Voldigoade/equalturn/blob/main/docs/registry-publication-status.md) and [registry trust design](https://github.com/Voldigoade/equalturn/blob/main/docs/registry-trust.md) for implementation status and production gates.
