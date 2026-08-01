# 🎮 Endless Wheel - Godot 4.6 Runner Game

A production-ready endless runner game built with **Godot 4.6** using the **KIDAKU AI Architecture** pattern. Jump over obstacles, beat high scores, and experience smooth mobile gameplay.

[![Godot 4.6](https://img.shields.io/badge/Godot-4.6-blue?logo=godotengine)](https://godotengine.org)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Android](https://img.shields.io/badge/Platform-Android-green?logo=android)](https://play.google.com/store)
[![iOS](https://img.shields.io/badge/Platform-iOS-black?logo=apple)](https://apps.apple.com)

---

## 📸 Features

### 🎮 Gameplay
- **Jump Mechanics** - Touch/tap to jump, physics-based gravity
- **Procedural Spawning** - Randomized obstacle placement and selection
- **Progressive Difficulty** - Speed increases from 450 to 1200 units/sec
- **Score System** - Speed-based scoring with real-time updates
- **High Score Persistence** - Automatic save/load system
- **Collision Detection** - Precise hit detection with game over

### ✨ Visual Effects
- **Animation Tweens** - Squash/stretch jump and land animations
- **Particle Effects** - Dust trails following the player
- **Rotation Animation** - Sprite rotates with increasing speed
- **Camera Shake** - Cinematic effect on collision
- **Mobile Optimization** - 60 FPS target with efficient rendering

### 🎨 User Interface
- **Main Menu** - Clean start screen with high score display
- **In-Game HUD** - Real-time score display during gameplay
- **Game Over Screen** - Shows final score and best score
- **Responsive Controls** - Touch input optimized for mobile
- **Menu Navigation** - Seamless transitions between screens

### 🏗️ Architecture
- **Event Bus Pattern** - Decoupled systems via signal communication
- **Autoload Services** - Global GameEvents and SaveManager
- **Signal-Based** - No direct node references between systems
- **Mobile-First** - Optimized for Android and iOS
- **Extensible** - Ready for audio, analytics, power-ups

---

## 🚀 Quick Start

### Requirements
- **Godot 4.6** (or later)
- **Git** (optional, for cloning)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/endless-wheel.git
   cd endless-wheel
   ```

2. **Open in Godot 4.6**
   - Launch Godot 4.6
   - Click "Open Project"
   - Select `project.godot` file
   - Wait for import (10-30 seconds first load)

3. **Play**
   ```
   Press F5 to run the game
   ```

4. **Build & Export**
   ```
   Project → Export → Android (or iOS)
   Configure your platform settings
   Export AAB or APK
   ```

---

## 📁 Project Structure

```
endless-wheel/
├── project.godot                 # Godot 4.6 configuration
├── README.md                     # This file
├── PRIVACY_POLICY.md             # Privacy policy (required for Play Store)
│
├── src/
│   ├── autoload/                 # Global services
│   │   ├── game_events.gd        # Event bus (signals)
│   │   └── save_manager.gd       # Save/load system
│   │
│   ├── world/                    # Main game scene
│   │   ├── game_world.gd         # Game coordinator
│   │   ├── game_world.tscn       # Main scene (ENTRY POINT)
│   │   └── camera_effects.gd     # Camera shake effects
│   │
│   ├── entities/                 # Game objects
│   │   ├── player.gd             # Player controller
│   │   ├── player.tscn           # Player scene
│   │   ├── obstacle_base.gd      # Obstacle base class
│   │   ├── obstacle.tscn         # Obstacle scene
│   │   └── obstacle_spawner.gd   # Procedural spawner
│   │
│   └── ui/                       # User interface
│       ├── main_menu.gd          # Menu controller
│       ├── main_menu.tscn        # Menu scene
│       ├── hud.gd                # HUD controller
│       ├── hud.tscn              # HUD scene
│       ├── game_over_menu.gd     # End screen
│       └── game_over_menu.tscn   # End screen scene
│
├── assets/
│   └── textures/                 # Sprites and graphics
│       ├── player.png            # Player sprite (64×64)
│       ├── obstacle.png          # Obstacle sprite (64×64)
│       └── wheel.png             # App icon (128×128)
│
└── docs/                         # Documentation
    ├── ARCHITECTURE.md           # System design details
    ├── KIDAKU_AI_MANUAL.md       # Scene documentation
    └── FILE_MANIFEST.md          # Complete file inventory
```

---

## 🎮 How to Play

1. **Start Game**
   - Launch the app
   - Press PLAY button

2. **Jump**
   - Tap/touch anywhere on screen to jump
   - Time your jumps to avoid obstacles

3. **Score**
   - Points increase as you play longer
   - Speed increases over time = higher scores
   - One collision = game over

4. **Save High Score**
   - Automatically saved to device
   - Persists between sessions
   - View best score on main menu

---

## 🔧 Configuration

### Difficulty Settings

Edit in Godot Inspector (GameWorld node):

```gdscript
initial_speed: 450.0          # Starting speed (units/sec)
max_speed: 1200.0             # Speed cap
speed_acceleration: 15.0      # Speed increase per second
spawn_distance_min: 450.0     # Obstacle spacing (min)
spawn_distance_max: 750.0     # Obstacle spacing (max)
```

### Easy Mode
```
initial_speed: 300.0
max_speed: 800.0
speed_acceleration: 10.0
spawn_distance_min: 600.0
spawn_distance_max: 1000.0
```

### Hard Mode
```
initial_speed: 600.0
max_speed: 1500.0
speed_acceleration: 25.0
spawn_distance_min: 300.0
spawn_distance_max: 500.0
```

---

## 🎨 Customization

### Replace Graphics
1. Go to `assets/textures/`
2. Replace PNG files (keep same dimensions):
   - `player.png` (64×64) - Player sprite
   - `obstacle.png` (64×64) - Obstacle sprite
   - `wheel.png` (128×128) - App icon
3. Godot auto-reimports textures

### Add Obstacles
1. Duplicate `src/entities/obstacle.tscn`
2. Change sprite texture in new scene
3. Add to `ObstacleSpawner.obstacle_scenes` array
4. Obstacles spawn randomly from the pool

### Add Audio
```gdscript
# In game_world.gd _ready():
GameEvents.game_started.connect(func(): 
    AudioEngine.play("music_loop"))

GameEvents.game_over.connect(func(_f, _h): 
    AudioEngine.play("game_over_sound"))
```

### Extend Gameplay
See `docs/ARCHITECTURE.md` for:
- Signal hooks for analytics
- Extension points for power-ups
- Adding new game states
- Implementing level systems

---

## 📱 Platform Support

| Platform | Status | Notes |
|----------|--------|-------|
| **Android** | ✅ Ready | AAB export configured |
| **iOS** | ✅ Ready | Xcode export configured |
| **Web** | ✅ Ready | HTML5 export available |
| **Desktop** | ✅ Ready | Windows, macOS, Linux |

### Minimum Requirements

**Android**
- API Level: 21+
- Orientation: Portrait
- Touch input required

**iOS**
- iOS 14.0+
- Orientation: Portrait
- Touch input required

---

## 📊 Performance

- **Target FPS:** 60
- **Resolution:** 1280×720 (adaptive)
- **Memory:** 50-100 MB
- **Active Obstacles:** 5-10 (dynamic)
- **Rendering:** Mobile Forward+ (optimized)
- **Assets:** ETC2/ASTC compressed

---

## 🏗️ Architecture

### Event Bus Pattern
```
GameEvents (Autoload)
├── signal game_started
├── signal game_over(score, high_score)
├── signal score_changed(score)
└── signal speed_updated(speed)
```

No direct node references. All systems communicate via signals.

### Game Loop
```
GameWorld._process()
├── Calculate speed (ramp up)
├── Emit speed_updated → all entities sync
├── Calculate score
├── Emit score_changed → HUD updates
└── Check game state
```

### Save System
```
SaveManager (Autoload)
├── load_gamedata() → Load from disk at startup
├── save_gamedata(score) → Save when game ends
└── high_score → Always in memory
```

---

## 🧩 Code Quality

- **Language:** GDScript 2.0 (Godot 4.6+)
- **Typing:** Strict static typing throughout
- **Patterns:** Event bus, signal-based communication
- **Memory:** Proper queue_free() usage, no leaks
- **Testing:** Manual play-tested across platforms

---

## 📚 Documentation

- **[START_HERE.md](docs/START_HERE.md)** - Getting started guide
- **[ARCHITECTURE.md](docs/ARCHITECTURE.md)** - System design & signal flow
- **[KIDAKU_AI_MANUAL.md](docs/KIDAKU_AI_MANUAL.md)** - Scene hierarchy documentation
- **[FILE_MANIFEST.md](docs/FILE_MANIFEST.md)** - Complete file inventory
- **[PRIVACY_POLICY.md](PRIVACY_POLICY.md)** - Privacy policy (Play Store required)

---

## 📦 Build & Release

### Android (AAB Format)

1. **Configure**
   - Project → Project Settings → Run
   - Configure Android export template
   - Set package name (com.yourcompany.endless_wheel)

2. **Export**
   ```
   Project → Export → Android
   Select "Android App Bundle (AAB)"
   Configure signing (required for Play Store)
   Export file
   ```

3. **Upload to Play Store**
   - Go to Google Play Console
   - Create new app
   - Upload AAB file
   - Fill store listing details
   - Submit for review

### iOS (App Archive)

1. **Configure**
   - Project → Project Settings → Run
   - Configure iOS export template
   - Set bundle identifier

2. **Export**
   ```
   Project → Export → iOS
   Export as Xcode project
   Open in Xcode
   Archive and submit to App Store
   ```

### Web (HTML5)

```
Project → Export → Web
Configure HTML file
Export to build/web/
Deploy to web server
```

---

## 🔒 Privacy & Compliance

This project includes:
- ✅ Privacy Policy template (see `PRIVACY_POLICY.md`)
- ✅ No tracking or analytics (optional to add)
- ✅ No external connections (optional to add)
- ✅ Local save file only
- ✅ GDPR compliant by default

**Important:** Before publishing to any app store, review and customize the privacy policy for your specific implementation.

---

## 🤝 Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open Pull Request

### Development Guidelines
- Follow GDScript naming conventions
- Use `@onready` for scene node references
- Emit signals instead of direct node calls
- Add comments for non-obvious logic
- Test changes on target platform

---

## 📄 License

This project is licensed under the **MIT License** - see [LICENSE](LICENSE) file for details.

You are free to:
- ✅ Use commercially
- ✅ Modify the code
- ✅ Distribute copies
- ✅ Include in proprietary projects

You must:
- ✅ Include license notice
- ✅ Include copyright notice

---

## ⚠️ Disclaimer

This game is provided as-is for educational and commercial use. 

**Before publishing to app stores:**
- Review and customize the privacy policy
- Configure proper signing certificates
- Test thoroughly on target devices
- Comply with app store guidelines
- Set appropriate age ratings

---

## 🐛 Troubleshooting

### Project won't open
```
Ensure Godot 4.6+ is installed
Check that project.godot exists in root folder
Try: Project → Reimport All
```

### Game won't start
```
Check Console for error messages
Verify autoloads: Project → Settings → Autoload
Ensure main scene is set: Project → Settings → Run
```

### Missing textures
```
Project → Reimport All
Wait for import to complete
Restart Godot if needed
```

### Performance issues
```
Check FPS in debugger
Verify obstacle count (should be 5-10)
Profile with Godot's built-in profiler
Reduce active obstacle count if needed
```

See full troubleshooting in `docs/START_HERE.md`

---

## 📞 Support

- 📖 Check documentation in `docs/` folder
- 🐛 Report issues via GitHub Issues
- 💬 Discuss features via GitHub Discussions
- 📧 Contact: [your-email@company.com]

---

## 🙏 Credits

**Framework:** KIDAKU AI Architecture  
**Engine:** Godot 4.6  
**Language:** GDScript 2.0  
**Platform:** Android, iOS, Web

---

## 🎯 Roadmap

- [ ] Sound effects and music
- [ ] Power-up system
- [ ] Multiple difficulty levels
- [ ] Leaderboard integration
- [ ] Analytics dashboard
- [ ] Customizable themes
- [ ] More obstacle types
- [ ] Combo system

---

## 📊 Stats

- **Total Files:** 28
- **Lines of Code:** 279
- **Documentation:** 2,400+
- **Development Time:** Complete & production-ready
- **License:** MIT

---

## 🎮 Get Started Now!

1. Clone this repository
2. Open in Godot 4.6
3. Press F5 to play
4. Customize as needed
5. Export and publish!

---

## 📜 Legal

This project is provided "as-is" without warranty. See LICENSE file for full details.

When publishing to app stores, ensure compliance with:
- ✅ App Store Guidelines (iOS)
- ✅ Google Play Policies (Android)
- ✅ GDPR & Privacy Laws
- ✅ Content Rating Requirements

---

## 🌟 Show Your Support

If you find this project useful:
- ⭐ Star this repository
- 🔄 Share with others
- 🐛 Report bugs
- 💡 Suggest features
- 🎮 Create something amazing

---

**Happy developing! 🚀**

Made with ❤️ for game developers.

---

*Last Updated: July 2026*  
*Godot 4.6 | GDScript 2.0 | Production Ready*
