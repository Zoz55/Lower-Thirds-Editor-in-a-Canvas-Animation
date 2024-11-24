
# Lower Thirds Editor in a Canvas Animation

The **Lower Thirds Editor in a Canvas Animation** is a free dock plugin designed for use with OBS Studio. It allows users for creating, editing, and animating visual elements like shapes, text, and images on a canvas. Built using **fabricJS** and **GSAP**, it provides dynamic customization, precise controls, and powerful animation features for **lines**, **circles**, **capsules**, **rounded rectangles**, **polygons**, **images**, **textboxes**, and more.

It consists of three main components:

1. **Animation Viewer (`canvas.html`)**: Displays animated visual elements as a `Browser Source page`.
2. **Control Panel (`control_panel.html`)**: Provides control buttons for starting, stopping, and reversing animations, as a `dock page`.
3. **Canvas Editor (`canvas_editor.html`)**: The Canvas Editor is an advanced tool designed for creating, editing, and animating visual content. It is tailored for designers, developers, and creators who need a highly customizable and interactive environment for crafting dynamic graphics and animations.

**fabricJS**, the core library powering the Canvas Editor, provides robust support for handling SVG files, including those enriched with custom data attributes. These attributes are seamlessly stored in the JSON representation of the canvas, ensuring that all customizations, metadata, and animation settings are preserved. Users can save their work as JSON files and reopen them later, allowing for a smooth workflow and efficient reuse of designs. This capability makes the Canvas Editor a powerful solution for projects requiring precise data management and reusability.

---

## Installation

### Prerequisites
- A local web server.
- A modern browser supporting **ES6 features**.

### Steps
1. Download the repository (via Git or ZIP) and extract the ZIP file to your desired location.
2. Open OBS
3. Add a new Browser Source in your scene and point the browser source to the `canvas.html` (e.g., `http://lower-thirds-editor/canvas.html`).
4. Add `control_panel.html` as a dock page to perform start animation and reverse animation actions (e.g., `http://lower-thirds-editor/control_panel.html`).
5. Open your browser
6. Add the `canvas_editor.html` in your browser to edit new or existing JSON files (e.g., `http://lower-thirds-editor/canvas_editor.html`).

---

## Dependencies

The editor uses libraries and `.ttf` fonts that have been downloaded locally, allowing it to function offline without requiring an internet connection.

