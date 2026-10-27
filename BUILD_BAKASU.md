# A52s BakaSU builds

Open **Actions → Build A52s BakaSU → Run workflow** on `main`.

- Leave `bakasu_sha` empty to select the latest successful **Build Manager** run on `Baka-SU/BakaSU`'s `main` branch that has a non-expired `Manager-release` artifact.
- Choose `oneui`, `aosp`, or `both`.
- Download `A52s-BakaSU-oneui` or `A52s-BakaSU-aosp` from the completed run. Extract the artifact archive to obtain the flashable kernel ZIP.
- Download the matching **Manager-release** artifact from the BakaSU run linked in the build summary. Use its arm64-v8a APK for the A52s.
- `build-logs-*` contains the log, final `.config`, exact kernel/BakaSU commit IDs and BakaSU version code.

The kernel sources are in `bakasu-oneui` and `bakasu-aosp`, based on upstream's corresponding ReSukiSU branches. `main` retains the original rootless kernel sources and hosts the build workflow. Builds use manual hooks, without SUSFS.

For reproducibility, enter a full BakaSU commit SHA. The initial matching Manager build is https://github.com/Baka-SU/BakaSU/actions/runs/40109566037 (`d5e9e025b8b49155f8014684d64c91742b465f65`). The submodule is pinned to that commit for local builds; Actions records any selected override. Local builds use `bash build_kernel_zip.sh` on the appropriate `bakasu-*` branch.

The scripts reuse the repository's existing ROM-specific base boot images and installer. A successful CI build validates compilation and packaging; device boot and root operation still require testing on an A52s with the corresponding ROM.
