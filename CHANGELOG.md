# Changelog

All notable changes to GitSync will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-02-03

### Added

- Initial release
- Push to GitHub - upload all vault files to repository
- Pull from GitHub - download all files from repository
- Full sync - push then pull in one operation
- Auto-sync with configurable interval (5-120 minutes)
- Ribbon icon for quick sync access
- Command palette commands:
  - `GitSync: Push to GitHub`
  - `GitSync: Pull from GitHub`
  - `GitSync: Sync with GitHub`
- Settings tab with full configuration:
  - GitHub username
  - Personal access token (masked input)
  - Repository name
  - Branch selection
  - Auto-sync toggle and interval
  - Custom commit message with `{{date}}` placeholder
  - Excluded folders configuration
  - Excluded files configuration
- Test connection button to verify credentials
- Automatic private repository creation if it doesn't exist
- Binary file support (images, PDFs, etc.)
- Batch upload using Git Data API for efficiency
- Mobile compatibility (iOS and Android)
- Default exclusions:
  - `.obsidian/plugins`
  - `.obsidian/themes`
  - `.trash`

### Technical

- Uses GitHub REST API (no Git binary required)
- Efficient batch commits using Git trees
- Base64 encoding for binary files
- Proper error handling with user notifications
