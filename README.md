# Mandelbulb

A real-time GPU raymarcher for exploring Mandelbulb-family fractals, built with p5.js for a creative-code class.

Everything is in one file, `index.html`. Double-click it to open it in a browser. It needs an internet connection the first time, to load p5.js 1.9.4 from cdnjs.

## Controls

- **Drag** to orbit, **scroll** to zoom, **H** to hide the panel.
- **Formula** picks the fractal. **Preset** loads a known-good starting point for it, and **Reset to preset** returns there if you get lost.
- **Power n**, **Iterations**, **Theta/Phi offset** and the 4D sliders change the shape. **Palette** and **Glow** change the look.
- **Quality** sets the render resolution. Lower it if frames are slow.

## Formulas

| Formula | What it is |
| --- | --- |
| Mandelbulb | White and Nylander's spherical-coordinate power formula |
| Spherical (p, q) | The same formula with separate multipliers for the two angles |
| Cubic, Quintic, Power-nine | Trig-free polynomial variants. Quintic uses z → −z⁵, and Power-nine has power-9 Mandelbrot cross-sections |
| Quaternion | z² + c in quaternions, as a Julia set or the Mandelbrot set, shown as a 3D slice of 4D |
| Bicomplex | z^n + c in bicomplex numbers. At power 2 the slice is the Tetrabrot |

Each formula has a distance estimator, and the fragment shader raymarches it. 4D formulas are sliced at a chosen w and can be rotated through the x-w plane.

## If the page stops drawing

Very heavy settings can make the graphics driver reset the GPU. The page lowers Quality on its own when frames get slow. If a reset still happens, it shows a **Recover** button.

If the browser has turned WebGL off for the page, the page says so. Click Reload in the browser's warning bar if there is one. Otherwise close and reopen the browser.

## Sources

- [Mandelbulb, Wikipedia](https://en.wikipedia.org/wiki/Mandelbulb): formulas for the Mandelbulb, (p, q) family, cubic, quintic and power-nine variants
- [p5.js](https://p5js.org/)
