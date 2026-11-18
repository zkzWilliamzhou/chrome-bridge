# ChromeBridge - Universal Browser Extension API Adapter

[![npm version](https://img.shields.io/npm/v/chrome-bridge.svg)](https://npmjs.org/package/chrome-bridge)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Build Status](https://img.shields.io/badge/build-passing-brightgreen.svg)](https://github.com/yourname/chrome-bridge/actions)

Write once, deploy everywhere. Cross-browser extension API adapter with automatic normalization.

## 🚀 Quick Start

```bash
npm install chrome-bridge
npx chrome-bridge init ./my-extension
npx chrome-bridge build
```

## ✨ Features

- **Universal APIs**: Single codebase for Chrome, Firefox, Safari, Edge
- **Automatic Adaptation**: API differences handled automatically
- **Permission Management**: Smart permission requests and optimization
- **CI/CD Integration**: Automated cross-browser testing and publishing
- **TypeScript Support**: Full type safety with auto-completion

## 📦 API Coverage

| Feature | Chrome | Firefox | Safari | Edge | ChromeBridge |
|---------|--------|---------|--------|------|--------------|
| Background Scripts | ✅ | ✅ | ✅ | ✅ | ✅ |
| Content Scripts | ✅ | ✅ | ✅ | ✅ | ✅ |
| Storage API | ✅ | ✅ | ✅ | ✅ | ✅ |
| Notifications | ✅ | ✅ | ⚠️ | ✅ | ✅ |
| Side Panel | ✅ | ❌ | ❌ | ✅ | ✅ (fallback) |
| Offscreen Docs | ✅ | ❌ | ❌ | ✅ | ✅ (polyfill) |

## 🔧 CLI Usage

```bash
# Initialize new extension
npx chrome-bridge init my-extension

# Build for specific browser
npx chrome-bridge build --target chrome
npx chrome-bridge build --target firefox
npx chrome-bridge build --target safari
npx chrome-bridge build --target edge

# Run cross-browser tests
npx chrome-bridge test

# Package for distribution
npx chrome-bridge package
```

## 🔄 GitHub Actions

```yaml
name: Cross-Browser Extension
on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        browser: [chrome, firefox, edge]
    
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
      
      - name: Install ChromeBridge
        run: npm install -g chrome-bridge
      
      - name: Build Extension
        run: chrome-bridge build --target ${{ matrix.browser }}
      
      - name: Package
        run: chrome-bridge package --target ${{ matrix.browser }}
```

## 📊 Browser Compatibility

```typescript
import { browser } from 'chrome-bridge';

// Works identically across all browsers
browser.notifications.create({
  type: 'basic',
  iconUrl: 'icon.png',
  title: 'Hello',
  message: 'World'
});

// Automatic permission handling
await browser.permissions.request({ permissions: ['storage'] });

// Storage works the same everywhere
await browser.storage.local.set({ key: 'value' });
const result = await browser.storage.local.get('key');
```

## 🛠️ Architecture

```
┌─────────────────┐
│  Developer Code │
│  (Unified APIs) │
└─────────────────┘
         │
         ▼
┌─────────────────┐
│ ChromeBridge    │
│ - API Router    │
│ - Adapter Layer │
│ - Polyfill Lib  │
└─────────────────┘
         │
         ▼
┌─────────────────┐
│ Native Browser  │
│ - Chrome API    │
│ - Firefox API   │
│ - Safari API    │
│ - Edge API      │
└─────────────────┘
```

## 📖 Documentation

- [Getting Started Guide](docs/getting-started.md)
- [API Reference](docs/api-reference.md)
- [Browser Compatibility](docs/compatibility.md)
- [Migration Guide](docs/migration.md)

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch
3. Run tests: `npm test`
4. Submit a pull request

## 📄 License

MIT © 2026 ChromeBridge Contributors

---

**Ready to build your next extension? Start with ChromeBridge!**