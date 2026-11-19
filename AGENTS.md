# AGENTS.md

## Working in this repo

- Treat the codebase as the source of truth. Verify comments, docs, and claims from prior conversations or external sources against the implementation before relying on them. Start with the source tree for the build you are changing.

## Where changes go

- `extension/` is the tested Apple Silicon release source. `experimental/extension/` is a separate build for Apple Silicon and  untested Windows with NVIDIA CUDA. The default atm is the 0.3.x build, the "cross platform" is the 0.4.x build. The goal is to make the 0.4.x build the normal one, but until someone tests it 0.3.x will remain the default.

- Put release-facing usage and installation docs in `README.md` and `Setup.md`. Use `experimental/README.md` and `experimental/Setup.md` for the experimental build. Put documentation images in `images/`.
- Use the workspace's sibling `../test-footage/` for local clips and blend files, and `../.setup/` for temporary Blender probes and logs. Keep generated frames, analysis caches, model weights, and installed runtimes outside the repository. Saved blend files can reference analysis caches, so check before deleting caches or changing their layout.
- Keep old versions of the extension in the workspace's sibling `../oldVersions/` for easy future reference.
- The sibling `../corridorkey-v2-mlx/` is a local upstream reference. The add-on's MLX installer fetches a pinned backend revision. Check `setup_runtime.py` and `mlx_backend.py` before assuming that edits to the sibling copy affect the installed add-on.

## Build and check

- Use Blender 5.3 or later. From the repository root, validate the affected package with `blender --factory-startup --command extension validate extension`. Use `experimental/extension` for the experimental build. On macOS, use `/Applications/Blender.app/Contents/MacOS/Blender` if `blender` is unavailable on your PATH.
- For an install test on macOS, run `blender --factory-startup --command extension build --source-dir extension --output-dir /tmp`. Use `experimental/extension` for the experimental build. Both builds share an extension ID, so installing one replaces the other in the same Blender profile. Use a separate test profile when you need both installations.
- For node changes, analyze a short clip in the scene compositor. Also check a Sequencer strip compositor on MLX when the change affects that path. Check the affected outputs, frame alignment, and playback after reopening the blend file when changing sequence paths or cache handling. For job lifecycle changes, check cancel and rerun. For setup failures, inspect the setup log. For analysis failures, inspect `analysis.log` in the job folder.
- Report which build, platform, and behavior you tested. A macOS test exercises the MLX path. CUDA runtime and inference checks require Windows with a supported NVIDIA GPU.
- Build test ZIPs outside the repo. Update tracked ZIPs when the task calls for packaging a release. `UNZIPME.zip` bundles the Mac install ZIP with `README.md` and `Setup.md`. The experimental ZIP is installed directly.
