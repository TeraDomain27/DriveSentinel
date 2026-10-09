# Contributing to DriveSentinel

Thanks for considering a contribution. DriveSentinel is a Windows disk-health tool, so most changes touch low-level I/O, SMART parsing, UI rendering, or the failure-prediction model. The guidelines below exist to keep those parts stable and reviewable.

## Ground rules

- Open an issue before working on anything larger than a bug fix. Alignment on scope saves rework.
- One concern per pull request. A PR that mixes a bug fix with a refactor is harder to review and harder to roll back.
- Keep changes narrow. If you touch the SMART parser, do not also reflow the UI.
- English only in code, comments, commit messages, and discussion. Translations of the UI are handled through the localization files.

## What is in scope

- New SMART attribute decoders for vendor-specific IDs (please cite the datasheet).
- Prediction-model improvements backed by data, not intuition. Attach a reproducible notebook or dataset reference.
- UI fixes, accessibility improvements, high-DPI handling.
- Driver and controller compatibility fixes (NVMe passthrough, RAID, USB bridges that honor ATA passthrough).
- Documentation, examples, translations.

## What is out of scope

- Features that write to the drive. DriveSentinel is read-only by design.
- Overclocking, firmware flashing, or secure-erase workflows.
- Cloud sync of SMART data. Health data stays local.
- Bundled telemetry. We do not add it and we will not merge it.

## Development setup

1. Clone the repository.
2. Install the toolchain listed in `BUILD.md`.
3. Run the test suite before you touch anything so you know what green looks like on your machine.
4. Enable the pre-commit hooks. They run formatting, static analysis, and the unit tests that do not need a real drive.

Integration tests that require a physical drive are gated behind an environment variable. Do not add tests that mutate drive state.

## Pull request checklist

- [ ] The branch is rebased on `main` and the history is clean.
- [ ] `make check` (or the platform equivalent) passes locally.
- [ ] New code has unit tests. SMART parsing changes include a sample binary blob as a fixture.
- [ ] UI changes include a before/after screenshot at 100% and 200% scaling.
- [ ] The changelog entry is written in the past tense, from the user's perspective, not the implementer's.
- [ ] You have signed off commits with `git commit -s` if you want DCO credit.

## Reporting bugs

Open an issue with:

- Windows build and architecture.
- Drive model, firmware revision, and interface (SATA / NVMe / USB bridge chipset).
- A SMART dump exported from the app (**Help → Export diagnostic bundle**). The bundle is a plain text file with no personal identifiers.
- Steps that reproduce the problem, and what you expected instead.

If the issue only reproduces on one specific drive, that is useful information, not a reason to close.

## Security

Security issues go to the private advisory tracker on GitHub, not to the public issue list. See `SECURITY.md` for the full policy once it lands.

## Code of conduct

Participation in this project is governed by the [Code of Conduct](code_of_conduct.md). By contributing you agree to uphold it.
