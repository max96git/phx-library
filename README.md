# phx-library

Welcome to the PHX Library, a lightweight yet powerful library written in JavaScript, that brings the powers of Three.js, CANNON.js, and Babylon.js into a coherent framework of 3D rendering, physics, and interactivity.
Introduction

PHX simplifies your work while building 3D web experiences by providing functionality that's responsible for the rendering, physics, scene management, and interaction. Due to PHX, the developer will not have any problem creating complex immersive 3D scenes in a very intuitive and user-friendly way. Supported Features

- **Rendering**: Advanced scene graph, cameras, materials, and lights.
- **Physics**: Rigid body dynamics, collision detection, and constraints.
- **Advanced Interaction**: Particle systems, GUI, VR/AR support, and more.
- **Modular and Lightweight**: Designed for flexibility and scalability.
  
# Documentation
## Getting Started
### Installation

Download the minified library from `phx.min.js`.
Include it in your project:

`<script src="phx.min.js"></script>`

## Basic Usage
### Setup

Create a scene, a camera, and a renderer:

`const scene = new PHX.Scene();
const camera = new PHX.Camera({
fov: 75,
aspect: window.innerWidth / window.innerHeight,
near: 0.1,
far: 1000
});
const renderer = new PHX.Renderer({ antialias: true });
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);`

### Add a Mesh

Add a cube to the scene:

`const cube = new PHX.Mesh(
new PHX.BoxGeometry(1, 1, 1),
new PHX.Material({ color: 0x00ff00 })
);
scene.add(cube);`

### Physics Integration

Create a physics world and add a rigid body:

`const physicsWorld = new PHX.PhysicsWorld({ gravity: [0, -9.8, 0] });
const rigidBody = new PHX.RigidBody({
mass: 1,
shape: "box",
position: [0, 5, 0]
});
physicsWorld.addBody(rigidBody);`

### Animation Loop

Render the scene and update physics:

`function animate() {
requestAnimationFrame(animate);
physicsWorld.step(1 / 60); // Physics timestep
renderer.render(scene, camera);
}
animate();`

## API Reference
### Core Classes
**PHX.Scene**
- A 3D scene, holding objects, lights, and cameras.
- **Methods**:
  - `add(object)`: Adds an object to the scene.

**PHX.Camera**

- Creates a camera to view a scene.
- **Parameters:**
`fov` (number): Field of view in degrees.
`aspect` (number): Aspect ratio of the camera.
`near` (number): Near clipping plane.
`far` (number): Far clipping plane.

**PHX.Renderer**

- Renders the scene onto a WebGL canvas.
- **Methods:**
  - `setSize(width, height)`: Set the size of the rendering canvas.
  - `render(scene, camera)`: Renders the given scene using the specified camera.

**PHX.Mesh**

- Combine geometry and material into renderable objects.
- **Parameters:**
  - `geometry`: A geometry object, such as `PHX.BoxGeometry`.
  - `material`: An object of type Material. Example: `PHX.Material`.

**PHX.BoxGeometry**

- Creates a box-like geometry.
- **Parameters:**
  - `width` (number): Width of the box.
  - `height` (number): Height of the box.
  - `depth` (number): Depth of the box.

**PHX.Material**

- Creates a simple material.
- **Parameters:**
  - `color` (hex): Material color.

## Physics Classes
**PHX.PhysicsWorld**

- A wrapper class representing a physics simulation.
- **Methods:**
  - `addBody(body)`: Adds a rigid body to the physics world.
  - `step(timeStep)`: Advances the simulation ahead by the given timestep.

**PHX.RigidBody**

- Represents a physical object.
- **Parameters:**
  - `mass` (number) - Mass of the object
  - `shape` (string) - Shape type ex: "box", "sphere"
  - `position` (array) - Initial position of the object [x, y, z]

## Advanced Features
**Particles**

Create a particle system:

`const particles = new PHX.ParticleSystem({
count: 1000,
color: 0xffffff
});
scene.add(particles);`

**Lighting**

Add lighting to your scene:

`const light = new PHX.Light({ type: "point", color: 0xffffff, intensity: 1 });
scene.add(light);`

**Interactive Camera**

Enable the user to move the camera around in the scene:

`const controls = new PHX.CameraControls(camera, renderer.domElement);`

## Examples
### 1. Basic Cube

`const scene = new PHX.Scene();
const camera = new PHX.Camera({ fov: 75, aspect: window.innerWidth / window.innerHeight, near: 0.1, far: 1000 });
const renderer = new PHX.Renderer({ antialias: true });
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

const cube = new PHX.Mesh(new PHX.BoxGeometry(1, 1, 1), new PHX.Material({ color: 0x00ff00 }));
scene.add(cube);

function animate() {
requestAnimationFrame(animate);
renderer.render(scene, camera);
}
animate();`

### 2. Physics Simulation

`const scene = new PHX.Scene();
const physicsWorld = new PHX.PhysicsWorld({ gravity: [0, -9.8, 0] });

const box = new PHX.Mesh(new PHX.BoxGeometry(1, 1, 1), new PHX.Material({ color: 0xff0000 }));
scene.add(box);

const body = new PHX.RigidBody({ mass: 1, shape: "box", position: [0, 5, 0] });
physicsWorld.addBody(body);

function animate() {
requestAnimationFrame(animate);
physicsWorld.step(1 / 60);
renderer.render(scene, camera);
}`
