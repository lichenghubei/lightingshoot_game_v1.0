# Thunder Shooter - 雷电风格飞行射击游戏

## 1. Project Overview

**Project Name:** Thunder Shooter  
**Project Type:** HTML5 Canvas Game (Single-file)  
**Core Functionality:** A vertical scrolling space shooter game inspired by classic Thunder Force series, featuring player aircraft, enemy waves, shooting mechanics, and score tracking.  
**Target Users:** Casual gamers, retro game enthusiasts

---

## 2. Visual & Rendering Specification

### Scene Setup
- **Canvas:** Full viewport, responsive to window resize
- **Background:** Multi-layer parallax scrolling starfield (3 layers at different speeds)
- **Coordinate System:** Top-left origin, Y-axis increases downward

### Visual Style
- **Theme:** Retro sci-fi with neon accents
- **Color Palette:**
  - Background: Deep space black (#0a0a12)
  - Player: Cyan glow (#00ffff) with white core (#ffffff)
  - Enemy: Red/Orange (#ff4444, #ff8800)
  - Bullets: Yellow (#ffff00) with glow effect
  - UI Text: White (#ffffff) with cyan accents
- **Effects:** 
  - Particle explosions on enemy destruction
  - Engine trail on player ship
  - Screen flash on damage

### Game Elements

#### Player Aircraft
- Triangular ship design with glowing edges
- Size: 40x50 pixels
- Engine flame animation (flickering effect)
- Position constrained to canvas bounds

#### Enemy Aircraft
- **Type A (Basic):** Small red triangular ships, move straight down
- **Type B (Zigzag):** Medium orange ships, move in sine wave pattern
- **Type C (Heavy):** Large red ships, slower movement, takes 3 hits
- Size range: 30x30 to 60x60 pixels

#### Bullets
- Player bullets: Small yellow elongated rectangles, travel upward
- Size: 4x12 pixels
- Speed: 8 pixels/frame

#### Explosions
- Particle system: 15-25 particles per explosion
- Colors: Yellow → Orange → Red gradient
- Lifetime: 30-50 frames
- Spread: Radial burst pattern

### UI Elements
- **Score:** Top-left, large font, white text
- **Lives:** Top-right, heart icons or ship silhouettes
- **Game Over Screen:** Centered overlay with final score and restart prompt
- **Start Screen:** Game title with "Press SPACE to Start" instruction

---

## 3. Game Mechanics Specification

### Player Controls
| Input | Action |
|-------|--------|
| Arrow Up / W | Move up |
| Arrow Down / S | Move down |
| Arrow Left / A | Move left |
| Arrow Right / D | Move right |
| Space | Fire bullets |
| Enter | Start/Restart game |

### Player Parameters
- Movement speed: 5 pixels/frame
- Fire rate: 1 bullet per 10 frames (6 bullets/second at 60fps)
- Starting lives: 3
- Invincibility after hit: 90 frames (1.5 seconds)

### Enemy Spawning
- Initial spawn interval: 60 frames (1 second)
- Minimum spawn interval: 20 frames
- Spawn rate increases over time (difficulty scaling)
- Random horizontal position within canvas bounds
- Enemy types distributed: 60% Type A, 30% Type B, 10% Type C

### Scoring
| Enemy Type | Points |
|------------|--------|
| Type A | 100 |
| Type B | 200 |
| Type C | 500 |

### Collision Detection
- Axis-Aligned Bounding Box (AABB) collision
- Hitboxes slightly smaller than sprites for fair gameplay

### Difficulty Progression
- Enemy spawn rate increases every 30 seconds
- Enemy speed increases by 5% every 30 seconds
- Maximum difficulty reached at 3 minutes

---

## 4. Technical Specification

### Animation
- 60 FPS target using requestAnimationFrame
- Delta time compensation for consistent speed

### Performance Optimizations
- Object pooling for bullets and particles
- Off-screen culling for all game objects
- Efficient canvas rendering (minimal state changes)

### Code Structure
```
- Constants (canvas size, colors, speeds)
- Game state object
- Entity classes (Player, Enemy, Bullet, Particle)
- Collision system
- Input handler
- Render functions
- Game loop
- UI rendering
- Initialization
```

---

## 5. Acceptance Criteria

1. ✅ Player can move in all 4 directions using arrow keys or WASD
2. ✅ Player can fire bullets using spacebar
3. ✅ Enemies spawn from top and move downward
4. ✅ Bullets destroy enemies on collision
5. ✅ Player loses life when hit by enemy or enemy bullet
6. ✅ Score increases when enemies are destroyed
7. ✅ Game over screen displays when lives reach 0
8. ✅ Game can be restarted by pressing Enter
9. ✅ Parallax background creates sense of movement
10. ✅ Explosion particles play on enemy destruction
11. ✅ Game runs smoothly at 60 FPS
12. ✅ Canvas resizes responsively with window
