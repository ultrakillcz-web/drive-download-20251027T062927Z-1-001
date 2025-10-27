# Copilot Instructions - Android APK Versions Repository

## Purpose
This repository stores Android APK artifacts that belong to a broader, multi-platform product. Treat the files here as versioned outputs generated elsewhere. The goal is to document provenance, testing coverage, and security posture for every delivered build.

## Repository Shape
- Root directory: Git metadata plus APK binaries following the naming scheme: `Documento de 👉👉Léo👈👈.apk`, `Documento de 👉👉Léo👈👈(1).apk`, etc.
- Current files use Unicode characters and emojis. Consider normalizing future additions to ASCII (e.g., `Documento_de_Leo_v01.apk`) for better automation compatibility.
- Preserve historical builds unless product owners approve pruning. If repository size becomes a problem, migrate older artifacts to Git LFS or an external artifact store but keep references here.

## Tooling and Analysis Commands
- Inventory (PowerShell): `Get-ChildItem *.apk | Select-Object Name, Length | Sort-Object Name`
- Inventory (bash or zsh): `ls -lh *.apk`
- Manifest metadata (Android SDK build-tools): `aapt dump badging "Documento de 👉👉Léo👈👈(6).apk"`
- Deep inspection: `apktool d "Documento de 👉👉Léo👈👈(6).apk" -o out/v06` or `jadx -d out/v06 "Documento de 👉👉Léo👈👈(6).apk"`
- Signature verification: `apksigner verify --print-certs "Documento de 👉👉Léo👈👈(6).apk"`
- Binary diff (after decode): `diff -ruN out/v07 out/v08`
- Always extract and inspect builds in a disposable work folder to avoid polluting the artifact archive.

## Workflow for New Versions
1. Place the APK in the repository using the established naming convention (`Documento de 👉👉Léo👈👈(7).apk` with incremental numbers in parentheses).
2. Capture provenance in the commit message: upstream tag, CI job, git hash, or ticket reference.
3. Run `aapt dump badging` to confirm `package`, `versionCode`, `versionName`, and target SDK. Paste the key lines in the commit notes or maintain them in an updated manifest file.
4. Execute cross-platform testing: install on at least one Android 12+ device or emulator, and if the wider project supports other platforms (for example macOS via Android Studio), record results or known blockers.
5. Update shared documentation (CHANGELOG, release manifest, or sibling repos) so the larger project sees the new build and its readiness status.

## Cross-Platform and Integration Notes
- APK artifacts are consumed by mobile CI pipelines, distribution portals, and possibly hybrid frameworks tied to desktop or web components. Coordinate releases with the teams that maintain those surfaces.
- Keep feature toggles, backend API versions, and config files aligned across repositories. If an APK depends on new backend endpoints, flag that dependency in the commit description.
- When automating tasks, provide PowerShell and bash variants where possible to support Windows, macOS, and Linux contributors.

## Security and Compliance Guidance
- Scan every new APK with trusted antivirus and (when available) mobile security scanners such as Mobile Security Framework (MobSF) before committing.
- Verify signatures using `apksigner` and record certificate fingerprints in commit notes. Reject unsigned or mismatched builds.
- Do not store keystore files or signing keys in this repository. Document the secure storage location only.
- Respect third-party license terms when decompiling or reverse-engineering bundled libraries. If analysis is required, log the reasoning in the issue tracker rather than inside the artifact repo.

## Operational Tips
- Consider introducing a `manifest.json` or `VERSIONS.md` file that summarizes each build (version number, date, commit hash, QA status). This ensures downstream automation and human reviewers have consistent context.
- Tag releases (`apk/v08`, `apk/v09`) so automated systems can pull a stable reference without parsing commit history.
- When removing or replacing an artifact, open a ticket explaining the rationale and obtain sign-off from product/security owners to maintain traceability.
- For troubleshooting, capture findings and scripts in separate documentation or issue comments. Keep the repository focused on clean artifact storage plus minimal metadata.
