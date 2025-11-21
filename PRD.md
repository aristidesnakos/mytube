# Product Requirements Document: ScreenCompanion

## Executive Summary

ScreenCompanion is a macOS native application that revolutionizes content creation by combining script planning with high-fidelity screen recording. The application serves as a production companion, guiding users through their scripts via an integrated teleprompter while simultaneously recording their screen at professional-grade quality.

**Version:** 1.0  
**Last Updated:** 2025-11-21  
**Status:** Phase 0 - Planning

---

## Table of Contents

1. [Product Overview](#product-overview)
2. [Goals and Objectives](#goals-and-objectives)
3. [Target Audience](#target-audience)
4. [Technical Architecture](#technical-architecture)
5. [Feature Requirements](#feature-requirements)
6. [Development Roadmap](#development-roadmap)
7. [Risk Assessment](#risk-assessment)
8. [Success Metrics](#success-metrics)
9. [Dependencies and Constraints](#dependencies-and-constraints)

---

## Product Overview

### Problem Statement

Content creators, educators, and professionals often struggle with:
- Managing scripts while recording screen content
- Maintaining natural pacing and flow during recordings
- Achieving professional-quality screen recordings
- Synchronizing script delivery with on-screen actions
- Tracking cursor movements for post-production editing

### Solution

ScreenCompanion addresses these challenges by providing:
- Integrated script planning and timing estimation
- Real-time teleprompter overlay during recording
- High-fidelity 60FPS screen capture using ScreenCaptureKit
- Precise cursor tracking with timestamped metadata
- Professional-grade audio mixing
- Basic video editing with metadata-driven timeline

### Value Proposition

- **For Content Creators:** Streamline video production workflow from script to final edit
- **For Educators:** Create polished instructional videos with professional delivery
- **For Professionals:** Produce high-quality product demos and presentations

---

## Goals and Objectives

### Primary Goals

1. **Simplify Production Workflow:** Reduce the cognitive load of managing scripts and recording simultaneously
2. **Professional Quality Output:** Deliver 4K/60FPS recordings with pristine audio
3. **Enhanced Post-Production:** Provide rich metadata for efficient editing
4. **Native Performance:** Leverage macOS platform capabilities for optimal performance

### Success Criteria

- Users can plan, record, and produce videos 50% faster than traditional workflows
- 60FPS screen capture with zero dropped frames on target hardware
- Sub-100ms latency between recording start and teleprompter sync
- 95%+ user satisfaction with interface intuitiveness

---

## Target Audience

### Primary Users

1. **YouTube Content Creators**
   - Need: Tutorial and demo video production
   - Pain Point: Managing scripts while demonstrating software

2. **Online Educators**
   - Need: Course material and lecture recordings
   - Pain Point: Maintaining engagement while reading from notes

3. **Product Managers**
   - Need: Product demo and walkthrough videos
   - Pain Point: Forgetting key talking points during recordings

### User Personas

**Persona 1: "Tutorial Tom"**
- Creates software tutorials on YouTube
- Records 2-3 videos per week
- Values: Efficiency, professional quality, easy editing
- Tech-savvy, comfortable with macOS

**Persona 2: "Educator Emma"**
- Online course instructor
- Records lectures and demonstrations
- Values: Script adherence, clear delivery, minimal retakes
- Moderate technical skills

**Persona 3: "Demo Dave"**
- Product manager at SaaS company
- Creates internal and external product demos
- Values: Polish, brand consistency, quick turnaround
- Time-constrained, needs intuitive tools

---

## Technical Architecture

### Core Technology Stack

#### Platform Requirements
- **Operating System:** macOS 13.0 Ventura or later
- **Processor:** Apple Silicon (M1/M2/M3) or Intel x86_64
- **Memory:** Minimum 8GB RAM (16GB recommended)
- **Storage:** 500MB application + recording space

#### Programming Languages & Frameworks
- **Language:** Swift 5.9+
- **UI Framework:** SwiftUI (primary interface)
- **Legacy UI:** AppKit (windowing system for overlay)
- **Video Core:** ScreenCaptureKit (screen capture)
- **Audio:** AVFoundation (audio capture and mixing)
- **Persistence:** Core Data or JSON file storage

#### Development Tools
- **Primary IDE:** Xcode 15+ (compilation, signing, debugging)
- **Code Editor:** VS Code / Cursor (code editing, AI assistance)
- **AI Assistant:** Claude Code (code generation and refactoring)
- **Version Control:** Git / GitHub

### System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    ScreenCompanion                       │
├─────────────────────────────────────────────────────────┤
│  Presentation Layer (SwiftUI)                            │
│  ├─ Script Editor                                        │
│  ├─ Recording Controls                                   │
│  ├─ Timeline Editor                                      │
│  └─ Settings Panel                                       │
├─────────────────────────────────────────────────────────┤
│  Business Logic Layer                                    │
│  ├─ Script Manager (timing, segmentation)               │
│  ├─ Recording Engine (orchestration)                    │
│  ├─ Cursor Tracker (NSEvent monitoring)                 │
│  └─ Export Manager (video assembly)                     │
├─────────────────────────────────────────────────────────┤
│  Platform Layer (AppKit + System Frameworks)             │
│  ├─ Teleprompter Overlay (NSPanel)                      │
│  ├─ Screen Capture (SCStream)                           │
│  ├─ Audio Capture (AVCaptureSession)                    │
│  └─ File I/O (FileManager)                              │
├─────────────────────────────────────────────────────────┤
│  Data Layer                                              │
│  ├─ Scripts (JSON)                                       │
│  ├─ Cursor Metadata (JSON)                              │
│  └─ User Preferences (UserDefaults)                     │
└─────────────────────────────────────────────────────────┘
```

### Security & Permissions

#### Required Entitlements
1. **Hardened Runtime:** Required for ScreenCaptureKit usage
2. **App Sandbox:** With "User Selected File" (read/write) access
3. **Camera Access:** Optional for picture-in-picture
4. **Microphone Access:** Required for audio recording
5. **Screen Recording:** Required for screen capture

#### Info.plist Keys
- `NSDesktopFolderUsageDescription`
- `NSMicrophoneUsageDescription`
- `NSCameraUsageDescription` (optional)
- `NSScreenCaptureUsageDescription`

---

## Feature Requirements

### Phase 0: Environment Setup

**Status:** Foundation  
**Timeline:** Week 0 (Pre-development)

#### Xcode Setup (Critical Path)
- [ ] Install Xcode 15+ from Mac App Store
- [ ] Create new macOS App project
  - Product Name: "ScreenCompanion"
  - Interface: SwiftUI
  - Language: Swift
  - Minimum Deployment: macOS 13.0
- [ ] Configure Signing & Capabilities
  - Add "Hardened Runtime"
  - Add "App Sandbox" with "User Selected File" access
  - Configure Development Team for code signing
- [ ] Verify project builds successfully (⌘R)

#### Development Environment Setup
- [ ] Initialize Git repository
- [ ] Create comprehensive `.gitignore` for Swift/Xcode
- [ ] Configure VS Code / Cursor
  - Install "Swift" extension by The Swift Server Workgroup
  - Configure Swift LSP (Language Server Protocol)
- [ ] Set up Claude Code integration
  - Run `claude config add .` for project context
  - Test AI code generation capability

#### Repository Structure
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
├── .gitignore                 # Git ignore rules
└── README.md                  # Project documentation
```

---

### Phase 1: Core Infrastructure (MVP)

**Status:** Planned  
**Timeline:** Weeks 1-7  
**Goal:** Minimum viable product with core recording and scripting features

---

#### Week 1-2: Scripting Engine ("The Planner")

**Objective:** Enable users to write, time, and segment scripts

##### User Stories
- As a content creator, I want to write my script in the app so I can estimate video duration
- As a user, I want to see estimated duration so I can plan my recording
- As a user, I want to split my script into sections so I can organize my content

##### Functional Requirements

**FR-1.1: Text Editor**
- Rich text input using SwiftUI `TextEditor`
- Real-time character and word count display
- Auto-save every 30 seconds
- Support for basic formatting (optional: bold, italic)

**FR-1.2: Duration Algorithm**
- Formula: `Duration (minutes) = Word Count / 140 WPM`
- Display as: "Estimated: X min Y sec"
- Update in real-time as user types
- Allow customization of WPM (range: 100-180)

**FR-1.3: Script Segmentation**
- Define "Beats" (script sections): Intro, Main Content, Demo, Outro
- Each beat displays its own word count and duration
- Drag-and-drop reordering of beats
- Color-coded beats in UI

**FR-1.4: Data Persistence**
- Save scripts as JSON files in user-selected directory
- JSON schema:
```json
{
  "title": "My Video Script",
  "created": "2025-11-21T00:00:00Z",
  "modified": "2025-11-21T01:30:00Z",
  "wpm": 140,
  "beats": [
    {
      "id": "uuid",
      "name": "Intro",
      "text": "Welcome to...",
      "order": 0
    }
  ]
}
```

##### Technical Requirements
- Swift `Codable` protocol for JSON serialization
- `ObservableObject` view model for reactive UI
- Debounced auto-save to prevent excessive I/O

##### Acceptance Criteria
- [ ] User can create new script
- [ ] Duration updates within 100ms of text change
- [ ] Scripts save/load without data loss
- [ ] UI remains responsive with 10,000+ word scripts

---

#### Week 3-4: High-Performance Recorder

**Objective:** Capture screen at 60FPS with professional quality

##### User Stories
- As a user, I want to record my screen at 60FPS so my videos are smooth
- As a user, I want to include my microphone audio so I can narrate
- As a user, I want to choose which display/window to record

##### Functional Requirements

**FR-2.1: Permission Handling**
- Detect screen recording permission status
- Detect microphone permission status
- Present user-friendly dialogs explaining permissions
- Deep-link to System Preferences if permissions denied
- Graceful degradation (disable features vs. crash)

**FR-2.2: Screen Capture Configuration**
- Use ScreenCaptureKit `SCStream` API
- Capture options:
  - **Resolution:** Native Retina (up to 4K)
  - **Frame Rate:** 60 FPS
  - **Color Space:** Display P3
  - **Source:** Entire display, specific display, or window
- Exclude ScreenCompanion windows from capture
- Hardware acceleration via Metal

**FR-2.3: Audio Capture**
- Microphone input via `AVCaptureSession`
- Audio format: 48kHz, 16-bit, AAC
- Optional noise reduction
- Real-time audio level meter
- Mute/unmute hotkey (⌘⇧M)

**FR-2.4: Recording Controls**
- Start/Stop/Pause recording
- Visual recording indicator (red dot in menu bar)
- Keyboard shortcuts:
  - ⌘R: Start/Stop
  - ⌘P: Pause/Resume
- Recording timer display (HH:MM:SS)

##### Technical Requirements

**TR-2.1: ScreenCaptureKit Setup**
```swift
let configuration = SCStreamConfiguration()
configuration.width = 3840  // 4K
configuration.height = 2160
configuration.minimumFrameInterval = CMTime(value: 1, timescale: 60)
configuration.colorSpaceName = CGColorSpace.displayP3
configuration.pixelFormat = kCVPixelFormatType_32BGRA
```

**TR-2.2: Audio Synchronization**
- Use `CMSampleBuffer` timestamps for A/V sync
- Common timebase for both streams
- Buffer management to prevent drift
- Maximum sync tolerance: ±33ms (2 frames at 60fps)

**TR-2.3: Performance Optimization**
- Metal-backed `CVPixelBuffer` for GPU acceleration
- Asynchronous encoding to prevent frame drops
- Background thread for file I/O
- Memory pressure monitoring

##### Acceptance Criteria
- [ ] Achieves 60 FPS on M1 MacBook Air (baseline hardware)
- [ ] Zero dropped frames during 10-minute recording
- [ ] Audio sync drift < 50ms over 30 minutes
- [ ] Recording starts within 500ms of button press
- [ ] Output file plays correctly in QuickTime Player

---

#### Week 5-6: Companion Overlay ("The Prompter")

**Objective:** Display script as transparent, non-obstructive HUD

##### User Stories
- As a user, I want to see my script while recording so I don't forget my points
- As a user, I want the prompter to scroll automatically so I can maintain flow
- As a user, I want to customize prompter appearance so it's comfortable to read

##### Functional Requirements

**FR-3.1: HUD Window**
- Transparent, floating window
- Click-through (doesn't capture mouse events)
- Always-on-top (floats above all windows)
- Excluded from screen recording
- Draggable by title bar
- Resizable with stored preferences

**FR-3.2: Prompter Display**
- Large, readable font (default: 24pt San Francisco)
- High contrast text (white on semi-transparent black)
- Auto-scrolling synchronized with recording timer
- Current sentence/paragraph highlighted
- Configurable scroll speed

**FR-3.3: Synchronization**
- Start scrolling when recording begins
- Pause scrolling when recording pauses
- Scroll speed calculated from script duration and recording time remaining
- Manual scroll override (mouse wheel, trackpad)
- Jump-to-beat buttons

**FR-3.4: Appearance Customization**
- Font size: 16-48pt
- Opacity: 50-100%
- Background color: Black, Dark Gray, Blue
- Text color: White, Yellow, Green
- Position presets: Top, Bottom, Left, Right

##### Technical Requirements

**TR-3.1: AppKit NSPanel Implementation**
```swift
class TeleprompterPanel: NSPanel {
    override var canBecomeKey: Bool { false }
    override var canBecomeMain: Bool { false }
    
    init() {
        super.init(
            contentRect: NSRect(x: 0, y: 0, width: 800, height: 200),
            styleMask: [.titled, .closable, .resizable, .nonactivatingPanel],
            backing: .buffered,
            defer: false
        )
        
        self.level = .floating
        self.isOpaque = false
        self.backgroundColor = NSColor.black.withAlphaComponent(0.7)
        self.ignoresMouseEvents = true  // Click-through
        self.collectionBehavior = [.canJoinAllSpaces, .stationary]
    }
}
```

**TR-3.2: SwiftUI Integration**
- Wrap NSPanel in `NSViewRepresentable` / `NSViewControllerRepresentable`
- Bind SwiftUI state to AppKit properties
- Use Combine for reactive updates

**TR-3.3: Auto-Scroll Algorithm**
```
scrollSpeed = totalScrollHeight / estimatedDuration
currentPosition = scrollSpeed * elapsedTime
```

##### Acceptance Criteria
- [ ] Window is transparent and click-through
- [ ] Not visible in screen recordings
- [ ] Scrolling is smooth (no jank)
- [ ] Maintains sync within 2 seconds over 10-minute recording
- [ ] User can manually override auto-scroll without breaking sync

---

#### Week 7: MVP Editor & Export

**Objective:** Basic video editing and export functionality

##### User Stories
- As a user, I want to see my recording on a timeline so I can review it
- As a user, I want to see where I clicked so I can identify key moments
- As a user, I want to export my video so I can upload it

##### Functional Requirements

**FR-4.1: Timeline View**
- Horizontal timeline with playback scrubber
- Thumbnail preview strip (every 2 seconds)
- Waveform visualization for audio
- Playback controls (play, pause, skip ±5s)
- Zoom controls (fit to window, 100%, 200%)

**FR-4.2: Cursor Metadata Overlay**
- Display click events as vertical markers on timeline
- Marker colors:
  - Blue: Left click
  - Yellow: Right click
  - Green: Double-click
- Hover tooltip showing timestamp and coordinates
- Click marker to jump to that timestamp

**FR-4.3: Basic Trimming**
- Set in/out points to trim start and end
- Split clip at playhead
- Delete selected clip segment
- Non-destructive editing (original file preserved)

**FR-4.4: Export**
- Format options: .mov (ProRes), .mp4 (H.264)
- Resolution options: Original, 1080p, 720p
- Quality presets: High (25 Mbps), Medium (10 Mbps), Low (5 Mbps)
- Progress bar with time remaining estimate
- Reveal in Finder when complete

##### Technical Requirements

**TR-4.1: Timeline Rendering**
- Use `AVKit` `AVPlayerView` for playback
- `AVAssetImageGenerator` for thumbnails
- `AVAudioPlayer` for waveform visualization

**TR-4.2: Cursor Metadata Format**
```json
{
  "recording_id": "uuid",
  "start_time": "2025-11-21T12:00:00Z",
  "events": [
    {
      "timestamp": 1.234,
      "type": "left_click",
      "position": {"x": 1920, "y": 1080}
    }
  ]
}
```

**TR-4.3: Export Pipeline**
- Use `AVAssetExportSession` for transcoding
- `AVMutableComposition` for trimming
- Background export with progress callback
- Error handling for insufficient disk space

##### Acceptance Criteria
- [ ] Timeline loads 10-minute video in < 3 seconds
- [ ] Playback is smooth (no buffering)
- [ ] Click markers align with video events (±100ms)
- [ ] Export completes successfully
- [ ] Exported video plays in VLC, QuickTime, and web browsers

---

### Phase 2: Advanced Features (Post-MVP)

**Status:** Future  
**Timeline:** TBD

#### Potential Features
- Picture-in-picture camera overlay
- Multi-take management
- Cloud sync (iCloud Drive)
- Collaborative script editing
- Advanced editing (transitions, titles)
- AI-powered script suggestions
- Voice recognition for hands-free control
- Analytics (recording quality metrics)
- Template library for common video types
- Plugin system for extensibility

---

## Development Roadmap

### Hybrid Workflow Strategy

**Philosophy:** Leverage AI for rapid code generation, use Xcode for Apple-specific features

#### Workflow Steps

1. **Design in VS Code (with AI)**
   - Write Swift code using AI assistance (Claude Code)
   - Implement business logic and algorithms
   - Refactor and optimize code
   - Write unit tests

2. **Build in Xcode**
   - Compile and run (⌘R)
   - Manage entitlements and permissions
   - Debug with Instruments
   - Profile performance
   - Handle code signing

3. **Version Control (Git)**
   - Commit frequently (feature branches)
   - Meaningful commit messages
   - Pull requests for review
   - Tag releases

#### Weekly Milestones

| Week | Milestone | Deliverable | Success Metric |
|------|-----------|-------------|----------------|
| 0 | Environment Setup | Project builds in Xcode | Green build |
| 1 | Text Editor | Basic script input | 500-word script |
| 2 | Duration Estimation | Working timer | Accurate to ±10% |
| 3 | Screen Capture | 60 FPS recording | Zero drops |
| 4 | Audio Integration | Synced audio | < 50ms drift |
| 5 | HUD Window | Floating panel | Click-through works |
| 6 | Auto-Scroll | Synced prompter | ±2s accuracy |
| 7 | Export | Working video file | Plays in QuickTime |

---

## Risk Assessment

### Technical Risks

#### Risk 1: ScreenCaptureKit Permissions

**Impact:** HIGH  
**Probability:** MEDIUM  
**Description:** macOS denies screen recording permission, blocking core functionality

**Mitigation Strategy:**
- Comprehensive `Info.plist` configuration with clear usage descriptions
- User-friendly permission request flow with visual guides
- Fallback to legacy `CGWindowListCreateImage` API if ScreenCaptureKit unavailable
- Extensive testing on clean macOS installations
- Documentation for troubleshooting permission issues

**Contingency Plan:**
- Provide video tutorial for granting permissions
- Detect permission state and guide user to System Preferences
- Log permission request failures for debugging

---

#### Risk 2: Audio/Video Synchronization

**Impact:** HIGH  
**Probability:** MEDIUM  
**Description:** Microphone audio drifts from video over long recordings

**Mitigation Strategy:**
- Use `CMSampleBuffer` timestamps from the same timebase
- Implement drift detection and correction
- Regular sync checks every 60 seconds
- Audio/video buffer management

**Contingency Plan:**
- Provide manual A/V sync adjustment in editor
- Record separate audio file as backup
- Implement post-processing sync correction

---

#### Risk 3: Build System Fragility

**Impact:** MEDIUM  
**Probability:** HIGH  
**Description:** VS Code builds fail due to SwiftUI preview issues or incomplete tooling

**Mitigation Strategy:**
- Always keep Xcode open as "source of truth"
- Use Xcode for final builds and debugging
- Limit VS Code to code editing only
- Document known VS Code/Swift tooling limitations

**Contingency Plan:**
- Fall back to Xcode-only development if VS Code issues persist
- Use Xcode Cloud for CI/CD instead of local builds

---

#### Risk 4: Performance on Intel Macs

**Impact:** MEDIUM  
**Probability:** MEDIUM  
**Description:** 60 FPS screen capture drops frames on older Intel hardware

**Mitigation Strategy:**
- Adaptive quality settings based on hardware detection
- Performance profiling on various Mac models
- Optimize Metal pipeline for Intel GPUs
- Allow users to lower FPS/resolution

**Contingency Plan:**
- Minimum requirement: Apple Silicon only (M1+)
- Or: Reduce default to 30 FPS on Intel
- Provide performance benchmarking tool

---

#### Risk 5: App Store Rejection

**Impact:** HIGH  
**Probability:** LOW  
**Description:** App rejected due to entitlement usage or privacy concerns

**Mitigation Strategy:**
- Follow Apple's guidelines strictly
- Clear, justified privacy policy
- Transparent permission requests
- No data collection or telemetry without opt-in

**Contingency Plan:**
- Distribute via direct download (notarized)
- Use Gumroad or Paddle for licensing
- Build community outside App Store

---

### Business Risks

#### Risk 6: Market Competition

**Impact:** MEDIUM  
**Probability:** HIGH  
**Description:** Existing tools (ScreenFlow, Camtasia) offer similar features

**Mitigation Strategy:**
- Focus on integrated script+record workflow (unique value prop)
- Target specific user persona (tutorial creators)
- Competitive pricing
- Superior UX for primary use case

---

#### Risk 7: macOS Version Fragmentation

**Impact:** LOW  
**Probability:** MEDIUM  
**Description:** Supporting older macOS versions increases complexity

**Mitigation Strategy:**
- Minimum: macOS 13.0 Ventura (ScreenCaptureKit requirement)
- Use `@available` checks for newer APIs
- Document feature availability by OS version

---

## Success Metrics

### Phase 1 (MVP) Metrics

#### Engineering KPIs
- **Build Success Rate:** > 95% (Xcode builds succeed)
- **Test Coverage:** > 70% (unit tests)
- **Performance:** 60 FPS recording on M1 MacBook Air
- **Crash Rate:** < 0.1% (per user session)
- **Audio Sync Accuracy:** < 50ms drift over 30 minutes

#### User Experience KPIs
- **Permission Grant Rate:** > 80% (users complete setup)
- **Recording Completion Rate:** > 90% (recordings finish without errors)
- **Export Success Rate:** > 98% (exports complete)
- **Time to First Recording:** < 5 minutes (from app launch for new user)

### Post-MVP Metrics

#### Adoption Metrics
- **Weekly Active Users:** Track growth
- **Retention Rate (Week 1):** > 40%
- **Retention Rate (Month 1):** > 20%

#### Engagement Metrics
- **Average Recordings per User per Week:** > 2
- **Average Recording Duration:** Track to optimize features
- **Feature Usage:** % users using teleprompter, editor, etc.

#### Quality Metrics
- **User Satisfaction Score (NPS):** > 40
- **App Store Rating:** > 4.0 stars
- **Support Ticket Rate:** < 5% of users

---

## Dependencies and Constraints

### Technical Dependencies

#### System Requirements
- macOS 13.0 Ventura or later
- ScreenCaptureKit framework availability
- 8GB RAM minimum (16GB recommended)
- 5GB available storage (for recordings)

#### Development Dependencies
- Xcode 15+ (free via Mac App Store)
- Apple Developer Account ($99/year for distribution)
- VS Code / Cursor (free)
- Claude Code subscription (for AI assistance)

#### Third-Party Frameworks
- **Minimal External Dependencies:** Use native frameworks where possible
- Potential: Swift Algorithms, Swift Collections (Apple packages)
- Avoid: Large third-party SDKs to minimize bloat

### Business Constraints

#### Timeline Constraints
- Phase 0: 1 week (environment setup)
- Phase 1: 7 weeks (MVP development)
- **Total Time to MVP:** 8 weeks

#### Resource Constraints
- **Team Size:** 1 developer (AI-augmented)
- **Budget:** < $500 (Apple Developer + tools)
- **Support:** Community-based (GitHub issues)

### Legal Constraints

#### Privacy Compliance
- No data collection without explicit consent
- Screen recording warning to users
- Compliance with macOS privacy standards
- No third-party analytics by default

#### Licensing
- Open-source: MIT License (repository)
- Or: Proprietary with commercial licensing
- Clear attribution for any third-party code

---

## Appendices

### Appendix A: Recommended .gitignore

```gitignore
# macOS System Files
.DS_Store

# Xcode User Settings
UserInterfaceState.xcuserstate
xcuserdata/

# Build Artifacts
DerivedData/
build/
*.moved-aside

# Swift Package Manager
.build/
.swiftpm/

# Temporary Files
*.tmp
*.log
```

### Appendix B: Key Technical References

- [ScreenCaptureKit Documentation](https://developer.apple.com/documentation/screencapturekit)
- [SwiftUI Documentation](https://developer.apple.com/documentation/swiftui)
- [AVFoundation Guide](https://developer.apple.com/documentation/avfoundation)
- [App Sandbox](https://developer.apple.com/documentation/security/app_sandbox)
- [Hardened Runtime](https://developer.apple.com/documentation/security/hardened_runtime)

### Appendix C: Glossary

- **Beat:** A script segment (e.g., Intro, Demo, Outro)
- **HUD:** Heads-Up Display (transparent overlay window)
- **ScreenCaptureKit:** Apple's framework for screen recording (macOS 12.3+)
- **SwiftUI:** Apple's declarative UI framework
- **WPM:** Words Per Minute (speaking rate metric)
- **SCStream:** ScreenCaptureKit's stream class for capture sessions
- **CMSampleBuffer:** Core Media sample buffer for A/V data

---

## Document Control

**Version History:**

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-11-21 | Initial | PRD created from project specification |

**Approvals:**

| Role | Name | Date | Signature |
|------|------|------|-----------|
| Product Owner | TBD | - | - |
| Technical Lead | TBD | - | - |
| Stakeholder | TBD | - | - |

**Distribution:**
- Development Team
- Stakeholders
- Community Contributors (if open-source)

---

**END OF DOCUMENT**
