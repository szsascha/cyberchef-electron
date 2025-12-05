# CyberChef Electron App

A native macOS Electron application for [CyberChef](https://github.com/gchq/CyberChef) - the Cyber Swiss Army Knife.

![CyberChef Logo](https://github.com/gchq/CyberChef/raw/master/src/web/static/images/cyberchef-256x256.png)

## Features

- Native macOS application
- No Docker required
- Works completely offline
- Universal binary (Intel & Apple Silicon)

## Requirements

- macOS 10.13 or later
- Node.js 16.x or later
- Git
- Xcode Command Line Tools (for icon generation)

## Quick Start

### 1. Clone the Repository

```bash
git clone --recurse-submodules <your-repo-url>
cd cyberchef-electron
```

If you already cloned without submodules:

```bash
git submodule update --init --recursive
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Build CyberChef

```bash
cd CyberChef
npm install
npm run build
cd ..
```

### 4. Generate App Icon

```bash
# Install imagemagick if you don't have it
brew install imagemagick

# Create icon set
mkdir cyberchef.iconset


sips -z 16 16 CyberChef/src/web/static/images/cyberchef-512x512.png --out cyberchef.iconset/icon_16x16.png
sips -z 32 32 CyberChef/src/web/static/images/cyberchef-512x512.png --out cyberchef.iconset/icon_16x16@2x.png
sips -z 32 32 CyberChef/src/web/static/images/cyberchef-512x512.png --out cyberchef.iconset/icon_32x32.png
sips -z 64 64 CyberChef/src/web/static/images/cyberchef-512x512.png --out cyberchef.iconset/icon_32x32@2x.png
sips -z 128 128 CyberChef/src/web/static/images/cyberchef-512x512.png --out cyberchef.iconset/icon_128x128.png
sips -z 256 256 CyberChef/src/web/static/images/cyberchef-512x512.png --out cyberchef.iconset/icon_128x128@2x.png
sips -z 256 256 CyberChef/src/web/static/images/cyberchef-512x512.png --out cyberchef.iconset/icon_256x256.png
sips -z 512 512 CyberChef/src/web/static/images/cyberchef-512x512.png --out cyberchef.iconset/icon_256x256@2x.png
sips -z 512 512 CyberChef/src/web/static/images/cyberchef-512x512.png --out cyberchef.iconset/icon_512x512.png

# Create .icns file
iconutil -c icns cyberchef.iconset -o cyberchef.icns
```

This creates `icon.icns` from the official CyberChef logo.

### 5. Run in Development Mode

```bash
npm start
```

**Note:** The icon may not display properly in development mode - this is normal.

### 6. Build Production App

```bash
npm run build:mac
```

The `.dmg` installer will be in the `dist/` folder.

## Development

### Running the App

```bash
npm start
```

### Building for Distribution

```bash
# Build for macOS (DMG)
npm run build:mac

# Build for all platforms
npm run build
```

## Updating CyberChef

To update to a newer version of CyberChef:

```bash
cd CyberChef
git fetch --tags
git tag -l  # List available versions
git checkout v10.x.x  # Replace with desired version
npm install
npm run build
cd ..
```

Then regenerate the icon and rebuild.

### Update Submodule via Git

```bash
# Update to latest version
git submodule update --remote CyberChef

# Commit the submodule update
git add CyberChef
git commit -m "Update CyberChef submodule to latest version"
```