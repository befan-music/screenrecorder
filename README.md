# Screen Recorder

A free, open-source desktop screen recording application built with Electron.

## Overview

This is a simple, lightweight screen recorder that runs entirely on your local machine. No login required, no payments, no internet connection needed - just download and start recording.

## Features

- **High-Quality Screen Recording**: Record your screen or specific windows
- **Simple Interface**: Clean, intuitive UI with easy-to-use controls
- **No Account Required**: Completely free and runs locally on your computer
- **Privacy First**: All recordings stay on your machine
- **Real-time Preview**: See what you're recording as you record
- **Recording Timer**: Keep track of recording duration
- **Source Selection**: Choose which screen or window to record

## Technology Stack

- **Electron**: Cross-platform desktop application framework
- **HTML/CSS/JavaScript**: Simple, fast frontend
- **MediaRecorder API**: Browser-based screen capture

## Project Structure

```
screenrecording/
├── index.html          # Main application UI
├── renderer.js         # Recording logic and UI interactions
├── main.js             # Electron main process
├── preload.js          # Electron preload script
├── styles.css          # Application styles
├── package.json        # Dependencies and scripts
└── README.md          # This file
```

## Getting Started

### Prerequisites

- Node.js 18+ and npm

### Installation

1. Clone or download this repository
2. Navigate to the project directory:

```bash
cd screenrecording
```

3. Install dependencies:

```bash
npm install
```

4. Run the application:

```bash
npm start
```

## How to Use

1. **Launch the app**: Run `npm start`
2. **Select Source**: Click "Choose Source" to select which screen or window to record
3. **Start Recording**: Click the "Start Recording" button
4. **Record**: The preview shows what you're recording in real-time
5. **Stop Recording**: Click "Stop Recording" when done
6. **Save**: Your recording will be automatically saved to your computer

## Building for Production

To create a distributable package for your platform:

```bash
npm run build
```

This will create an executable application in the `dist/` folder.

## Browser Permissions

The application requires screen capture permissions to function. When you first start recording, your system will ask you to grant these permissions.

## Supported Platforms

- Windows
- macOS
- Linux

## Privacy & Security

- **100% Local**: All recordings are processed and stored on your machine
- **No Tracking**: No analytics, no telemetry, no data collection
- **No Internet Required**: Works completely offline
- **Open Source**: Inspect the code to verify what it does

## Troubleshooting

### Recording Not Starting
- Check that you've granted screen capture permissions
- Try restarting the application
- Ensure you've selected a valid source

### Performance Issues
- Close other resource-intensive applications
- Try recording a smaller window instead of full screen
- Check available disk space

## License

MIT License - Free to use, modify, and distribute

---

**A free, privacy-focused screen recorder for everyone**