1. **[fabricJS](http://fabricjs.com/)** - For rendering and manipulating objects on the canvas.
   - **CDN**: `<script src="https://cdnjs.cloudflare.com/ajax/libs/fabric.js/5.2.4/fabric.min.js"></script>`
   
2. **[GSAP](https://greensock.com/gsap/)** - For smooth animations on the canvas.
   - **CDN**: `<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.9.1/gsap.min.js"></script>`

3. **[Polygon Maker](https://github.com/ManolisMariakakis/Clip-path-Maker-by-Drag-Drop)** - For polygon design.

4. **[LC-color-picker.js](https://github.com/LCweb-ita/LC-color-picker)** - Color picker updated for custom needs.

5. **BroadcastChannel API** - For communication between the control panel (`control_panel.html`) and canvas (`canvas.html`).

---

## The **Canvas Editor (`canvas_editor.html`)**

An interactive canvas editor that allows users to dynamically add, move, resize, rotate, delete, and animate objects. The canvas supports exporting designs as JSON or PNG files and reloading saved designs for further editing.

### Adding Objects
- **Line**: Add and customize stroke, width, and dash patterns.
- **Circle**: Adjust diameter, colors, and gradients.
- **Capsule**: Control radii, angle, and line length.
- **Rounded Rectangle**: Customize dimensions, corner radius, and border styles.
- **Polygon**: Add, edit, and adjust vertices dynamically.
- **Image**: Upload and edit brightness, contrast, and color channels.
- **Textbox**: Style text with fonts, alignment, spacing, and effects.

### Animation Features

- **Duration**: Specify the animation length.
- **Delay**: Add a delay before the animation starts.
- **Easing**: Choose from various easing options.
- **Properties**: Animate starting position, scaling, opacity, and rotation.

### Save & Load

- **Save as JSON**: Export the canvas design for future editing.
- **Save as PNG**: Export the canvas as a high-quality PNG image.
- **Load JSON**: Load an existing JSON file to continue editing.
- **Load JSON files from `fontnames.txt`**: Load JSON files listed in the configuration file (`fontnames.txt`) for editing.

### Font Management for Textbox Canvas Objects

To ensure that the editor works offline, you'll need to manage the font families using local font files. The editor allows users to select a font family for each Textbox. The font families available are managed through a configuration file and the corresponding font files on the system.

- The list of selectable font families is stored in the `fontnames.txt` file located in the `fonts` folder.
- Each line in `fontnames.txt` represents the name of a font family.
- For each font family added to `fontnames.txt`, ensure the corresponding `.ttf` files are installed on the operating system.
- If you want to use the font families listed in the sample `fontnames.txt` file, you need to install the `ttf.zip` files on your operating system.
- All `.ttf` files of `ttf.zip` have been downloaded from [fonts.google.com](https://fonts.google.com).

The image below shows the editor interface with a toolbar for editing options, a canvas settings panel on the left and a central canvas workspace displaying customizable text and decorative elements.

![image](https://github.com/ManolisMariakakis/Lower-Thirds-Editor-in-a-Canvas-Animation/blob/main/editor.png)

---

## The **Control Panel (`control_panel.html`)**

The control panel enables users to manage JSON files, allowing actions such as animating, and reversing animations.

### Features
1. **Dynamic JSON List**: Displays a list of JSON file names retrieved from the text file (`jsonfiles.txt`). You can control as many files as exist as entries in the JSON file (`jsonfiles.txt`).
2.  **Animation Buttons**:
   
    - **Animate**: Sends a broadcast message to animate the associated JSON file.
    - **Reverse Actions**: Sends a broadcast message to reverse animate with specific actions like `Reverse Animate`, `Reverse Outside-Left`, etc.

3. **BroadcastChannel Integration**: Uses the `BroadcastChannel` API for real-time communication between `control_panel.html` and `canvas.html`.

### How It Works
1. **Loading JSON Files**:
   - The `control_panel.html` page fetches file names from `jsonfiles/jsonfiles.txt`.
   - Each file name is displayed in a structured list with corresponding action buttons.

2. **Animation and Reverse Actions**:
   - The "Animate" button sends a broadcast message to perform animation on the selected JSON file.
   - Reverse actions are also initiated via broadcast messages, allowing animations to be played in reverse.

3. **BroadcastChannel Communication**:
   - Sends messages with JSON file names and action types.
   - Listens for messages to update the button states dynamically.

### Example `jsonfiles.txt` Format

```plaintext
file1.json
file2.json
file3.json
```
The image below displays the control panel interface with rows corresponding to JSON file names and columns for animation actions. Each row represents a JSON file (e.g., sample1.json, sample2.json, sample3.json), and each column contains buttons for triggering specific animation-related actions like "Animate Action," "Reverse Animate," and directional animation reversals ("Reverse Outside-Left," "Reverse Outside-Bottom," "Reverse Outside-Right," "Reverse Fade-Out"). The buttons are styled with icons indicating play or reverse actions for easy identification.

![image](https://github.com/ManolisMariakakis/Lower-Thirds-Editor-in-a-Canvas-Animation/blob/main/panel.png)

## The **Animation Viewer (`canvas.html`)**

Animation Viewer is an animation system for JSON data on an HTML canvas. It leverages **fabricJS** for canvas rendering and **GSAP** for animations. The animations are controlled using broadcast messages, and the canvas updates dynamically based on the provided JSON configuration.

### Features
1. **Dynamic Canvas Initialization**:
   - The canvas dimensions and objects are loaded dynamically from JSON files.
2. **BroadcastChannel Communication**:
   - Inter-tab communication is achieved using the `BroadcastChannel` API.
3. **GSAP Animations**:
   - Animations include entrance, reverse, and various directional effects.
4. **Custom Metadata Support**:
   - Objects have custom metadata attributes like `data-duration`, `data-delay`, `data-position`, etc.
5. **Concurrent Animations**:
   - Multiple canvas objects animate concurrently for seamless effects.
6. **Dynamic Reverse Animations**:
   - Supports reverse animations like `Reverse Outside-Left`, `Reverse Outside-Bottom`, etc.

### How It Works
1. **Loading JSON Files**:
   - The JSON file name is passed as a URL parameter (e.g., `?json=example.json`).
   - Objects are loaded onto the canvas based on the JSON configuration.

2. **BroadcastChannel Integration**:
   - Listens for messages to perform animations or reverse actions.
   - Reloads the page with the specified JSON file if triggered.

3. **Animation Logic**:
   - Uses GSAP to animate objects from specific start positions based on metadata.
   - Reverse animations move objects outside the canvas boundaries.

4. **Custom Object Metadata**:

The custom data represents the status of the object at its starting position ("from" position) before it transitions to its final state (original status) during the animation. These attributes define how the object behaves and appears at the beginning of the animation and determine the transformation it undergoes to reach its original state.

Key attributes include:
- `data-duration`: Duration of the animation in seconds.
- `data-ease`: Easing function for a smooth transition.
- `data-delay`: Delay before the animation starts, in seconds.
- `data-position`: Starting position of the object (e.g., outside-left).
- `data-opacity`: Initial opacity of the object.
- `data-distance`: Distance the object travels from its starting position (optional - must be selected `inside` starting position).
- `data-scalex`: Initial scale along the X-axis.
- `data-scaley`: Initial scale along the Y-axis.
- `data-rotation`: Initial rotation angle of the object in degrees.

---

Enjoy!


