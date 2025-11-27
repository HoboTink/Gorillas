# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Gorillas** is a modern browser-based recreation of the classic MS-DOS Gorillas game. It features two versions:
- **3D Edition** (Gorillas3D.html): Full 3D rendering with Three.js, free-rotating camera, dynamic lighting, and particle effects
- **2D Edition** (Gorillas3DProject.html): Classic retro experience with simple 2D canvas rendering

The project is deployed on **GitHub Pages** at `https://hobotink.github.io/Gorillas/` with automatic deployment on push to main.

## Architecture

### Game Structure
The game consists of three main HTML files, each self-contained with inline JavaScript and CSS (no build process required):

1. **index.html** - Landing page with game version selector
   - Pure HTML/CSS/JS with no dependencies
   - Responsive grid layout showing both game versions
   - Links to play either 3D or 2D version

2. **Gorillas3D.html** - Modern 3D version
   - Uses **Three.js** (loaded via CDN: `https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js`)
   - Single `Gorillas3D` class handles all game logic, rendering, physics, and controls
   - Modular methods for: scene setup, lighting, environment, city generation, gorilla creation, physics simulation, collision detection, camera controls, UI updates

3. **Gorillas3DProject.html** - Classic 2D version
   - Pure HTML5 Canvas 2D rendering
   - Procedurally generated 2D buildings
   - Simple physics simulation with wind effects

### Key Design Patterns

**3D Version Class Structure:**
- Single class (`Gorillas3D`) encapsulates all functionality
- State management via `gameState` object: `{ currentPlayer, score, wind, isAnimating, banana }`
- Camera control via `cameraControl` object with rotation (x, y, z), zoom, and pan properties
- Physics constants: gravity (9.81) and wind force (0.5)

**Game Loop:**
- Uses `requestAnimationFrame()` for smooth 60fps rendering
- Physics updates happen during animation frames
- Collision detection runs every frame for banana trajectory

**Controls (3D Version - Optimized for MacBook Trackpad):**
- Drag: Orbit camera (rotation around x and y axes)
- Shift + Drag: Tilt/roll camera (rotation around z axis)
- Scroll: Zoom in/out
- WASD: Pan camera in x/y directions
- Space: Reset camera to default position

## Development Workflow

### Local Testing
```bash
# Open landing page (game selector)
open index.html

# Or test specific version directly
open Gorillas3D.html      # 3D version
open Gorillas3DProject.html  # 2D version
```

### Deployment
- **Automatic**: Push to `main` branch triggers GitHub Pages deployment (files in root are served)
- **Manual**: Visit repo settings > Pages section to check deployment status
- **Verify**: Check `https://hobotink.github.io/Gorillas/` after 1-2 minutes

### Git Workflow
```bash
git add <file>
git commit -m "Your message"
git push origin main
```

Note: GitHub Personal Access Token with `repo` scope is configured. PAT with `workflow` scope is needed only for GitHub Actions workflows.

## Common Development Tasks

### Adding New Features
1. **UI Changes**: Edit inline CSS in `<style>` tags
2. **Game Logic**: Modify methods in the game class (e.g., `throwBanana()`, `updateBanana()`)
3. **Physics**: Adjust constants in physics object (gravity, windForce) or update in `gameLoop()`
4. **Controls**: Add/modify event listeners in `setupControls()` and handlers like `onMouseMove()`, `onKeyDown()`

### Fixing Issues
1. **Camera Problems**: Debug in `updateCameraPosition()` and rotation limit checks in `onMouseMove()`
2. **Collision Detection**: Check `checkBuildingCollision()` and `checkGorilllaCollision()` (note: typo "Gorilllla" in method name)
3. **Physics Issues**: Verify in `updateBanana()` - wind application, gravity, velocity updates
4. **Building Generation**: Adjust `generateCity()` parameters (width range, height range, spacing)
5. **Rendering Issues**: Check `setupLighting()`, `setupEnvironment()`, material properties in `createBuilding()`

