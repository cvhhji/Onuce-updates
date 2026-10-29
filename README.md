# Onuce private distribution

This repository contains APK releases, verified device adapters, and their distribution workflows. It does not contain the Onuce or KowSU application source.

The lightweight timer runs every eight hours on this repository's default branch. The builder reads only `cvhhji/Onuce` branch `codex/onuce-manager-build-20261029`, checks supported official upstream managers, verifies APK signatures and source identities, compiles exact device modules when needed, and publishes only verified artifacts. KowSU automatic adaptation is disabled until explicitly updated.

Server publication uses this repository's ephemeral `GITHUB_TOKEN`. A dedicated `ONUCE_SOURCE_DEPLOY_KEY` Actions secret permits the builder to read the source repository and write validated payload changes back to the independent branch. This key is not distributed to clients. The kernel container receives neither credentials nor the application source repository.

Clients should create a fine-grained token selecting only this distribution repository with Contents read-only permission. Do not grant clients access to any source repository. Client credentials are not embedded in APKs.

The `device-adapters-v1` release body points to an immutable, digest-verified adapter catalog. Catalog pointers change only after all referenced files are verified; old adapter files remain available. A successful build does not replace device runtime validation.
