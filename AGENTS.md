# GitSync - Development Guide

## Project Overview

GitSync is an Obsidian community plugin that syncs your vault to GitHub using the REST API. It works on both mobile and desktop without requiring Git to be installed.

- **Target**: Obsidian Community Plugin (TypeScript → bundled JavaScript)
- **Entry point**: `src/main.ts` compiled to `main.js`
- **Release artifacts**: `main.js`, `manifest.json`, `styles.css`

## Architecture

```
src/
  main.ts           # Plugin entry point, lifecycle, commands
  settings.ts       # Settings tab UI and exports
  types.ts          # TypeScript interfaces and default settings
  github-api.ts     # GitHub REST API wrapper
  sync-service.ts   # Sync logic (push/pull/sync operations)
```

### Module Responsibilities

| Module | Purpose |
|--------|---------|
| `main.ts` | Plugin lifecycle, ribbon icon, commands, auto-sync |
| `settings.ts` | Settings tab with all configuration UI |
| `types.ts` | `GitSyncSettings` interface, `DEFAULT_SETTINGS`, sync types |
| `github-api.ts` | GitHub API calls: auth, files, commits, trees |
| `sync-service.ts` | Orchestrates sync: file reading, exclusions, upload/download |

## Environment & Tooling

- **Node.js**: v18+ LTS recommended
- **Package manager**: npm
- **Bundler**: esbuild
- **Types**: `obsidian` type definitions

### Commands

```bash
npm install          # Install dependencies
npm run dev          # Build in watch mode
npm run build        # Production build
npm run lint         # Run ESLint
```

## Key Features

1. **GitHub REST API**: No Git binary needed, works on mobile
2. **Batch uploads**: Uses Git Data API for efficient multi-file commits
3. **Binary file support**: Images, PDFs encoded as base64
4. **Auto-sync**: Configurable interval (5-120 minutes)
5. **Exclusions**: Skip folders/files from sync

## GitHub API Flow

### Push
1. Read all vault files (respecting exclusions)
2. Create blobs for large files
3. Create a new tree with all files
4. Create a commit pointing to the tree
5. Update branch reference

### Pull
1. Get latest commit SHA
2. Fetch tree recursively
3. Download each file's content
4. Write to vault (creating folders as needed)

## Settings Structure

```typescript
interface GitSyncSettings {
  githubUsername: string;
  githubToken: string;
  repositoryName: string;
  branch: string;
  autoSync: boolean;
  autoSyncInterval: number;
  lastSyncTime: number;
  excludedFolders: string[];
  excludedFiles: string[];
  commitMessage: string;
}
```

## Security Considerations

- Token stored in plugin data (encrypted by Obsidian)
- Only `repo` scope required
- Private repos created by default
- No telemetry or external services beyond GitHub API
- User must explicitly configure and enable sync

## Adding New Features

### New Command
```typescript
// In main.ts onload()
this.addCommand({
  id: 'gitsync-new-feature',
  name: 'New feature description',
  callback: async () => {
    // Implementation
  }
});
```

### New Setting
1. Add property to `GitSyncSettings` in `types.ts`
2. Add default value to `DEFAULT_SETTINGS`
3. Add UI in `settings.ts` `display()` method

### Modifying Sync Behavior
- File operations: `sync-service.ts`
- API calls: `github-api.ts`

## Testing

1. Build: `npm run build`
2. Reload Obsidian: `Ctrl/Cmd + R`
3. Check console for errors: `Ctrl/Cmd + Shift + I`
4. Test on mobile by copying files to vault

## Do's and Don'ts

### Do
- Use `this.register*` helpers for cleanup
- Handle errors gracefully with user notices
- Keep API calls minimal and batched
- Test on mobile before release

### Don't
- Store sensitive data in plain text
- Make unnecessary API calls
- Block the main thread during sync
- Commit `main.js` or `node_modules`

## Release Checklist

1. Update `version` in `manifest.json`
2. Update `versions.json` with new version mapping
3. Run `npm run build`
4. Create GitHub release with tag matching version
5. Attach `main.js`, `manifest.json`, `styles.css`

## References

- [Obsidian Plugin API](https://docs.obsidian.md)
- [GitHub REST API](https://docs.github.com/en/rest)
- [GitHub Git Data API](https://docs.github.com/en/rest/git)
