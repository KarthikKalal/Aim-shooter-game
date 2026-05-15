

# Aim-shooter-game
# 🎯 AIMFORGE — Futuristic 3D Aim Trainer


<img width="1200" height="900" alt="592929950-dc880052-53e4-4c0c-a306-747ba63b7ecc" src="https://github.com/user-attachments/assets/ba056d92-493e-405e-8aeb-cc07f2a56008" />


https://github.com/user-attachments/assets/484056aa-7fbf-4e45-89df-f1e8fb67f35e














---

# 🚀 Overview

**AIMFORGE** is a futuristic cyberpunk-inspired 3D aim trainer built using **Three.js**, designed to improve:

- 🎯 Precision
- ⚡ Reflex
- 🧠 Tracking
- 🔥 Flick shots
- 🚀 Speed aiming

Inspired by professional FPS aim trainers with immersive neon aesthetics and high-performance gameplay.

---

# 🖼️ Features

| Feature | Description |
|---|---|
| 🎯 Gridshot | Multiple fast targets |
| ⚡ Flick Shot | Single reaction target |
| 👁 Tracking | Follow moving targets |
| 🔥 Reflex Mode | Random spawn timing |
| 🚀 Speed Training | Small rapid targets |
| 📊 Session Stats | Accuracy & combo tracking |
| 🌌 3D Environment | Neon cyberpunk room |
| ✨ Particle Effects | Dynamic glowing particles |
| 🎮 Smooth Crosshair | Responsive FPS feel |

---

# 📂 Project Structure

```bash
AIMFORGE/
│
├── index.html
├── game.html
├── stats.html
│
├── css/
│   ├── style.css
│   ├── game.css
│   └── ui.css
│
├── js/
│   ├── main.js
│   ├── targets.js
│   ├── particles.js
│   ├── score.js
│   └── settings.js
│
├── assets/
│   ├── sounds/
│   ├── textures/
│   └── models/
│
└── README.md
```

---

# 🎨 Cyberpunk UI Style

```css
body {
  margin: 0;
  overflow: hidden;
  background: radial-gradient(circle, #090014, #02030a);
  color: white;
  font-family: 'Orbitron', sans-serif;
}

button {
  background: #00d9ff;
  border: none;
  padding: 14px 28px;
  color: black;
  font-weight: bold;
  border-radius: 10px;
  cursor: pointer;
  transition: 0.3s;
}

button:hover {
  transform: scale(1.05);
  box-shadow: 0 0 20px #00d9ff;
}
```

---

# 🎯 Aim Trainer Menu UI

```html
<div class="menu">

  <h1>AIMFORGE</h1>

  <div class="modes">

    <button>Gridshot</button>
    <button>Flick Shot</button>
    <button>Tracking</button>
    <button>Reflex</button>
    <button>Speed</button>

  </div>

  <button class="start">
    START TRAINING
  </button>

</div>
```

---

# 🌌 Three.js Scene Setup

```javascript
import * as THREE from 'three';

const scene = new THREE.Scene();

scene.fog = new THREE.Fog(0x000000, 10, 80);

const camera = new THREE.PerspectiveCamera(
  75,
  window.innerWidth / window.innerHeight,
  0.1,
  1000
);

camera.position.z = 10;

const renderer = new THREE.WebGLRenderer({
  antialias: true
});

renderer.setSize(
  window.innerWidth,
  window.innerHeight
);

document.body.appendChild(renderer.domElement);
```

---

# 💡 Neon Lighting

```javascript
const light1 = new THREE.PointLight(0x00ffff, 5);
light1.position.set(-10, 10, 10);

const light2 = new THREE.PointLight(0xff00ff, 5);
light2.position.set(10, 10, 10);

scene.add(light1, light2);
```

---

# 🎯 Target Creation

```javascript
const geometry = new THREE.SphereGeometry(0.5, 32, 32);

const material = new THREE.MeshStandardMaterial({
  color: 0x00ffff,
  emissive: 0x00ffff,
  emissiveIntensity: 2
});

const target = new THREE.Mesh(
  geometry,
  material
);

scene.add(target);
```

---

# 🖱 Mouse Aim Detection

```javascript
window.addEventListener('click', shoot);

function shoot(event) {

  const mouse = new THREE.Vector2();

  mouse.x = (event.clientX / window.innerWidth) * 2 - 1;

  mouse.y = -(event.clientY / window.innerHeight) * 2 + 1;

  const raycaster = new THREE.Raycaster();

  raycaster.setFromCamera(mouse, camera);

  const hits = raycaster.intersectObjects(scene.children);

  if (hits.length > 0) {

    score++;

    console.log('Target Hit');
  }
}
```

---

# ✨ Particle Background

```javascript
const particlesGeometry = new THREE.BufferGeometry();

const particlesCount = 500;

const positions = new Float32Array(
  particlesCount * 3
);

for (let i = 0; i < particlesCount * 3; i++) {
  positions[i] = (Math.random() - 0.5) * 100;
}

particlesGeometry.setAttribute(
  'position',
  new THREE.BufferAttribute(positions, 3)
);

const particlesMaterial = new THREE.PointsMaterial({
  size: 0.1,
  color: 0x00ffff
});

const particles = new THREE.Points(
  particlesGeometry,
  particlesMaterial
);

scene.add(particles);
```

---

# 🎮 Crosshair UI

```html
<div class="crosshair"></div>
```

```css
.crosshair {
  position: fixed;
  top: 50%;
  left: 50%;
  width: 20px;
  height: 20px;
  transform: translate(-50%, -50%);
  pointer-events: none;
}

.crosshair::before,
.crosshair::after {
  content: '';
  position: absolute;
  background: cyan;
}

.crosshair::before {
  width: 2px;
  height: 20px;
  left: 9px;
}

.crosshair::after {
  width: 20px;
  height: 2px;
  top: 9px;
}
```

---

# 📊 Session Result Screen

```html
<div class="results">

  <h1>SESSION COMPLETE</h1>

  <div class="stats">

    <div class="card">
      <h2>3945</h2>
      <p>FINAL SCORE</p>
    </div>

    <div class="card">
      <h2>91%</h2>
      <p>ACCURACY</p>
    </div>

    <div class="card">
      <h2>17x</h2>
      <p>MAX COMBO</p>
    </div>

  </div>

</div>
```

---

# ⚙️ Settings Menu

```javascript
const settings = {
  duration: 30,
  targetColor: 'cyan',
  sensitivity: 1.0
};
```

---

# 🔥 Animation Loop

```javascript
function animate() {

  requestAnimationFrame(animate);

  particles.rotation.y += 0.0005;

  renderer.render(scene, camera);
}

animate();
```

---

# 📦 Installation
https://claude.ai/public/artifacts/7c64104d-9283-4a0b-a867-5e4a9709931c

```bash
