# Development Environment

Feishin is a modern self-hosted music player built with Electron and React. The development environment requires the following technologies:

## Programming Languages and Frameworks
- **Node.js** (v23.11.0 recommended) - JavaScript runtime environment
- **TypeScript** (^5.8.3) - Type system for JavaScript
- **React** (^19.1.0) - Frontend framework
- **Electron** (^35.1.5) - Cross-platform desktop application framework

## Development Tools
- **electron-vite** - Build system specifically designed for Electron applications
- **pnpm** - Fast, disk space efficient package manager (required)
- **Visual Studio Code** - Recommended IDE with extensive TypeScript and React support
- **MPV** - External media player binary (required for native audio playback)

## Build System
- **Vite** (^6.3.5) - Fast build tool and development server
- **electron-builder** - Packaging and distribution tool
- Multi-target builds supporting Electron, web, and remote deployments

# Dependencies and Installation

## System Dependencies

### Node.js and pnpm Installation
```bash
# Install Node.js (using NodeSource repository)
curl -fsSL https://deb.nodesource.com/setup_23.x | sudo -E bash -
sudo apt-get install -y nodejs

# Install pnpm globally
curl -fsSL https://get.pnpm.io/install.sh | sh -
source ~/.bashrc

# Verify installations
node --version  # Should be v23.11.0 or higher
pnpm --version
```

### MPV Media Player Installation
```bash
# Install MPV (required for native audio playback)
sudo apt update
sudo apt install mpv

# Verify MPV installation
mpv --version
```

### Additional System Dependencies
```bash
# Install development tools and libraries
sudo apt install -y \
  build-essential \
  git \
  python3 \
  python3-pip \
  libnss3-dev \
  libatk-bridge2.0-dev \
  libdrm2 \
  libgtk-3-dev \
  libgbm-dev \
  libasound2-dev

# Install credential storage libraries (for password management)
sudo apt install -y libsecret-1-0 libsecret-1-dev
```

## Project Dependencies Installation

### Core Project Setup
```bash
# Clone the repository
git clone https://github.com/jeffvli/feishin.git
cd feishin

# Install all project dependencies
pnpm install

# Install Electron app dependencies
pnpm run postinstall
```

### Key Dependencies Overview

**Core Framework Dependencies:**
- React (^19.1.0) - Frontend framework
- Electron (^35.1.5) - Desktop application framework
- TypeScript (^5.8.3) - Type system and compilation

**UI and Styling:**
- @mantine/core (^8.1.1) - Component library with full ecosystem
- react-icons (^5.5.0) - Icon library
- sass-embedded (^1.89.0) - SCSS preprocessing

**State Management:**
- zustand (^5.0.5) - State management
- @tanstack/react-query (^4.32.1) - Server state management

**Media and Audio:**
- node-mpv (custom fork) - MPV integration
- react-player (^2.11.0) - Web audio player
- audiomotion-analyzer (^4.5.0) - Audio visualization

**Build and Development Tools:**
- electron-vite (^3.1.0) - Build system
- vite (^6.3.5) - Build tool and dev server
- electron-builder (^26.0.12) - Packaging

# Development Setup on Ubuntu with VS Code

## Step 1: Install Visual Studio Code

```bash
# Install VS Code using official Microsoft repository
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /etc/apt/trusted.gpg.d/
echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/trusted.gpg.d/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" | sudo tee /etc/apt/sources.list.d/vscode.list

sudo apt update
sudo apt install code

# Launch VS Code
code --version
```

## Step 2: Install Required VS Code Extensions

