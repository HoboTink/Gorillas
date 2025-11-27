# Gorillas - Banana Toss Game

A modern recreation of the classic MS-DOS Gorillas game with both 2D and 3D versions playable directly in your browser.

## Play Now

**[🎮 Play the Game](https://hobotink.github.io/Gorillas/)**

Choose between:
- **3D Edition**: Modern 3D rendering with Three.js, free camera controls, and dynamic lighting
- **2D Edition**: Classic retro experience with simple controls

## Features

### 3D Version (Modern)
- Full 3D rendering with Three.js and WebGL
- Free-rotating camera with mouse and keyboard controls
- Dynamic lighting system with shadows
- Procedurally generated 3D cityscape
- Physics-based banana trajectories
- Particle explosion effects
- Modern UI with animations

### 2D Version (Classic)
- Clean 2D canvas rendering
- Retro MS-DOS inspired aesthetics
- Simple angle and velocity controls
- Wind effect simulation
- Building collision detection
- Responsive controls

## How to Play

1. Set the throw **angle** (0-180°) and **power** (20-200)
2. Click **THROW** to launch the banana
3. Try to hit the opponent gorilla across the city
4. Wind affects the banana trajectory
5. Take turns until someone scores!

## Controls

### 3D Version
- **Mouse Drag**: Rotate camera
- **Scroll Wheel**: Zoom in/out
- **WASD Keys**: Pan camera
- **Spacebar**: Reset camera

### 2D Version
- **Angle Input**: Set throw angle
- **Velocity Input**: Set throw power
- **THROW Button**: Fire the banana

## Technical Stack

- **Three.js**: 3D graphics and WebGL rendering
- **Vanilla JavaScript**: Game logic and physics
- **HTML5**: Semantic structure
- **CSS3**: Modern styling and animations
- **GitHub Pages**: Hosting and deployment

## Development

### Local Testing
```bash
# Clone the repository
git clone https://github.com/HoboTink/Gorillas.git
cd Gorillas

# Open in browser (macOS)
open index.html

# Or open Gorillas3D.html for 3D version
open Gorillas3D.html

# Or open Gorillas3DProject.html for 2D version
open Gorillas3DProject.html
```

## Project Structure

```
Gorillas/
├── index.html                 # Game selector / landing page
├── Gorillas3D.html           # Modern 3D version
├── Gorillas3DProject.html    # Classic 2D version
├── README.md                 # This file
├── .gitignore               # Git ignore rules
└── .github/
    └── workflows/
        └── deploy.yml       # GitHub Pages deployment
```

## Browser Support

- Chrome/Edge 60+
- Firefox 55+
- Safari 12+
- Any modern browser with WebGL support

## License

MIT License - Feel free to fork, modify, and share!

## Credits

Recreation of the classic Gorillas game originally by IBM (1991).

---

**Built with modern web standards and best practices.**
