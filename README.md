# ScreenCompanion

A macOS native application that combines script planning with high-fidelity screen recording. ScreenCompanion serves as your production companion, guiding you through scripts via an integrated teleprompter while recording your screen at professional quality.

## 🎯 Project Overview

ScreenCompanion revolutionizes content creation by solving the common challenge of managing scripts while recording screen content. Whether you're creating tutorials, educational content, or product demos, ScreenCompanion streamlines your workflow from script to final edit.

### Key Features (Planned)

- **📝 Script Planning:** Write and time your scripts with automatic duration estimation
- **🎬 High-Fidelity Recording:** Capture your screen at 60 FPS in up to 4K resolution
- **📺 Integrated Teleprompter:** Follow your script with an auto-scrolling, transparent overlay
- **🎤 Professional Audio:** Mix microphone audio with pristine quality
- **🖱️ Cursor Tracking:** Record cursor movements as metadata for enhanced editing
- **✂️ Basic Editing:** Timeline-based editor with cursor event markers

## 🏗️ Technical Stack

- **Platform:** macOS 13.0 Ventura or later
- **Language:** Swift 5.9+
- **UI Framework:** SwiftUI with AppKit integration
- **Video Core:** ScreenCaptureKit
- **Audio:** AVFoundation
- **Development:** Xcode 15+ (build/sign) + VS Code/Cursor (editing)

## 📋 Documentation

For detailed project requirements, development roadmap, and technical specifications, see:

👉 **[Product Requirements Document (PRD.md)](./PRD.md)**

## 🚀 Development Roadmap

### Phase 0: Environment Setup ✅
- [x] Repository initialization
- [x] PRD creation
- [ ] Xcode project setup
- [ ] Development environment configuration

### Phase 1: MVP Development (Weeks 1-7)
- [ ] **Week 1-2:** Scripting Engine
- [ ] **Week 3-4:** High-Performance Recorder
- [ ] **Week 5-6:** Teleprompter Overlay
- [ ] **Week 7:** Basic Editor & Export

## 🛠️ Setup Instructions

### Prerequisites

1. **macOS 13.0 Ventura or later**
2. **Xcode 15+** (Download from Mac App Store)
3. **VS Code or Cursor** (Optional, for AI-assisted development)
4. **Apple Developer Account** (For code signing and distribution)

### Getting Started

```bash
# Clone the repository
git clone https://github.com/aristidesnakos/mytube.git
cd mytube

# Open in Xcode to build
open ScreenCompanion.xcodeproj

# Or open in VS Code for editing
code .
```

> **Note:** The project follows a hybrid development workflow. Use VS Code/Cursor for code editing with AI assistance, but use Xcode for building, signing, and managing entitlements.

## 📁 Project Structure

```
ScreenCompanion/
├── ScreenCompanion/           # Main app target
│   ├── App/                   # App lifecycle
│   ├── Models/                # Data models
│   ├── Views/                 # SwiftUI views
│   ├── ViewModels/            # MVVM view models
│   ├── Services/              # Business logic
│   ├── Utilities/             # Helpers
│   └── Resources/             # Assets, etc.
├── ScreenCompanion.xcodeproj  # Xcode project
├── PRD.md                     # Product Requirements Document
├── .gitignore                 # Git ignore rules
└── README.md                  # This file
```

## 🤝 Contributing

This project is currently in early development. Contributions, issues, and feature requests are welcome!

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

See the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built with [ScreenCaptureKit](https://developer.apple.com/documentation/screencapturekit) - Apple's modern screen recording framework
- Powered by [SwiftUI](https://developer.apple.com/xcode/swiftui/) - Apple's declarative UI framework
- AI-assisted development with Claude Code

## 📞 Contact

Project Maintainer: [aristidesnakos](https://github.com/aristidesnakos)

---

**Status:** 🟡 Phase 0 - Environment Setup  
**Version:** 0.1.0-alpha  
**Last Updated:** 2025-11-21