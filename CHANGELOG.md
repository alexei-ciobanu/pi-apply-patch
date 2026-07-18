# Changelog

## [Unreleased]

### Added

- Initial standalone `apply_patch` pi extension.

### Fixed

- Resolve absolute, parent-relative, and symlinked patch paths with normal Node path semantics.
- Show settled diff hunks in the Pi TUI by default after successful and partially failed patches.
- Render complete and partial patch failures with error styling in the Pi TUI.
- Mark complete and partial failures as Pi error results so the entire tool shell is red.
- Use consistent diff colors for standalone added and removed lines.
- Render failure details in normal text on Pi's error-colored shell.
- Show delete operations without reading or rendering the deleted file contents.
- Report underlying per-file failure reasons and applied files instead of generic reread instructions.
- Serialize concurrent patch mutations through Pi's per-file mutation queue.
