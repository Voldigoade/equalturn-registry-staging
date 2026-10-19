# Equalturn registry staging

> **NON-PRODUCTION STAGING REPOSITORY.** This repository exists only to exercise the
> TUF-on-CI publication and Equalturn client verification path. Its metadata, targets,
> signer configuration, and root trust are disposable test material. Nothing published
> here is an authoritative Equalturn registry release.

This repository was created from the [TUF-on-CI template](https://github.com/theupdateframework/tuf-on-ci-template)
and retains the upstream TUF-on-CI workflows. Publication uses a separate GitHub Pages
site at <https://voldigoade.github.io/equalturn-registry-staging/>. Equalturn's
production repository and trust root are separate and remain uninitialized until the
offline production signer ceremony documented in
[Equalturn](https://github.com/Voldigoade/equalturn).

## Staging boundaries

- Never reuse staging keys, roots, metadata, or target signatures in a production build.
- Do not store or publish production credentials, user/session evidence, or private
  signing material in this repository.
- TUF signatures prove that staging metadata was authorized by the staging root; they
  do not establish that a registry indicator is accurate or safe to enforce.
- Staging publication is for interoperability and release-flow testing only. It does
  not authorize endpoint enforcement.

The workflows remain pinned to reviewed upstream action commits and use job-scoped
permissions. GitHub Actions' repository-level default token permission is read-only;
its narrowly scoped ability to create pull requests is enabled here solely for the
upstream TUF signing-event workflow. The Pages environment only accepts the `publish`
branch, following the upstream TUF-on-CI setup procedure.

## Status

Repository setup is in progress. No production trust material is present. See the
[Equalturn registry publication status](https://github.com/Voldigoade/equalturn/blob/main/docs/registry-publication-status.md)
for the current integration status.
