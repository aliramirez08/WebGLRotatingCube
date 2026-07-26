# WebGL Rotating Cube

This project was developed to strengthen my understanding of 3D graphics programming with WebGL and JavaScript. It renders a colored three-dimensional cube directly in the browser and continuously rotates it around the X and Y axes.

The project creates the cube from vertex, color, and index data. Custom vertex and fragment shaders transform and color the geometry, while the glMatrix library provides the matrix operations needed for perspective projection, positioning, and rotation.

## Features

- Renders a three-dimensional cube with WebGL
- Builds cube geometry from vertices and triangle indices
- Assigns a different color to each vertex
- Interpolates colors across the cube’s surfaces
- Uses custom vertex and fragment shaders
- Applies perspective projection
- Rotates the cube around the X and Y axes
- Uses depth testing for correct face visibility
- Animates with `requestAnimationFrame`
- Checks for WebGL initialization and shader errors
- Runs directly in a compatible web browser

## Concepts Demonstrated

- WebGL
- 3D computer graphics
- Vertex buffers
- Color buffers
- Index buffers
- Vertex shaders
- Fragment shaders
- GLSL
- Triangle-based geometry
- Perspective projection
- Model-view transformations
- Matrix operations
- Depth testing
- Indexed drawing
- Color interpolation
- Browser animation loops

## Technologies Used

- HTML5
- JavaScript
- WebGL
- GLSL
- glMatrix 2.8.1
- Visual Studio Code
- Live Server
- Git
- GitHub

## Project Structure

```text
WebGLRotatingCube/
├── Screenshots/
│   ├── LiveServer.png
│   └── RotatingCubeDemo.mov
├── index.html
├── cube.js
├── README.md
└── .gitignore
```

- `index.html` – Creates the canvas and loads the required scripts
- `cube.js` – WebGL setup, geometry, shaders, transformations, and animation
- `Screenshots/LiveServer.png` – Demonstrates launching the project with Live Server
- `.gitignore` – Excludes editor and operating-system files
- `README.md` – Project documentation

## How to Run

### Prerequisites

- A modern browser with WebGL support
- An internet connection to load the glMatrix library
- Visual Studio Code with the Live Server extension recommended

### Steps

1. Clone the repository:

```bash
git clone https://github.com/aliramirez08/WebGLRotatingCube.git
```

2. Navigate to the project directory:

```bash
cd WebGLRotatingCube
```

3. Open the project in Visual Studio Code:

```bash
code .
```

4. Right-click `index.html`.

5. Select **Open with Live Server**.

The project will open in the default browser and display the rotating cube.

You can also open `index.html` directly in a browser, although running it through a local development server is recommended.

## Code Examples

### WebGL Initialization

```javascript
const canvas = document.getElementById("glcanvas");
const gl = canvas.getContext("webgl");

if (!gl) {
    alert("Unable to initialize WebGL.");
} else {
    console.log("WebGL initialized successfully.");
}
```

The program retrieves the canvas element and requests a WebGL rendering context.

### Cube Vertices

```javascript
const vertices = [
    -1.0, -1.0,  1.0,
     1.0, -1.0,  1.0,
     1.0,  1.0,  1.0,
    -1.0,  1.0,  1.0,
    -1.0, -1.0, -1.0,
     1.0, -1.0, -1.0,
     1.0,  1.0, -1.0,
    -1.0,  1.0, -1.0
];
```

The cube is defined by eight vertices representing its corners in three-dimensional space.

### Triangle Indices

```javascript
const indices = [
    0, 1, 2,  0, 2, 3,
    4, 5, 6,  4, 6, 7,
    0, 1, 5,  0, 5, 4,
    3, 2, 6,  3, 6, 7,
    0, 4, 7,  0, 7, 3,
    1, 5, 6,  1, 6, 2
];
```

Each group of three indices defines one triangle. Two triangles form each face of the cube.

### Vertex Shader

```glsl
attribute vec3 aVertexPosition;
attribute vec3 aVertexColor;

uniform mat4 uModelViewMatrix;
uniform mat4 uProjectionMatrix;

varying lowp vec3 vColor;

void main(void) {
    gl_Position =
        uProjectionMatrix *
        uModelViewMatrix *
        vec4(aVertexPosition, 1.0);

    vColor = aVertexColor;
}
```

The vertex shader transforms each vertex from model coordinates into clip space and passes its color to the fragment shader.

### Fragment Shader

```glsl
varying lowp vec3 vColor;

void main(void) {
    gl_FragColor = vec4(vColor, 1.0);
}
```

The fragment shader assigns the interpolated vertex color to each rendered pixel.

### Cube Transformations

```javascript
mat4.translate(
    modelViewMatrix,
    modelViewMatrix,
    [0, 0, -6]
);

mat4.rotate(
    modelViewMatrix,
    modelViewMatrix,
    cubeRotation,
    [0, 1, 0]
);

mat4.rotate(
    modelViewMatrix,
    modelViewMatrix,
    cubeRotation * 0.7,
    [1, 0, 0]
);
```

The cube is moved away from the camera and rotated around both the Y and X axes.

### Animation Loop

```javascript
function render(now) {
    now *= 0.001;
    cubeRotation += 0.01;

    drawScene();
    requestAnimationFrame(render);
}

requestAnimationFrame(render);
```

`requestAnimationFrame` repeatedly calls the render function, allowing the browser to update the rotating cube efficiently.

## What I Learned

This project strengthened my understanding of how WebGL renders three-dimensional geometry from buffers and triangles. I learned how vertex positions, colors, and indices are uploaded to the graphics processor and connected to shader attributes.

Writing vertex and fragment shaders helped me understand how vertices are transformed and how colors are calculated across a surface. I also learned how projection and model-view matrices position a 3D object within a scene.

Implementing depth testing and a browser animation loop helped me understand how WebGL maintains correct face visibility and continuously redraws an animated scene.

## Future Improvements

- Make rotation speed independent of frame rate
- Resize the canvas responsively
- Add mouse controls for rotating the cube
- Add zoom controls
- Allow the user to pause and resume animation
- Add controls for rotation speed
- Add lighting and surface normals
- Apply textures to the cube faces
- Add additional 3D objects
- Move shader code into separate files
- Display shader errors in the page
- Host the project with GitHub Pages
- Add a screenshot or GIF showing the rendered cube

## Screenshots

### Launching with Live Server

![Launching with Live Server](Screenshots/LiveServer.png)

## Demo Video

Watch the rotating cube demonstration:

[View Rotating Cube Demo](Screenshots/RotatingCubeDemo.mov)