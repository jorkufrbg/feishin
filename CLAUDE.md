# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Feishin is a modern self-hosted music player built with Electron and React. It's a rewrite of Sonixd that supports multiple music server backends (Navidrome, Jellyfin, OpenSubsonic-compatible) with both MPV and web player backends.

## Development Commands

### Important for development on UBUNTU

1. Disable namespace restrictions (required for Electron on Ubuntu)

2. This needs to be run after each reboot
```sh
echo 0 | sudo tee /proc/sys/kernel/apparmor_restrict_unprivileged_userns
```

3. Make this persistent across reboots (optional)

```sh
echo 'kernel.apparmor_restrict_unprivileged_userns=0' | sudo tee -a /etc/sysctl.conf
```

### Essential Commands

- `pnpm run dev` - Start the development server
- `pnpm run dev:watch` - Start development server in watch mode (for main/preload HMR)
- `pnpm run build` - Full build (includes typecheck, electron, and remote builds)
- `pnpm run typecheck` - Run TypeScript type checking for all parts
- `pnpm run lint` - Run ESLint and stylelint
- `pnpm run lint:fix` - Fix linting errors automatically

### Specific Build Commands

- `pnpm run build:electron` - Build electron app (main, preload, renderer)
- `pnpm run build:remote` - Build remote app only
- `pnpm run build:web` - Build standalone web app
- `pnpm run start` - Start app in production preview mode

### Type Checking

- `pnpm run typecheck:node` - Type check main process (tsconfig.node.json)
- `pnpm run typecheck:web` - Type check renderer process (tsconfig.web.json)

### Package Management

Uses `pnpm` as the package manager. The project has specific `pnpm` configurations for `electron` and `esbuild` dependencies.

## Architecture

### Multi-Target Build System

The project builds for three different targets:

1. **Electron Desktop App** - Main target with both MPV and web player backends
2. **Remote/Hosted Web Version** - Hosted at feishin.vercel.app
3. **Standalone Web App** - For local web deployment

### Source Structure

```
src/
├── main/           # Electron main process
├── preload/        # Electron preload scripts  
├── renderer/       # React frontend (main UI)
├── remote/         # Remote/web-specific code
├── shared/         # Shared utilities and types
├── types/          # TypeScript type definitions
└── i18n/           # Internationalization
```

### Renderer (Frontend) Architecture

- **Features-based organization** - Code organized by feature domains in `src/renderer/features/`
- **Zustand for state management** - Multiple stores in `src/renderer/store/`
- **React Query (@tanstack/react-query)** - For server state management
- **Mantine UI components** - Component library for the interface
- **React Router** - For navigation

### Key Technologies

- **Frontend**: React 19, TypeScript, Mantine UI, Zustand, React Query
- **Backend**: Electron, Node.js
- **Media Player**: MPV integration via node-mpv
- **Build System**: electron-vite, Vite
- **Package Manager**: pnpm

### Path Aliases

The build system defines several path aliases:

- `/@/main` → `src/main`
- `/@/preload` → `src/preload`
- `/@/renderer` → `src/renderer`
- `/@/remote` → `src/remote`
- `/@/shared` → `src/shared`
- `/@/i18n` → `src/i18n`

### Platform-Specific Code

The build system supports platform-specific code with environment flags:

- `import.meta.env.IS_LINUX`
- `import.meta.env.IS_MACOS`
- `import.meta.env.IS_WIN`

## Development Notes

### Multi-Process Electron Architecture

- **Main Process** (`src/main/`) - Window management, system integration, MPV control
- **Preload Scripts** (`src/preload/`) - Bridge between main and renderer processes
- **Renderer Process** (`src/renderer/`) - React UI application

### Music Server Integration

Supports multiple server types via API abstraction:

- Navidrome API
- Jellyfin API
- OpenSubsonic-compatible APIs

### Player Backends

- **MPV Backend** - Native audio playback via MPV binary
- **Web Backend** - Browser-based audio playback

### Styling

