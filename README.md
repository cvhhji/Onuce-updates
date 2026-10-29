# Onuce private distribution

This repository contains APK releases, verified device adapters, and their distribution workflows. It does not contain the Onuce or KowSU application source.

The lightweight timer runs every eight hours on this repository's default branch. The builder reads only `cvhhji/Onuce` branch `codex/onuce-manager-build-20261029`, checks supported official upstream managers, verifies public manager APK signatures and source identities, compiles exact device modules when needed, and publishes only verified artifacts. Private KowSU adaptation follows production `manager-build-<version>` source tags, verifies master ancestry, the real source version and UAPI, and uses the pinned manager certificate. Clients independently inspect their installed APK before selecting a matching module.

Server publication uses this repository's ephemeral `GITHUB_TOKEN`. A dedicated `ONUCE_SOURCE_DEPLOY_KEY` Actions secret permits the builder to read the source repository and write validated public-manager payload changes back to the independent branch. A separate read-only `ONUCE_KOWSU_DEPLOY_KEY` reads only KowSU source; it cannot access release API assets or change that repository. Private source updates publish device modules without fabricating new APK or daemon evidence in the pinned application payload. These keys are not distributed to clients. The kernel container receives neither credentials nor the application source repository.

Clients should create a fine-grained token selecting only this distribution repository with Contents read-only permission. Do not grant clients access to any source repository. Client credentials are not embedded in APKs.

The `device-adapters-v1` release body points to an immutable, digest-verified adapter catalog with only the newest version of each manager. Catalog pointers change only after all referenced files are verified. Retained historical files are not selectable fallbacks. A successful build does not replace device runtime validation.
