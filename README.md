# ASURA mobile builds

This repository contains only public build orchestration. ASURA game source,
compiler logs, binaries and game data are not published here.

Authorized maintainers can use **Actions -> Build ASURA mobile -> Run workflow**
and select **both**, **ios**, or **android**. Each run resolves the selected
reviewed branch in private `jayandradeph/asura` once, then all jobs build that
exact revision. Use `main` for normal builds; `integration/pc-mobile` is the
reviewed PC/mobile consolidation candidate. This is not a pull-request build path.

- iOS: standard `macos-26` runner; unsigned device IPA, without game data.
- Android: standard `windows-2025` runners; x86_64 and ARM64 native libraries,
  plus an unsigned, asset-free x86_64 emulator APK. No full phone APK.
- Outputs and diagnostic logs: draft releases in the private source repository.
  GitHub authentication and source-repository access are required to download.

## Maintainer setup

Add `ASURA_SOURCE_TOKEN` as a **repository Actions secret**, not a variable.
Use a fine-grained token scoped only to the private source repository with
**Contents: Read and write**. Give it an expiration date and replace it before
it expires. Never put the value in this repository, an issue, or a build input.

Builds are manual-only. There are no pull-request triggers, public build artifacts,
or source-derived caches. The private checkout does not persist credentials.
Compiler output is redirected to files and uploaded only after checking that the
destination remains private. Do not enable verbose public compiler output or
Actions step debugging when handling private source.

Standard public-repository runner usage is covered by GitHub's public Actions
offering; this does not promise zero cost for unrelated services, larger runners,
or future changes to GitHub's terms. No larger runner is configured.

Build success proves compilation and package checks, not gameplay parity,
physical-device FPS, or thermal behavior. Runtime testing remains separate.