- Uses CSS Modules with scoped naming: `fs-[name]-[local]`
- Mantine theme system for UI consistency
- Custom SCSS/CSS in `src/renderer/styles/`

### Internationalization

- i18next for translations
- Translation files managed in `src/i18n/`
- Weblate integration for community translations

### Docker Support

- Multi-stage Docker builds supported
- Environment variables for server configuration
- Can be deployed as web-only version via Docker

## Code Analysis Summary

**Feishin** is a modern, cross-platform music player application designed for self-hosted music streaming. The project serves as a complete rewrite of Sonixd, offering a desktop-first experience built with Electron and React.

**Key Features and Components:**
- **Multi-platform desktop application** supporting Windows, macOS, and Linux
- **Dual player backend support**: Native MPV integration for high-quality audio and web-based playback
- **Multiple music server compatibility**: Navidrome, Jellyfin, and OpenSubsonic-compatible APIs
- **Modern React-based UI** with responsive design and dark/light theme support
- **Advanced music management**: Smart playlists, synchronized lyrics, scrobbling capabilities
- **Web deployment options**: Standalone web version and Docker containerization
- **Internationalization support** with community-driven translations via Weblate

**Architecture:**
- Electron multi-process architecture (main process, preload scripts, renderer process)
- Feature-based code organization with modular components
- State management using Zustand with React Query for server state
- TypeScript throughout with strict type checking

## Required Dependencies

**Core Framework Dependencies:**
- **React** (^19.1.0) - Frontend framework
- **Electron** (^35.1.5) - Desktop application framework
- **TypeScript** (^5.8.3) - Type system and compilation
- **Node.js** - Runtime environment (v23.11.0 recommended)

**UI and Styling:**
- **@mantine/core** (^8.1.1) - Component library
- **@mantine/hooks, @mantine/dates, @mantine/form, @mantine/modals, @mantine/notifications** (^8.1.1) - Mantine ecosystem
- **react-icons** (^5.5.0) - Icon library
- **sass-embedded** (^1.89.0) - SCSS preprocessing
- **postcss-preset-mantine** (^1.17.0) - PostCSS configuration

**State Management and Data Fetching:**
- **zustand** (^5.0.5) - State management
- **@tanstack/react-query** (^4.32.1) - Server state management
- **@tanstack/react-query-devtools, @tanstack/react-query-persist-client** (^4.32.1) - React Query extensions

**Media and Audio:**
- **node-mpv** (custom fork) - MPV integration for native audio playback
- **react-player** (^2.11.0) - Web audio player
- **audiomotion-analyzer** (^4.5.0) - Audio visualization

**Electron Ecosystem:**
- **@electron-toolkit/preload, @electron-toolkit/utils** (^3.0.1, ^4.0.0) - Electron utilities
- **electron-store** (^8.1.0) - Persistent storage
- **electron-updater** (^6.3.9) - Auto-updates
- **electron-localshortcut** (^3.2.1) - Keyboard shortcuts
- **mpris-service** (^2.1.2) - Media player integration (Linux)

**Build and Development Tools:**
- **electron-vite** (^3.1.0) - Build system
- **vite** (^6.3.5) - Build tool and dev server
- **electron-builder** (^26.0.12) - Packaging and distribution
- **@vitejs/plugin-react** (^4.3.4) - React integration
- **pnpm** - Package manager (required)

**Code Quality and Linting:**
- **eslint** (^9.24.0) with multiple plugins for React and TypeScript
- **stylelint** (^16.14.1) - CSS/SCSS linting
- **prettier** (^3.5.3) - Code formatting

**Internationalization and Utilities:**
- **i18next, react-i18next** (^21.10.0, ^11.18.6) - Internationalization
- **dayjs** (^1.11.6) - Date manipulation
- **lodash** (^4.17.21) - Utility functions
- **axios** (^1.6.0) - HTTP client
- **zod** (^3.22.3) - Schema validation

**External System Requirements:**
- **MPV binary** - Required for native audio playback (user must install separately)
- **Docker** (optional) - For containerized deployment
- **libsecret/kwallet** (Linux) - Credential storage
