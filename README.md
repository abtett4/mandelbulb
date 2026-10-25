# Mandelbulb

A real-time GPU raymarcher for exploring Mandelbulb-family fractals, built with p5.js for a creative-code class.

Double-click `index.html` to open it in a browser. It works offline: p5.js 1.9.4 is included in `lib/`, and the page only falls back to cdnjs if that file is missing.

Live version: https://abtett4.github.io/mandelbulb/

## Controls

- **Drag** to orbit, **scroll** (or the **Zoom** slider in the Camera section) to zoom, **H** to hide the panel.
- **W/S**, **A/D** and **Q/E** move the point the camera orbits: forward and back, sideways, and down and up. To explore inside, steer that point into a crevice, zoom in close and orbit around it. Movement slows as you zoom in. **Re-center view** puts the point back at the middle.
- The panel groups its controls into **Parameters**, **Animation** and **Graphics** sections. Click a heading (or focus it and press Enter) to open or close it.
- **Formula** picks the fractal. Its equation is at the top of the **Parameters** section: symbols in blue match a slider (for example **n** is Power), and they light up while you hover over or focus that slider. **Preset** loads a known-good starting point for it, and **Reset to preset** returns there if you get lost.
- **Power n**, **Iterations**, **Theta/Phi offset** and the 4D sliders change the shape. For Julia sets, **Animate c** morphs the shape by moving c along the edge of the Mandelbrot set.
- **Palette**, **Glow** and **Coloring** change the look. **Orbit stripes** colors by how close each point's orbit comes to the center, and **Curvature** colors creases and ridges. **Soft shadows** adds shadows from the light, at some cost to frame rate.
- **Quality** sets the render resolution. Lower it if frames are slow.
- **Copy link** copies a link to the current view. The address bar always holds it too, so any view can be bookmarked or put in slides.
- **Save PNG** saves the current view at full window resolution.
- **Tour** (or **T**) hides the panel and slowly orbits through every preset, cross-fading between them. A bar at the bottom shows the current stop and the time until the next one. **Space** or a click pauses and resumes, and **Esc** or **Exit** ends the tour.

## Formulas

| Formula | What it is |
| --- | --- |
| Mandelbulb | White and Nylander's spherical-coordinate power formula |
| Spherical (p, q) | The same formula with separate multipliers for the two angles |
| Cubic, Quintic, Power-nine | Trig-free polynomial variants. Quintic uses z → −z⁵, and Power-nine has power-9 Mandelbrot cross-sections |
| Quaternion | z² + c in quaternions, as a Julia set or the Mandelbrot set, shown as a 3D slice of 4D |
| Bicomplex | z^n + c in bicomplex numbers. At power 2 the slice is the Tetrabrot |

Each formula has a distance estimator, and the fragment shader raymarches it. 4D formulas are sliced at a chosen w and can be rotated through the x-w plane. Shading uses ambient occlusion, a rim light, depth fog and optional soft shadows.

Each formula is compiled as its own shader. With every formula in one shader, Windows' shader compiler took about 30 seconds before the first frame. The page compiles the other formulas in the background after it loads, so switching formula later is instant.

## If the page stops drawing

Very heavy settings can make the graphics driver reset the GPU. The page lowers Quality on its own when frames get slow. If a reset still happens, it shows a **Recover** button.

If the browser has turned WebGL off for the page, the page says so. Click Reload in the browser's warning bar if there is one. Otherwise close and reopen the browser.

## Sources

- [Mandelbulb, Wikipedia](https://en.wikipedia.org/wiki/Mandelbulb): formulas for the Mandelbulb, (p, q) family, cubic, quintic and power-nine variants
- [p5.js](https://p5js.org/)
