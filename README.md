# Shipown macOS build

This repository holds one workflow and no source code. **Actions → macOS
installer → Run workflow** builds the Shipown macOS installer from the private
source repository at the branch, tag or commit you give it, reading it through
a read-only deploy key (`OPS_DEPLOY_KEY`).

The result is one universal DMG (Apple Silicon and Intel, macOS 11 and later),
checked on both kinds of Mac and kept as a workflow artifact for 7 days. Nothing
is published from here: installers are served only from the Shipown download
server, after their SHA-512 is checked against `latest-mac.yml`.
