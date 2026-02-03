# Contributing to GitSync

Thank you for your interest in contributing to GitSync! This document provides guidelines for contributing to the project.

## Getting Started

### Prerequisites

- Node.js 18+ LTS
- npm
- An Obsidian vault for testing

### Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/vishal-go/obsidian-gitsync.git
   cd obsidian-gitsync
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start development build (watch mode):
   ```bash
   npm run dev
   ```

4. Link to your Obsidian vault for testing:
   - Copy or symlink the plugin folder to `<YourVault>/.obsidian/plugins/gitsync/`
   - Or develop directly in your vault's plugins folder

5. Reload Obsidian and enable the plugin in **Settings → Community plugins**

## Development Workflow

### Building

```bash
npm run dev      # Watch mode - rebuilds on file changes
npm run build    # Production build
npm run lint     # Run ESLint
```

### Testing

1. Make your changes
2. Run `npm run build` to compile
3. Reload Obsidian (`Ctrl/Cmd + R`)
4. Open Developer Tools (`Ctrl/Cmd + Shift + I`) to check for errors
5. Test your changes manually

### Testing on Mobile

1. Build the plugin: `npm run build`
2. Copy `main.js`, `manifest.json`, and `styles.css` to your mobile vault's plugin folder
3. Use a sync service (iCloud, Dropbox, etc.) or manual transfer
4. Reload Obsidian on mobile

## Code Style

- **TypeScript**: Use strict mode, proper types
- **Formatting**: Follow existing code style
- **Comments**: Add JSDoc comments for public methods
- **Naming**: Use camelCase for variables/functions, PascalCase for classes/interfaces

### File Structure

```
src/
  main.ts           # Plugin lifecycle only
  settings.ts       # Settings tab UI
  types.ts          # Interfaces and defaults
  github-api.ts     # GitHub API wrapper
  sync-service.ts   # Sync logic
```

### Guidelines

- Keep `main.ts` minimal - delegate to other modules
- Each file should have a single responsibility
- Handle errors gracefully with user-friendly notices
- Use `async/await` over promise chains
- Register all listeners with `this.register*` helpers

## Submitting Changes

### Pull Request Process

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Make your changes
4. Test thoroughly (desktop and mobile if possible)
5. Commit with clear messages: `git commit -m "Add: description of feature"`
6. Push to your fork: `git push origin feature/your-feature`
7. Open a Pull Request

### Commit Message Format

```
Type: Short description

Longer description if needed.
```

Types:
- `Add`: New feature
- `Fix`: Bug fix
- `Update`: Update existing feature
- `Refactor`: Code refactoring
- `Docs`: Documentation changes
- `Style`: Formatting, no code change

### Pull Request Checklist

- [ ] Code compiles without errors (`npm run build`)
- [ ] No ESLint warnings (`npm run lint`)
- [ ] Tested on desktop
- [ ] Tested on mobile (if applicable)
- [ ] Updated README if adding features
- [ ] Added comments for complex logic

## Reporting Issues

### Bug Reports

Please include:
- Obsidian version
- Plugin version
- Operating system (and mobile device if applicable)
- Steps to reproduce
- Expected vs actual behavior
- Console errors (if any)

### Feature Requests

- Describe the feature clearly
- Explain the use case
- Consider mobile compatibility

## Questions?

- Open an issue for questions
- Check existing issues first
- Be respectful and patient

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
