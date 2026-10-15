# ASURA public build orchestration

- This repository is public. Keep game source, source-derived compiler caches,
  raw build logs, binaries, assets and credentials out of every commit and public
  Actions artifact. This applies to failure paths as well as successful builds.
- Only workflow configuration and maintainer documentation belong here. The
  game and build scripts live in the private `jayandradeph/asura` repo.
- Use manual-only builds and one resolved private source commit per run. Never
  add a secret-bearing pull-request, fork or untrusted branch execution path.
- Pin third-party actions to reviewed commit hashes. Use minimum permissions,
  and never persist private checkout credentials or pass them to the compiler.
- Keep `ASURA_SOURCE_TOKEN` in repository Actions secrets, never variables.
- Deliver raw logs and unsigned test packages only to the private source repo;
  verify its private visibility before upload. Do not enable public debug output.
- Default Android output is native libraries and an asset-free emulator APK.
  A full phone APK requires a fresh explicit user request.
- Build success does not prove gameplay parity, device FPS or thermal behavior.
- Keep the README accurate. Commit/push/publish only with user authorization.
