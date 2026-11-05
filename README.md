# Game of Life

Three browser versions of Conway's Game of Life. Each one is a single HTML file with no dependencies and no build step: just open it in a browser.

| File | What it is |
|---|---|
| `evolve-zoom.html` | **Zero-player, with zoom and pan.** Starts from a tiny seed on an almost empty world. An auto camera follows the growth, and you can zoom and pan freely. |
| `evolve.html` | **Zero-player.** Same idea, with a fixed view that fills the screen. |
| `index.html` | **Interactive.** A colorful version with glow and trails, spaceship rain, and click-to-launch spaceships. |
| `snapshots/` | Frozen copies of earlier versions. |

## How the Game of Life works

Every cell interacts with its eight neighbours: the cells that are horizontally, vertically, or diagonally adjacent. At each generation, all cells update at once:

1. A live cell with fewer than two live neighbours **dies** (underpopulation).
2. A live cell with two or three live neighbours **lives on**.
3. A live cell with more than three live neighbours **dies** (overcrowding).
4. A dead cell with exactly three live neighbours **becomes alive** (reproduction).

That's all of it. Spaceships, guns and breeders are just these births and deaths repeating. A glider doesn't move: each generation, cells die on its back edge and are born on its front edge.

Both zero-player versions have an **info button** (top right, next to the gear) that explains the rules with animated, zoomed-in demos.

## Zero-player versions (`evolve.html`, `evolve-zoom.html`)

You only watch; clicking never changes the simulation. Each run works like this:

1. The screen starts (almost) empty.
2. One pattern is placed. It's either a **small seed** of 5–20 cells, such as acorn, rabbits, Lidka, the R-pentomino, the 20-cell quadratic-growth pattern or the puffer train, or a **big machine**, such as Gosper's original breeder, rake breeders, switch-engine breeders, glider rakes, guns or a spacefiller.
3. Patterns that move start on the far side so they cross the whole world.
4. Sometimes a second small seed appears partway through (an **encounter**), so two growths collide.
5. When the population settles down, or the maximum run length is reached, the screen fades out and a new run begins.

### Controls

| Action | `evolve.html` | `evolve-zoom.html` |
|---|---|---|
| Pause / play | Space | Space |
| Next run | N | N |
| How it works | I | I |
| Close panels | Esc | Esc |
| Zoom | – | Scroll wheel, trackpad pinch, `+` / `-` |
| Pan | – | Drag, arrow keys |
| Back to auto camera | – | Double-click, F, or the fit button |

The **auto camera** (zoom version) starts close in on the seed and slowly pulls back as it grows. It frames the main mass of cells and ignores the occasional glider flying off on its own. Zooming or panning takes over; double-click hands control back.

### Settings (gear, top right)

- **Theme:** Golly gray, night, phosphor green, paper
- **Speed:** 1–2000 generations per second (a target; very busy patterns may run slower)
- **Cell size** (`evolve.html`) or **World size** (`evolve-zoom.html`)
- **Small seeds ↔ big machines:** how often a run starts with a machine
- **Encounters:** chance of a second seed during a run
- **Max run length:** 1–30 minutes, or unlimited
- **Auto camera** (zoom version), **Wrap edges**, **Frame**

Settings are saved in the browser.

## Interactive version (`index.html`)

- Random soup start, plus a steady rain of spaceships (glider, LWSS, MWSS, HWSS, copperhead, loafer), some arriving as fleets
- Wrap-around edges; it reseeds itself when things go quiet
- **Click** to launch a spaceship, **Shift-click** to launch a fleet, **drag** to draw cells
- Keys: Space pause, S step, F fleet, R new soup, C clear, `+` / `-` speed
- Settings for speed, color theme, trails, glow, cell size, spaceship rain, fleets and soup density

## Technical notes

- Plain HTML, CSS and JavaScript drawn on `<canvas>`. Works offline.
- The zero-player engine splits the grid into 32×32 tiles and skips any tile whose neighbourhood didn't change in the last generation, so mostly empty worlds stay fast. It was checked cell for cell against a straightforward reference simulation, with and without wrapping edges.
- When zoomed out past one pixel per cell, every live cell is still drawn as a crisp pixel instead of being blurred away.

## Credits

Conway's Game of Life was devised by John Horton Conway in 1970.

The seeds and machines in the zero-player versions come from the pattern collection bundled with [Golly](https://golly.sourceforge.io/), the open-source Life simulator. The original pattern files credit their discoverers, including Bill Gosper (breeder), Charles Corderman (acorn), Andrew Trevorrow (rabbits), Andrzej Okrasiński, David Bell, Dean Hickerson, Nick Gotts, Jason Summers, Dieter Leithner, Achim Flammenkamp, Helmut Postl, Keith Amling, Tim Coe and many others.
