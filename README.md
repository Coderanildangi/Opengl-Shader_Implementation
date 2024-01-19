# OpenGL Visualizer with Shaders

## Overview

This repository contains a simple OpenGL visualizer implemented in C++ using the Qt framework. The application enables the visualization of geometric shapes and curves, allowing users to interactively add points, lines, polygons, and curves. Shaders are employed for rendering, providing flexibility and customization in defining the visual appearance of the rendered objects.

## Shaders

The shaders used in this project are written in GLSL (OpenGL Shading Language) and control the visual appearance of the rendered objects. The following shaders are included in the project:

### Vertex Shader (`vertexShader.glsl`)

Handles the transformation of vertex positions. It reads vertex positions and colors from the buffers and passes data to the fragment shader.

``glsl

attribute highp vec4 posAttr;
attribute lowp vec4 colAttr;
varying lowp vec4 col;
uniform highp mat4 matrix;
uniform float time;

void main() {
    col = colAttr;
    float scaleSpeed = 0.5;
    float scaleFactor = 1.0 + scaleSpeed * sin(time * scaleSpeed);
    vec4 scaledPosition = posAttr * vec4(scaleFactor, scaleFactor, 1.0, 1.0);
    gl_Position = matrix * scaledPosition;
}

### Fragment Shader (fragmentShader.glsl)

Controls the color of each pixel, utilizing varying variables to receive data from the vertex shader. It can be dynamically updated to change the rendering appearance.

``glsl

varying lowp vec4 col;

void main() {
    gl_FragColor = col;
}

## Usage

### Building and Running:

- Ensure you have the necessary dependencies installed.
- Build the project using a C++ compiler.
- Run the executable.


### User Interface:

- The UI allows users to add points, lines, polygons, and curves.
- Region and polygon clipping functionalities are available.
- Users can interactively change the color of the rendered shapes.

### Shaders:

- The shaders (vertexShader.glsl and fragmentShader.glsl) can be modified to customize the rendering.
- Use the setColor method in the OpenGLWindow class to dynamically change the fragment shader color.

``cpp

void OpenGLWindow::setColor(const QString& text, const QString& filePath) {
    // Code to update the fragment shader with the provided color text.
}

## Notes

- This application uses Qt for GUI and OpenGL for rendering.
- Shaders play a crucial role in defining the visual appearance of rendered shapes.