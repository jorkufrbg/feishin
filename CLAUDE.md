# Feishin - Project Analysis

## What does this project do?

Feishin is a modern self-hosted music player designed as a complete rewrite of Sonixd. It provides a sleek interface for streaming music from various self-hosted music servers. The application offers multiple deployment options:

- **Desktop Application**: Cross-platform Electron app supporting both MPV and web player backends
- **Web Application**: Browser-based version with web player backend only
- **Docker Container**: Self-hosted web deployment option

Key features include:

- Multiple player backends (MPV for desktop, web audio for browser)
- Modern, responsive user interface built with React
- Smart playlist editor (for Navidrome servers)
- Synchronized and unsynchronized lyrics support
- Scrobble playback tracking to music servers
- Cross-platform support (Windows, macOS, Linux)
- Support for multiple music server types

## Technologies Used

### Frontend Framework & UI

- **React 19.1.0** - Main UI framework
- **TypeScript** - Type safety and development experience
- **Mantine 8.1.1** - Component library for UI elements
- **React Router 6.16.0** - Client-side routing
- **Framer Motion 12.18.1** - Animations and transitions
- **React Query (TanStack) 4.32.1** - Data fetching and state management

### Desktop Application

- **Electron 35.1.5** - Cross-platform desktop framework
- **Electron Vite 3.1.0** - Build tooling for Electron apps
- **Electron Builder 26.0.12** - Application packaging and distribution

### State Management & Data

- **Zustand 5.0.5** - Lightweight state management
- **Immer 9.0.21** - Immutable state updates
- **IDB Keyval 6.2.1** - IndexedDB wrapper for persistence
- **Zod 3.22.3** - Runtime type validation

### Media & Audio

- **Node-MPV** - MPV media player integration (desktop only)
- **React Player 2.11.0** - Web audio player
- **Audiomotion Analyzer 4.5.0** - Audio visualization
- **Fast Average Color 9.3.0** - Color extraction from album art

### Development & Build Tools

- **Vite 6.3.5** - Build tool and dev server
- **PNPM** - Package manager
- **ESLint 9.24.0** - Code linting
- **Prettier 3.5.3** - Code formatting
- **Stylelint 16.14.1** - CSS linting

### Additional Libraries

- **Axios 1.6.0** - HTTP client for API calls
- **Dayjs 1.11.6** - Date manipulation
- **Lodash 4.17.21** - Utility functions
- **React Icons 5.5.0** - Icon library
- **i18next 21.10.0** - Internationalization
- **Discord RPC** - Discord rich presence integration

### Server Compatibility

Supports multiple music server APIs:

- Navidrome
- Jellyfin
- OpenSubsonic-compatible servers (Airsonic, Ampache, Gonic, etc.)

## Folder Structure

```
feishin-original/
├── .github/                 # GitHub workflows and issue templates
│   ├── ISSUE_TEMPLATE/     # Bug report and feature request templates
│   └── workflows/          # CI/CD workflows
├── .vscode/                # VS Code configuration
├── assets/                 # Static assets
│   ├── fonts/             # Font files
│   └── icons/             # Application icons
├── media/                  # Screenshots and media for README
├── resources/              # Electron build resources
├── src/                    # Source code
│   ├── i18n/              # Internationalization files
│   ├── main/              # Electron main process
│   │   └── features/      # Main process features (Discord RPC, player, lyrics)
│   ├── preload/           # Electron preload scripts
│   ├── remote/            # Remote/server deployment code
│   ├── renderer/          # React frontend application
│   │   ├── api/           # API layer and HTTP clients
│   │   ├── assets/        # Frontend assets (icons, images)
│   │   ├── components/    # Reusable React components
│   │   ├── context/       # React contexts
│   │   ├── features/      # Feature-specific components and logic
│   │   │   ├── albums/    # Album-related components
│   │   │   ├── artists/   # Artist-related components
│   │   │   ├── player/    # Player controls and logic
│   │   │   ├── playlists/ # Playlist management
│   │   │   ├── search/    # Search functionality
│   │   │   ├── settings/  # Application settings
│   │   │   └── ...        # Other feature modules
│   │   ├── hooks/         # Custom React hooks
│   │   ├── layouts/       # Page layout components
│   │   ├── lib/           # Utility libraries and configurations
│   │   ├── router/        # Routing configuration
│   │   ├── store/         # State management (Zustand stores)
│   │   ├── styles/        # Global stylesheets
│   │   ├── themes/        # Theme definitions
│   │   ├── types/         # TypeScript type definitions
│   │   └── utils/         # Utility functions
│   ├── shared/            # Shared code between processes
│   └── types/             # Global TypeScript types
├── *.config.*             # Configuration files
│   ├── electron.vite.config.ts  # Electron Vite configuration
│   ├── remote.vite.config.ts    # Remote deployment config
│   ├── web.vite.config.ts       # Web-only build config
│   ├── eslint.config.mjs        # ESLint configuration
│   └── postcss.config.cjs       # PostCSS configuration
├── package.json           # Dependencies and scripts
├── tsconfig.json          # TypeScript configuration
├── Dockerfile            # Docker container definition
└── README.md             # Project documentation
```

### Key Architectural Components

1. **Electron Main Process** (`src/main/`): Handles system integration, file operations, media keys, Discord RPC, and lyrics fetching
2. **React Renderer** (`src/renderer/`): The main UI application with feature-based organization
3. **Preload Scripts** (`src/preload/`): Secure bridge between main and renderer processes
4. **Shared Code** (`src/shared/`): Type definitions and utilities used across processes
5. **Remote/Web Build** (`src/remote/`): Standalone web version configuration

The project follows a modular architecture with feature-based organization in the renderer, clean separation between Electron processes, and support for multiple deployment targets through different build configurations.

## Important Commands

1. Disable AppArmor for Ubuntu

```bash
echo 0 | sudo tee /proc/sys/kernel/apparmor_restrict_unprivileged_userns
```
