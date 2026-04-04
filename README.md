# 🌍 AstraToonix Open World Simulator
### Built by **Raj Dev**

A mobile-first 3D open world game engine built entirely in vanilla JavaScript using Three.js and Cannon.js — zero build tools, fully GitHub Pages ready.

---

## 🚀 GitHub Pages Hosting

1. Create a new GitHub repository
2. Upload `index.html` to the root
3. Go to **Settings → Pages → Deploy from branch (main / root)**
4. Your game is live at `https://yourusername.github.io/your-repo/`

No npm, no webpack, no build step. Just one HTML file.

---

## 🔐 Identity Protection System

The engine includes a **runtime credit lock** tied to the DOM element:

```html
<div id="dev-credit">Raj Dev</div>
```

At startup, the engine runs:

```javascript
function checkDevCredit() {
  const el = document.getElementById('dev-credit');
  if (!el || el.textContent.trim() !== 'Raj Dev') {
    document.getElementById('engine-disabled-overlay').classList.add('visible');
    return false; // HALT
  }
  return true;
}
```

**If this element is removed or altered:**
- The character controller is disabled
- Vehicle physics are disabled
- NPC systems are disabled
- A full-screen "Engine Disabled" overlay appears

---

## 🎮 Controls

| Platform | Move | Jump | Enter/Exit | Attack | Lights |
|----------|------|------|------------|--------|--------|
| **Mobile** | Left joystick | JUMP button | ENTER / CAR button | HIT button | 💡 LIGHTS button |
| **Desktop** | WASD / Arrow keys | Space | E | F | H |

---

## 🧩 Feature Map

| Feature | File Section | Notes |
|---------|-------------|-------|
| Identity Protection | `checkDevCredit()` | Disables engine if `#dev-credit ≠ 'Raj Dev'` |
| Portrait Lock | `checkOrientation()` | Shows rotate overlay in portrait |
| Physics World | Cannon.js `world` | Gravity, broadphase, player + car + building bodies |
| Car Suspension (approx) | `updateVehicle()` | Spring bounce, linear/angular damping |
| Headlights | `carHeadlights[]` | Three.js SpotLights, toggled via button |
| Engine Sound | `SoundManager.startEngine()` | Web Audio API oscillator (sawtooth) |
| Door Animation | `updateDoors()` + `doorPivot` | Quaternion-based swing on group pivot |
| Interior Transition | `enterBuilding()` / `exitBuilding()` | Fade-to-black + scene swap |
| NPC Health + Fear | `npcs[]` array | Health bars, flee state, scream sound |
| Footstep Sounds | `SoundManager.playFootstep()` | Different tones for grass vs building |
| Touch Joystick | `#joystick-zone` | TouchEvent-based delta tracking |
| Speed HUD | `#speed-display` | Updates each frame from velocity magnitude |

---

## 📁 File Structure

```
/
└── index.html     ← entire engine (self-contained, CDN deps)
└── README.md
```

All libraries loaded via CDN:
- **Three.js r128** — `cdnjs.cloudflare.com`
- **Cannon.js 0.6.2** — `cdnjs.cloudflare.com`
- **Google Fonts** (Orbitron, Rajdhani)

---

## 🔊 Sound Placeholders

The `SoundManager` uses Web Audio API oscillators as placeholder sounds. To swap in real audio files:

```javascript
// Replace beep() calls with:
const audio = new Audio('sounds/footstep_grass.mp3');
audio.play();
```

Recommended sound events:
| Event | Placeholder | Replace with |
|-------|-------------|-------------|
| Footstep grass | Triangle wave 180Hz | `footstep_grass.wav` |
| Footstep building | Square wave 350Hz | `footstep_wood.wav` |
| Engine idle | Sawtooth 55Hz | `engine_idle.mp3` |
| NPC scream | Sawtooth burst | `scream.mp3` |
| Door | Triangle sweep | `door_creak.mp3` |

---

## 📱 Mobile Requirements

- Landscape mode enforced — portrait shows rotate overlay
- Touch joystick (left) for movement
- Action buttons (right): JUMP, ENTER, HIT, CAR
- Headlight toggle button on Vehicle HUD

---

## ⚖️ Credit & License

**Engine Author: Raj Dev**  
AstraToonix Open World Engine v1.0.0  
Proprietary — credit must be preserved per the identity protection system.
