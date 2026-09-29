# Magnus Desktop

Releases of **Magnus Desktop**, the Windows app that gives [Magnus AI](https://www.powercademy.com) hands on your machine: builds from the Magnus chat run on your computer with your own Claude Code and Power Platform CLI sign-ins, with no terminal to keep open.

This repository holds binaries only. The source lives in `desktop/` of the private `powercademy-3.0` repository. It is public so the app can check for updates here without a token.

## Install

Download `Magnus-Desktop-Setup-<version>.exe` from the [latest release](https://github.com/HowdangPowercademy/magnus-desktop/releases/latest) and run it. It installs for your user only (no admin rights) and updates itself. Then, in Magnus, open Settings → Runners → Pair a runner and press **Open Magnus Desktop**.

Until the code-signing certificate lands, releases are unsigned betas: Windows warns on install. They are for named testers only.

## Releasing (for Powercademy)

1. On `powercademy-3.0`, bump `desktop/package.json`'s version and merge to `dev`.
2. Either push a tag here, `vX.Y.Z` (the same number), or run the **Release Magnus Desktop** workflow by hand and pick the ref.
3. The workflow checks out the source with a read-only deploy key, runs the app's smoke test, builds the NSIS installer, and publishes the release with `latest.yml`, which is what the app's updater reads.

Signing switches on when two repository variables exist: `AZURE_SIGNING_PROFILE` (the Azure Trusted Signing certificate profile) and `AZURE_SIGNING_PUBLISHER` (the certificate subject). The signer's credentials are already in the repository's secrets.
