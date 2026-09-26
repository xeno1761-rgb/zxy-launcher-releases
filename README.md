# Zxy Launcher — releases

Release artifacts and the update feed for **Zxy Launcher**.

The source lives in a private repository; this one holds only what a shipped copy
of the launcher needs in order to install itself and to keep itself up to date:

- `Zxy Launcher_<version>_x64-setup.exe` — the Windows installer.
- `Zxy Launcher_<version>_x64_en-US.msi` — the MSI installer.
- `zxy-launcher.exe` — the portable executable.
- `latest.json` — the update feed. An installed copy fetches
  `releases/latest/download/latest.json` and verifies the signature against the
  public key compiled into the app. An update signed by any other key is rejected,
  so this file is only trustworthy because the private key that produced it never
  leaves the build workflow.
- `addons/` — the built-in addon catalog and its archives, which the launcher's
  addon hub fetches over `raw.githubusercontent.com`. These are read directly from
  this branch rather than from a release, so that installing an addon does not
  depend on a release having been published.

This repository is public on purpose. A private repository answers an
unauthenticated request for release assets with `404`, and an installed launcher
has no token to send, so the artifacts have to live somewhere readable without
credentials.

Download the newest build from the [releases page](../../releases/latest).

## Publishing

Releases are built and published by the `Release` workflow in the private source
repository, triggered by pushing a `v*` tag. Do not upload artifacts here by hand;
a manual upload would produce a `latest.json` whose signature no installed copy
can verify against a build it was not published with.
