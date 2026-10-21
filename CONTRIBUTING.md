# Developing Media Intake

This repository owns the reusable acquisition implementation. It was extracted
from `Code4me2/latent-timing-duplex`, preserving the package's Git history. The
import name is `media_intake`, the CLI is `media-intake`, and the distribution
name remains `media-intake-local`. No package-index publication is implied.

## Scope

Keep metadata inspection, media/caption acquisition, format policies, verification,
provenance and safe local storage here. Keep dataset eligibility, permission
workflows, sampling, labeling interfaces and model experiments in applications.
Do not add a dependency on the research repository, NumPy or PyYAML merely to
support one consumer.

## Local checks

```bash
uv sync --locked --extra dev
uv run --locked python -m pytest
uv build
git diff --check
```

Use the `tooling` extra if you want a locked Python installation of yt-dlp.
FFmpeg/ffprobe and JavaScript runtimes are separate external dependencies;
recording their versions is not equivalent to pinning them. Keep the committed
`uv.lock` updated when Python dependencies change.

Prefer injected adapters/runners in tests. Do not turn offline CI into an
unapproved download job. No raw media, full metadata with signed URLs, captions,
credentials or acquisition receipts belong in this repository.

## Compatibility and consumers

- Keep stage independence: metadata/captions must not require downloading MP4s.
- Preserve original-language defaults and explicit caption origin/status.
- Treat artifact schemas, receipt verification and command behavior as public
  contracts. Describe and test migrations rather than silently accepting new
  schemas over existing evidence.
- Add regressions for new policies, subprocess behavior and storage changes.
- The research consumer retains its legacy policy wrappers and a pinned vendored
  package. Public downstream builds must not require access to this private repo.
- Update downstream vendored snapshots deliberately, recording the exact upstream
  commit and Git tree. Run both standalone and host integration tests before
  updating the downstream branch. Do not make parallel fixes only in the vendor
  copy and leave this canonical repository behind.

The extraction initially leaves the research snapshot on the original split
commit; standalone repository setup does not change acquisition code behavior.
