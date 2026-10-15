# ASURA builds

This repository contains only public build orchestration. ASURA game source,
compiler logs, binaries and game data are not published here.

Authorized maintainers can use **Actions -> Build ASURA -> Run workflow**
and select **all**, **windows**, **mobile**, **ios**, or **android**.
`all` builds Windows, Android and iOS; `mobile` builds Android and iOS. Each run resolves the selected
reviewed branch in private `jayandradeph/asura` once, then all jobs build that
exact revision. Only the reviewed `main` branch is accepted. This is not a pull-request build path.

- Windows: standard `windows-2022` runner; all 25 Release/Win32 executables
  (client, emulator, four servers and 19 editors/tools), with checksums. This is
  compiled output, not a complete game installer or server deployment package.
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

## Windows validation

[Windows run 38695167901](https://github.com/jayandradeph/asura-builds/actions/runs/38695167901)
passed the full Release/Win32 solution build. The downloaded private bundle
passed the expected 25-executable inventory, architecture and checksum checks.
This is build/package verification; no installation or gameplay claim is made.