Open VS Code and install the following extensions (available in the project's `.vscode/extensions.json`):

```bash
# Install extensions via command line
code --install-extension dbaeumer.vscode-eslint
code --install-extension esbenp.prettier-vscode
code --install-extension bradlc.vscode-tailwindcss
code --install-extension ms-vscode.vscode-typescript-next
```

**Recommended Additional Extensions:**
- ESLint - JavaScript/TypeScript linting
- Prettier - Code formatting
- TypeScript Importer - Auto import for TypeScript
- Auto Rename Tag - HTML tag renaming
- Bracket Pair Colorizer - Better bracket visualization
- GitLens - Enhanced Git capabilities

## Step 3: Configure Development Environment

### Ubuntu-Specific Configuration

```bash
# Disable namespace restrictions (required for Electron on Ubuntu)
# This needs to be run after each reboot
echo 0 | sudo tee /proc/sys/kernel/apparmor_restrict_unprivileged_userns

# Make this persistent across reboots (optional)
echo 'kernel.apparmor_restrict_unprivileged_userns=0' | sudo tee -a /etc/sysctl.conf
```

### VS Code Workspace Configuration

The project includes pre-configured VS Code settings in `.vscode/settings.json`:

- **Code Formatting**: Prettier as default formatter for TypeScript, JavaScript, and JSON
- **ESLint Integration**: Automatic linting and fixing on save
- **TypeScript Configuration**: Enhanced TypeScript support with project diagnostics
- **File Associations**: Proper handling of configuration files
- **Search Exclusions**: Optimized search performance by excluding build directories

### Environment Variables Setup

```bash
# Create .env file in project root (if needed for development)
touch .env

# Example environment variables (adjust as needed)
echo "NODE_ENV=development" >> .env
echo "ELECTRON_IS_DEV=1" >> .env
```

## Step 4: Development Workflow Setup

### Initial Setup and Verification

```bash
# Navigate to project directory
cd /path/to/feishin

# Install dependencies (if not done already)
pnpm install

# Run type checking to verify setup
pnpm run typecheck

# Run linting to verify code quality setup
pnpm run lint

# Start development server
pnpm run dev
```

### VS Code Debugging Configuration

The project includes debugging configurations in `.vscode/launch.json`:

- **Debug Main Process**: Debug the Electron main process
- **Debug Renderer Process**: Debug the React renderer process  
- **Debug All**: Combined debugging of both processes

**To use debugging:**
1. Set breakpoints in your code
2. Go to VS Code's Debug panel (Ctrl+Shift+D)
3. Select "Debug All" configuration
4. Press F5 to start debugging

### Development Commands Reference

```bash
# Development
pnpm run dev                 # Start development server
pnpm run dev:watch          # Start with watch mode (HMR)

# Building
pnpm run build              # Full production build
pnpm run build:electron     # Build Electron app only
pnpm run build:web          # Build web version only

# Quality Assurance
pnpm run typecheck          # Run TypeScript type checking
pnpm run lint               # Run ESLint and Stylelint
pnpm run lint:fix           # Fix linting issues automatically

# Testing and Distribution
pnpm run start              # Preview production build
pnpm run package:dev        # Package for development testing
```

## Step 5: Troubleshooting Common Ubuntu Issues

### Electron Sandbox Issues
If you encounter sandbox-related errors:

```bash
# Temporary fix (lost on reboot)
echo 0 | sudo tee /proc/sys/kernel/apparmor_restrict_unprivileged_userns

# Permanent fix
echo 'kernel.apparmor_restrict_unprivileged_userns=0' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

### Chrome Sandbox Configuration
For Ubuntu 24.04 specifically:

```bash
# If you see SUID sandbox errors
sudo chmod 4755 /path/to/chrome-sandbox
sudo chown root:root /path/to/chrome-sandbox
```

### MPV Path Configuration
Ensure MPV is accessible:

```bash
# Check MPV installation
which mpv
mpv --version

# If not in PATH, note the full path for application settings
```

### File Permissions
```bash
# Ensure proper file permissions for development
sudo chown -R $USER:$USER /path/to/feishin
chmod -R 755 /path/to/feishin
```

## Step 6: Verify Complete Setup

```bash
# Final verification commands
cd /path/to/feishin

# Check Node.js and pnpm versions
node --version    # Should be v23.11.0+
pnpm --version    # Should be latest

# Check project dependencies
pnpm list

# Run type checking
pnpm run typecheck

# Start development server
pnpm run dev
```

**Success Indicators:**
- No TypeScript errors in `pnpm run typecheck`
- Development server starts without errors
- Electron application window opens
- VS Code shows no ESLint errors
- MPV path is configured correctly in application settings

Your development environment is now ready for Feishin development on Ubuntu with VS Code!