### Testing New Changes
- Always test locally first: `open Gorillas3D.html`
- Test both 2D and 3D versions if changes affect shared logic
- Verify on mobile/different browsers before pushing
- Check GitHub Pages deployment after push (may take 1-2 minutes)

## Known Quirks & Considerations

- **Typo in Code**: Method `checkGorilllaCollision()` has three 'l's (not a bug, just a naming quirk)
- **Building Positioning**: Buildings are positioned with `y = height/2 - 50` to sit on ground (y=0)
- **Gorilla Height**: Gorillas are placed at `building.position.y + (height/2) + 20` to stand on building tops
- **Physics Scale**: Banana velocity is multiplied by 1.5 in 2D version for better feel on canvas scale
- **Camera Limits**: Rotation.x limited to ±π/2.2 to prevent gimbal lock issues
- **Tilt Limit**: Rotation.z (tilt) limited to ±π/4 (45 degrees) to prevent disorientation

## Dependencies

### External Libraries
- **Three.js r128** - 3D graphics library (CDN: `cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js`)
- No other dependencies - pure vanilla JavaScript elsewhere

### Browser APIs Used
- WebGL (via Three.js)
- Canvas 2D API
- requestAnimationFrame
- Mouse/Touch events
- Keyboard events

## Performance Considerations

- **3D Version**: Uses WebGL with shadow mapping enabled - may impact performance on older devices
- **Particle Effects**: Limited to 20 particles per explosion, auto-removed after 500ms
- **Camera Rotation Limits**: Prevents gimbal lock and unnecessary computations
- **No Build Process**: Files served directly - no minification, consider adding for production optimization

## Recent Improvements (Latest Session)

### Visual & Physics Enhancements (Commit: 51a4c4e)
- **Banana physics**: Added realistic spin/rotation as banana flies
- **Rotation drag**: Spinning slows over time for natural motion
- **Screen shake**: Camera shakes on impact (200ms duration) for feedback
- **Enhanced explosions**: 35+ colorful particles with realistic gravity and fade-out
- **Banana trails**: Yellow particles follow banana path during flight
- **Glowing banana**: Added emissive glow to banana material for visibility
- **Better delta time**: Improved physics calculations for smoother feel

### Trackpad Optimization (Commit: b6c9313)
- Changed tilt control from right-click to **Shift + Drag** for MacBook trackpad compatibility
- All controls now work seamlessly on trackpad

### Camera & Positioning Fixes (Commits: 642c7f7, 1c3dd3b)
- Fixed buildings floating in air - now sit on ground properly
- Gorillas positioned correctly on building tops
- Expanded camera rotation limits to allow looking straight down
- Added tilt/roll control for full 3D perspective

### Documentation (Commit: c4239b9)
- Added comprehensive CLAUDE.md for future development sessions

## Future Enhancement Ideas

**High Priority (Next Session Ideas):**
- Add sound effects (throw sound, explosion, hit/miss)
- Implement difficulty levels (wind intensity, gravity variation)
- Add visual trajectory preview before throwing
- Implement power meter for throw visualization
- Add more gorilla animations (throw pose, celebration)

**Medium Priority:**
- Add leaderboard/score tracking (localStorage)
- Create mobile-optimized controls (touch gestures)
- Add more 3D visual polish (skybox, building textures, better materials)
- Implement wind visualization (wind direction particles)
- Create level/map variety with different city layouts

**Lower Priority:**
- Add replay mode functionality
- Implement multiplayer (if hosting becomes available)
- Add achievements/badges system
- Create game modes (timed, endless, tournament)

## Browser Compatibility

- **Minimum Requirements**: WebGL support (Three.js r128)
- **Tested On**: Chrome/Edge 60+, Firefox 55+, Safari 12+
- **Device**: Optimized for MacBook trackpad (Shift+drag for tilt)
- **Responsive**: CSS uses viewport units and flexbox for mobile adaptation
