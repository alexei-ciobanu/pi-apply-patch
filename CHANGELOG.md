# Changelog

## [Unreleased]

### Added

- Initial standalone `apply_patch` pi extension.

### Fixed

- Resolve absolute, parent-relative, and symlinked patch paths with normal Node path semantics.
- Show settled diff hunks in the Pi TUI by default after successful and partially failed patches.
- Report underlying per-file failure reasons and applied files instead of generic reread instructions.
- Serialize concurrent patch mutations through Pi's per-file mutation queue.
