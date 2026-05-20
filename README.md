# 🚀 Cosmic Defender

<div align="center">

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![React](https://img.shields.io/badge/react-18.2.0-61dafb.svg)
![Hacktoberfest](https://img.shields.io/badge/hacktoberfest-2024-orange.svg)

**A modern, arcade-style space shooter game built with React and HTML5 Canvas**

[Play Demo](#installation) • [Features](#features) • [How It Works](#how-it-works) • [Contributing](#contributing)

</div>

---

## 📖 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Game Mechanics](#game-mechanics)
- [Installation](#installation)
- [How It Works](#how-it-works)
- [Project Architecture](#project-architecture)
- [Technologies Used](#technologies-used)
- [Game Controls](#game-controls)
- [Contributing](#contributing)
- [Roadmap](#roadmap)
- [License](#license)

---

## 🎮 Overview

**Cosmic Defender** is an immersive space shooter game that combines classic arcade gameplay with modern web technologies. Built entirely with React and the HTML5 Canvas API, it demonstrates advanced game development concepts including:

- Real-time collision detection
- Particle systems for visual effects
- Progressive difficulty scaling
- State management for complex game logic
- 60 FPS smooth gameplay
- Responsive game UI

The game challenges players to defend Earth from waves of cosmic invaders, each with unique behaviors and characteristics. As you progress through levels, the difficulty increases with faster spawn rates and tougher enemies.

### 🎯 Project Goals

- Demonstrate modern React patterns for game development
- Showcase Canvas API capabilities
- Provide a beginner-friendly codebase for learning
- Create an engaging, polished gaming experience
- Build a community-driven open-source project

---

## ✨ Features

### 🎨 Visual & Audio
- **Animated Starfield Background** - Scrolling star particles create a space atmosphere
- **Particle Effects System** - Explosions, trails, and power-up collection effects
- **Glowing Effects** - Dynamic shadows and glows for enemies and bullets
- **Smooth Animations** - 60 FPS canvas rendering with trail effects
- **Color-Coded Entities** - Visual differentiation between enemy types and power-ups

### 🎯 Gameplay Mechanics
- **4 Unique Enemy Types**
  - **Basic (Red Circle)** - Standard enemy with balanced stats
  - **Fast (Orange Triangle)** - Quick moving, lower health
  - **Tank (Purple Square)** - Slow but high health
  - **Zigzag (Cyan Hexagon)** - Moves in zigzag patterns
  
- **Power-Up System**
  - **Health (Green)** - Restores 30 health points
  - **Rapid Fire (Orange)** - Increases fire rate for 5 seconds
  - **Shield (Blue)** - Coming soon!

- **Progressive Difficulty** - Every 500 points increases the level and enemy spawn rate
- **Health System** - Visual health bar with color indicators (green/yellow/red)
- **Score & High Score Tracking** - Persistent high score across sessions
- **Pause/Resume Functionality** - Press ESC to pause anytime

### 🕹️ Player Experience
- **Smooth Controls** - Responsive keyboard input with arrow keys
- **Multiple Game States** - Menu, Playing, Paused, Game Over
- **Visual Feedback** - Particles and effects for all interactions
- **Real-time HUD** - Score, level, and health displayed on-screen

---

## 🎲 Game Mechanics

### Enemy Spawning System

Enemies spawn at the top of the screen at intervals determined by the current level. The spawn rate decreases (gets faster) as you level up:

```javascript
Initial spawn rate: 1500ms
Minimum spawn rate: 500ms
Rate decrease: 100ms per level
```

### Enemy Characteristics

| Type | Health | Speed | Points | Special Ability |
|------|--------|-------|--------|----------------|
| **Basic** | 1 | 2.0 | 10 | None |
| **Fast** | 1 | 4.0 | 20 | High speed |
| **Tank** | 3 | 1.0 | 50 | High durability |
| **Zigzag** | 2 | 2.5 | 30 | Zigzag movement |

### Collision Detection

The game uses **Axis-Aligned Bounding Box (AABB)** collision detection:

```javascript
// Collision occurs when rectangles overlap
if (rect1.x < rect2.x + rect2.width &&
    rect1.x + rect1.width > rect2.x &&
    rect1.y < rect2.y + rect2.height &&
    rect1.y + rect1.height > rect2.y) {
    // Collision detected!
}
```

This efficient algorithm checks if two rectangles overlap by comparing their edges.

### Difficulty Progression

The game becomes progressively harder:

1. **Every 500 points** - Level increases
2. **Each level** - Enemy spawn rate decreases by 100ms (faster spawning)
3. **Higher levels** - More enemy types become available
4. **Level 1-2** - Only Basic and Fast enemies
5. **Level 3+** - Tank enemies appear
6. **Level 4+** - Zigzag enemies appear

### Power-Up Drop System

When an enemy is destroyed, there's a **30% chance** it drops a power-up:

```javascript
Power-up drop rate: 30%
Power-up types: 3 (Health, Rapid Fire, Shield)
Distribution: Equal probability (33.3% each)
```

---

## 💻 Installation

### Prerequisites

- **Node.js** v14.0.0 or higher
- **npm** or **yarn**
- A modern web browser (Chrome, Firefox, Safari, Edge)

### Step-by-Step Setup

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/cosmic-defender.git
cd cosmic-defender
```

2. **Install dependencies**
```bash
npm install
```

3. **Start the development server**
```bash
npm start
```

4. **Open your browser**
```
The game will automatically open at http://localhost:3000
```

### Building for Production

```bash
npm run build
```

This creates an optimized production build in the `build/` folder.

---

## 🔧 How It Works

### Architecture Overview

Cosmic Defender uses a **component-based architecture** with React managing the UI layer and Canvas API handling the game rendering.

```
┌─────────────────────────────────────────┐
│         React Component Layer           │
│  (State Management & UI Controls)       │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│         Game Loop (60 FPS)              │
│  (Update Logic & Collision Detection)   │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│      Canvas Rendering Layer             │
│  (Draw Entities, Effects, & HUD)        │
└─────────────────────────────────────────┘
```

### Core Game Loop

The game uses **requestAnimationFrame** for a smooth 60 FPS game loop:

```javascript
gameLoop() {
  1. Clear canvas with trail effect
  2. Update player position based on input
  3. Update and draw bullets
  4. Spawn enemies based on timer
  5. Update and draw enemies
  6. Check collisions (bullets vs enemies, enemies vs player)
  7. Update and draw power-ups
  8. Update and draw particle effects
  9. Draw HUD (score, health, level)
  10. Request next frame
}
```

### State Management

The game uses React's `useState` and `useRef` hooks:

- **`useState`** - For game state (menu, playing, paused, gameOver), score, level, and high score
- **`useRef`** - For mutable game data that doesn't trigger re-renders (player position, bullets, enemies, particles)

This hybrid approach ensures:
- UI updates only when necessary (state changes)
- Game logic runs at full 60 FPS without React re-renders
- Optimal performance for real-time gameplay

### Entity Management

All game entities are stored in arrays within the `gameRef`:

```javascript
gameRef.current = {
  player: { x, y, width, height, speed, health },
  bullets: [{ x, y, width, height, speed, damage }],
  enemies: [{ x, y, width, height, speed, health, type }],
  particles: [{ x, y, vx, vy, life, color, size }],
  powerUps: [{ x, y, width, height, type, speed }],
  keys: { 'ArrowLeft': false, 'ArrowRight': false, ... }
}
```

### Rendering Pipeline

#### 1. Background Layer
```javascript
// Trail effect for motion blur
ctx.fillStyle = 'rgba(10, 10, 30, 0.3)';
ctx.fillRect(0, 0, 800, 600);

// Animated starfield
for (let i = 0; i < 50; i++) {
  const y = ((i * 137.5 + now * 0.05) % 600);
  ctx.fillRect(x, y, 2, 2);
}
```

#### 2. Entity Layer
- Draw player ship (triangle with engine glow)
- Draw bullets with glow effects
- Draw enemies (different shapes per type)
- Draw power-ups (glowing circles)

#### 3. Effects Layer
```javascript
// Particle system
particles.forEach(p => {
  p.x += p.vx;  // Apply velocity
  p.y += p.vy;
  p.life -= 0.02;  // Fade out
  ctx.globalAlpha = p.life;
  ctx.fillRect(p.x, p.y, p.size, p.size);
});
```

#### 4. HUD Layer
- Score and level display
- Health bar with color coding
- Visual indicators for active power-ups

### Input Handling

Keyboard input uses event listeners with a key state tracker:

```javascript
const keys = {};

window.addEventListener('keydown', (e) => {
  keys[e.key] = true;
});

window.addEventListener('keyup', (e) => {
  keys[e.key] = false;
});

// In game loop
if (keys['ArrowLeft']) player.x -= player.speed;
if (keys['ArrowRight']) player.x += player.speed;
if (keys[' ']) shoot();
```

This approach allows for:
- Multiple simultaneous key presses
- Smooth, continuous movement
- No input lag

### Collision Detection Algorithm

```javascript
function checkCollision(rect1, rect2) {
  // Check if rectangles overlap on X-axis
  const xOverlap = rect1.x < rect2.x + rect2.width &&
                   rect1.x + rect1.width > rect2.x;
  
  // Check if rectangles overlap on Y-axis
  const yOverlap = rect1.y < rect2.y + rect2.height &&
                   rect1.y + rect1.height > rect2.y;
  
  // Collision occurs if overlap on both axes
  return xOverlap && yOverlap;
}
```

**Collision Checks Per Frame:**
- Bullets vs Enemies: O(n * m) where n = bullets, m = enemies
- Enemies vs Player: O(n) where n = enemies
- Power-ups vs Player: O(n) where n = power-ups

**Optimization:** Entities are removed from arrays immediately after collision, reducing checks in subsequent frames.

### Particle System

Creates explosion and trail effects:

```javascript
function createParticles(x, y, color, count) {
  const particles = [];
  for (let i = 0; i < count; i++) {
    particles.push({
      x, y,
      vx: (Math.random() - 0.5) * 8,  // Random X velocity
      vy: (Math.random() - 0.5) * 8,  // Random Y velocity
      life: 1,  // Fade from 1 to 0
      color,
      size: Math.random() * 3 + 2
    });
  }
  return particles;
}
```

**Particle Lifecycle:**
1. Created at collision point with random velocities
2. Move outward based on velocity
3. Fade out over time (life -= 0.02)
4. Removed when life reaches 0

---

## 🏗️ Project Architecture

### File Structure

```
cosmic-defender/
├── public/
│   ├── index.html          # HTML template with meta tags
│   └── favicon.ico         # Game icon
│
├── src/
│   ├── components/
│   │   └── CosmicDefender.jsx    # Main game component (500+ lines)
│   │
│   ├── App.js              # Root component
│   ├── App.css             # App-level styles
│   ├── index.js            # React entry point
│   └── index.css           # Global styles + Tailwind import
│
├── .gitignore              # Git ignore rules
├── package.json            # Dependencies and scripts
├── README.md               # This file
├── CONTRIBUTING.md         # Contribution guidelines
├── LICENSE                 # MIT License
└── SETUP.md                # Detailed setup instructions
```

### Component Breakdown

#### CosmicDefender.jsx (Main Component)

```javascript
CosmicDefender
├── State Management
│   ├── gameState: 'menu' | 'playing' | 'paused' | 'gameOver'
│   ├── score: number
│   ├── highScore: number
│   └── level: number
│
├── Game Logic (useRef)
│   ├── player: Player object
│   ├── bullets: Bullet[]
│   ├── enemies: Enemy[]
│   ├── particles: Particle[]
│   ├── powerUps: PowerUp[]
│   └── keys: KeyState object
│
├── Core Functions
│   ├── initGame() - Reset game state
│   ├── gameLoop() - Main update/render loop
│   ├── spawnEnemy() - Create enemy instances
│   ├── spawnPowerUp() - Create power-up instances
│   ├── checkCollision() - AABB collision detection
│   └── createParticles() - Particle effect generation
│
├── React Hooks
│   ├── useEffect - Keyboard event listeners
│   ├── useEffect - Game loop management
│   └── useCallback - Memoized game loop
│
└── UI Components
    ├── Canvas - Game rendering surface
    ├── Menu Screen - Start game UI
    ├── Pause Screen - Pause menu
    └── Game Over Screen - End game UI
```

### Data Flow

```
User Input (Keyboard)
      ↓
Key State Updates (gameRef)
      ↓
Game Loop (60 FPS)
      ↓
Entity Updates (position, collision)
      ↓
State Changes (score, level, gameState)
      ↓
Canvas Rendering
      ↓
Visual Output (Screen)
```

---

## 🛠️ Technologies Used

### Core Technologies

| Technology | Version | Purpose |
|------------|---------|---------|
| **React** | 18.2.0 | UI framework and state management |
| **HTML5 Canvas** | Native | 2D graphics rendering |
| **JavaScript (ES6+)** | ES2021 | Game logic and algorithms |
| **CSS3** | - | Styling and animations |
| **Tailwind CSS** | 3.3.0 | Utility-first CSS framework |

### Libraries & Tools

- **lucide-react** (0.263.1) - Icon components (Rocket, Star, Zap)
- **react-scripts** (5.0.1) - Build tooling and development server
- **requestAnimationFrame** - Browser API for smooth animations

### Key JavaScript Features Used

- **ES6 Modules** - Import/export syntax
- **Arrow Functions** - Concise function syntax
- **Destructuring** - Object and array destructuring
- **Spread Operator** - Array and object spreading
- **Template Literals** - String interpolation
- **Array Methods** - map, filter, forEach, splice
- **Hooks** - useState, useEffect, useRef, useCallback
- **Canvas API** - 2D rendering context

### Browser APIs

- **Canvas 2D Context** - Drawing shapes, text, and effects
- **requestAnimationFrame** - Smooth 60 FPS animations
- **Keyboard Events** - User input handling
- **Date.now()** - Timing and cooldowns

---

## 🎮 Game Controls

### Keyboard Controls

| Key | Action |
|-----|--------|
| **Arrow Keys** or **WASD** | Move spaceship in 4 directions |
| **Spacebar** | Fire bullets |
| **ESC** | Pause/Resume game |

### Mouse Controls

- **Click "Start Game"** - Begin new game
- **Click "Resume"** - Continue paused game
- **Click "Main Menu"** - Return to menu

---

## 📊 Game Statistics

### Performance Metrics

- **Frame Rate:** 60 FPS (locked)
- **Canvas Size:** 800x600 pixels
- **Entity Count:** Up to 100+ simultaneous entities
- **Particle System:** 300+ particles per second during combat
- **Input Latency:** < 16ms (1 frame)

### Gameplay Metrics

- **Bullet Speed:** 8 pixels per frame
- **Player Speed:** 6 pixels per frame
- **Enemy Speed:** 1-4 pixels per frame (varies by type)
- **Shoot Cooldown:** 250ms (normal), 100ms (rapid fire)
- **Power-up Duration:** 5 seconds (rapid fire)
- **Enemy Spawn Rate:** 1500ms → 500ms (progressive)

---

## 🤝 Contributing

We love contributions! Cosmic Defender is open-source and welcomes developers of all skill levels.

### Quick Contribution Guide

1. **Fork** the repository
2. **Clone** your fork: `git clone https://github.com/yourusername/cosmic-defender.git`
3. **Create a branch**: `git checkout -b feature/amazing-feature`
4. **Make changes** and test thoroughly
5. **Commit**: `git commit -m 'Add amazing feature'`
6. **Push**: `git push origin feature/amazing-feature`
7. **Open a Pull Request**

### Good First Issues

Perfect for beginners! 🌟

- [ ] Add sound effects (shooting, explosions, power-ups)
- [ ] Implement mobile touch controls
- [ ] Add more enemy types (spiral, bouncing, shooter)
- [ ] Create boss battles every 5 levels
- [ ] Add weapon upgrades (double shot, spread shot, laser)
- [ ] Implement local high score leaderboard
- [ ] Add background music with volume control
- [ ] Create different difficulty modes (Easy, Normal, Hard)
- [ ] Add player ship customization (colors, skins)
- [ ] Implement achievement system

### Enhancement Ideas

For experienced contributors 💪

- [ ] Online multiplayer (co-op or versus)
- [ ] Backend leaderboard with authentication
- [ ] Level editor for custom enemy waves
- [ ] Story mode with missions
- [ ] Special abilities and ultimate attacks
- [ ] Screen shake and advanced effects
- [ ] Replay system
- [ ] Tournament mode
- [ ] Mobile-responsive design
- [ ] Progressive Web App (PWA) support

### Code Contribution Guidelines

- Follow existing code style and formatting
- Add comments for complex logic
- Test your changes thoroughly
- Update documentation if needed
- Keep commits atomic and well-described

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

---

## 🗺️ Roadmap

### Version 1.1.0 (Planned)
- [ ] Sound effects and background music
- [ ] Mobile touch controls
- [ ] 3 new enemy types
- [ ] Shield power-up functionality
- [ ] Settings menu (volume, difficulty)

### Version 1.2.0 (Future)
- [ ] Boss battles
- [ ] Weapon upgrade system
- [ ] Achievement system
- [ ] Local leaderboard

### Version 2.0.0 (Long-term)
- [ ] Online multiplayer
- [ ] Backend leaderboard
- [ ] Story mode
- [ ] Level editor
- [ ] PWA support

---

## 🐛 Known Issues

None currently! 🎉

Found a bug? Please [open an issue](https://github.com/yourusername/cosmic-defender/issues) with:
- Description of the problem
- Steps to reproduce
- Expected vs actual behavior
- Screenshots (if applicable)
- Browser and OS information

---

## 📜 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

**TL;DR:** You can use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of this software. Just include the original license and copyright notice.

---

## 🙏 Acknowledgments

- Inspired by classic arcade games like **Galaga**, **Space Invaders**, and **Asteroids**
- Built with ❤️ for the open-source community
- Special thanks to all contributors who make this project better!
- Created for **Hacktoberfest 2024**

---

## 📞 Contact & Support

- **GitHub Issues:** [Report bugs or request features](https://github.com/yourusername/cosmic-defender/issues)
- **GitHub Discussions:** [Ask questions or share ideas](https://github.com/yourusername/cosmic-defender/discussions)
- **Email:** your.email@example.com
- **Twitter:** [@yourusername](https://twitter.com/yourusername)

---

## 📈 Project Stats

![GitHub stars](https://img.shields.io/github/stars/yourusername/cosmic-defender?style=social)
![GitHub forks](https://img.shields.io/github/forks/yourusername/cosmic-defender?style=social)
![GitHub issues](https://img.shields.io/github/issues/yourusername/cosmic-defender)
![GitHub pull requests](https://img.shields.io/github/issues-pr/yourusername/cosmic-defender)
![Lines of code](https://img.shields.io/tokei/lines/github/yourusername/cosmic-defender)

---

## 🎯 Learning Outcomes

By studying and contributing to this project, you'll learn:

✅ **React Fundamentals** - Components, hooks, state management  
✅ **Game Development** - Game loops, collision detection, entity systems  
✅ **Canvas API** - 2D rendering, animations, visual effects  
✅ **Performance Optimization** - 60 FPS rendering, efficient algorithms  
✅ **Event Handling** - Keyboard input, game states  
✅ **Algorithm Design** - Collision detection, particle systems  
✅ **Project Structure** - Clean code organization, modularity  
✅ **Open Source** - Collaboration, version control, documentation  

---

## 🌟 Star History

If you find this project helpful or interesting, please consider giving it a ⭐ on GitHub!

---

<div align="center">

**Made with 🚀 and ❤️ for Hacktoberfest 2024**

[⬆ Back to Top](#-cosmic-defender)

</div>
