# Changelog

## [Unreleased]

### Added

- Initial standalone `apply_patch` pi extension.

### Changed

- Refresh the development lockfile to Pi 0.80.10 and current compatible tooling with a clean security audit.
- Point installation and repository metadata at the maintained fork.
- Update GitHub Actions to checkout and setup-node v7.
- Limit published tarballs to runtime source and user-facing documentation.

### Fixed

- Resolve absolute, parent-relative, and symlinked patch paths with normal Node path semantics.
- Show settled diff hunks in the Pi TUI by default after successful and partially failed patches.
- Render complete and partial patch failures with error styling in the Pi TUI.
- Mark complete and partial failures as Pi error results so the entire tool shell is red.
- Use consistent diff colors for standalone added and removed lines.
- Render failure details in normal text on Pi's error-colored shell.
- Show delete operations without reading or rendering the deleted file contents.
- Match official apply_patch execution by rejecting empty move hunks and stopping at the first failed action.
- Preview repeated-path actions sequentially while preserving declared add, delete, update, and move labels.
- Summarize homogeneous patches by operation and mixed patches as file actions.
- Report successfully applied actions, rather than ambiguous file lists, after partial failures.
- Report underlying per-file failure reasons and applied files instead of generic reread instructions.
- Serialize concurrent patch mutations through Pi's per-file mutation queue.
