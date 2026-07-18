# Changelog

## [Unreleased]

### Added

- Initial standalone `apply_patch` pi extension.

### Fixed

- Resolve absolute, parent-relative, and symlinked patch paths with normal Node path semantics.
- Retain settled diff previews in the Pi TUI after successful and partially failed patches.
- Report underlying per-file failure reasons and applied files instead of generic reread instructions.
- Serialize concurrent patch mutations through Pi's per-file mutation queue.
