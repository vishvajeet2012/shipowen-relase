# Shipown installer builds

This repository holds the workflows that build every Shipown installer, and no
source code. They read the source from the private repository at the branch,
tag or commit you give them, through a read-only deploy key (`OPS_DEPLOY_KEY`).

| Workflow | Builds | Checked by |
|---|---|---|
| **All installers** | all three below, from one commit | each platform's own checks |
| **Windows installer** | `Shipown-Setup-<version>.exe` (x64) | `latest.yml` SHA-512, silent install, the installed app starts |
| **Linux installer** | `shipown-<version>-amd64.deb` | `latest-linux.yml` SHA-512, `apt install` on Ubuntu 22.04, the installed app starts |
| **macOS installer** | `Shipown-<version>.dmg`, universal | `latest-mac.yml` SHA-512, both architectures, signature, the DMG mounts, starts on Apple Silicon and on a real Intel Mac |

Each build is kept as a workflow artifact for 7 days. Once a build has passed its
checks, it deletes the artifacts of that platform's earlier runs, so only the
newest build is here.

Nothing is published from here, and these workflows have no key to the download
server. Installers are served only from the Shipown download server: in the
source repository, `push-ops/scripts/publish-from-actions.cjs` downloads a run's
artifacts, checks each installer's SHA-512 against its manifest, and uploads it.
Customers are offered a version only after it is published in the admin panel.
