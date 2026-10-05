<div align="center">

# 🎓 Late for Class — An OpenGL Campus Story

**A six-scene interactive animation built from scratch with C++, OpenGL and GLUT.**
A student runs late for class, sits through a lecture, daydreams — and ends up taking a penalty kick on the football field.

![C++](https://img.shields.io/badge/C%2B%2B-OpenGL%20%2F%20GLUT-00599C?logo=cplusplus&logoColor=white)
![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux-lightgrey)
![IDE](https://img.shields.io/badge/IDE-Code%3A%3ABlocks-brightgreen)
![Course](https://img.shields.io/badge/course-CSC%204118%20Computer%20Graphics-orange)

</div>

---

## 📖 About

This is the final-term project for **CSC 4118: Computer Graphics** at the American International University-Bangladesh (AIUB), Summer 2025–2026 (Group 03).

Instead of a collection of disconnected demos, the project is one continuous **narrative**: a student arrives at the ANNEX-9 building, gets through the face scanner, walks down the corridor, takes a seat in a lecture where the teacher explains how to draw a rectangle and triangle in OpenGL, gets bored, and daydreams about playing football. Every scene lives in its own C++ namespace and is stitched together by a shared master timer and keyboard handler.

Everything is drawn with raw OpenGL primitives (`GL_QUADS`, `GL_POLYGON`, `GL_LINES`, `GL_TRIANGLES`) — no textures, no models, no external assets.

## 🎬 The Story

| # | Scene | What happens |
|---|-------|--------------|
| 1 | **Entrance** | The student walks to the ANNEX-9 entrance, gets face-scanned, the view zooms in and the doors slide open. |
| 2 | **Corridor** | He walks down the corridor, reaches room 9302, reaches for the handle and opens the door. |
| 3 | **Classroom entry** | He walks in, turns to face the teacher and sits down among his classmates. |
| 4 | **Teacher** | The teacher lectures with hand gestures and lip animation; the projector screen unrolls to show a rectangle and a triangle, or the lesson question. |
| 5 | **Daydream** | A "Boring...." thought bubble floats up as the camera zooms in on the student. |
| 6 | **Football dream** | "I want to play football!" — then a playable penalty shootout against a goalkeeper. |

## 📸 Screenshots

<table>
  <tr>
    <td align="center"><img src="[docs/screenshots/01-entrance.png](https://github.com/MUNISH8/Computer-Graphics-Project/blob/main/01-entrance.png)" width="400"><br><sub><b>1 · Entrance</b></sub></td>
    <td align="center"><img src="docs/screenshots/02-corridor.png" width="400"><br><sub><b>2 · Corridor</b></sub></td>
  </tr>
  <tr>
    <td align="center"><img src="docs/screenshots/04-classroom-entry.png" width="400"><br><sub><b>3 · Classroom entry</b></sub></td>
    <td align="center"><img src="docs/screenshots/05-teacher.png" width="400"><br><sub><b>4 · Teacher & projector</b></sub></td>
  </tr>
  <tr>
    <td align="center"><img src="docs/screenshots/06-daydream.png" width="400"><br><sub><b>5 · Daydream</b></sub></td>
    <td align="center"><img src="docs/screenshots/08-football-match.png" width="400"><br><sub><b>6 · Football penalty match</b></sub></td>
  </tr>
</table>

## 🎮 Controls

The story advances with **`N`** whenever a scene is finished and waiting. Each scene also has its own keys:

| Scene | Key | Action |
|-------|-----|--------|
| **Global** | `N` | Continue to the next scene / step once the current one is ready |
| | `Esc` | Quit |
| **1 · Entrance** | `W` | Walk toward the entrance |
| | `N` | Zoom in and open the doors (after reaching the scanner) |
| | `W` | Walk through the open doors |
| **2 · Corridor** | `W` | Walk down the corridor |
| | `O` | Open the classroom door |
| **3 · Classroom entry** | `W` | Walk in, then stand and sit (automatic) |
| **4 · Teacher** | `L` | Start / stop arm gestures and talking |
| | `M` | Unroll / roll up the projector screen |
| | `A` | Toggle shapes ↔ lesson question on the screen |
| | `R` | Move the teacher sideways (press again to reverse) |
| **5 · Daydream** | `D` | Start the daydream (thought bubble + zoom) |
| **6 · Football** | `A` / `B` | Aim at the left / right corner (no key = straight down the middle) |
| | `X` | Kick the ball |
| | `Y` | Dive the goalkeeper to save the shot |

> The football result is shown as **GOAL!**, **SAVED!** or **NOT GOAL!**, then the field resets so you can keep shooting.

## 🛠️ Build & Run

### Requirements
- A C++ compiler (GCC / MinGW)
- [FreeGLUT](https://freeglut.sourceforge.net/) and OpenGL

### Option 1 — Code::Blocks (Windows)
1. Open `CG_FinalMergedPro.cbp`.
2. Make sure FreeGLUT is installed for your MinGW toolchain (the project links `freeglut`, `opengl32`, `glu32`, `winmm`, `gdi32`). If your MinGW path differs, update the include/lib directories under **Project → Build options → Search directories**.
3. Build and run (`F9`).

### Option 2 — Command line (Windows / MinGW)
```bash
g++ src/main.cpp -o CampusStory -lfreeglut -lopengl32 -lglu32 -lwinmm -lgdi32
./CampusStory
```

### Option 3 — Command line (Linux)
```bash
sudo apt install freeglut3-dev      # Debian / Ubuntu
g++ src/main.cpp -o CampusStory -lglut -lGL -lGLU
./CampusStory
```

The window opens at 1000 × 750 and every scene shares one `0..100 × 0..75` coordinate system.

## 🧠 How It Works

- **Scene namespaces** — `Entrance`, `Corridor`, `Classroom`, `Teacher` and `Football` each own their own state, drawing functions, timer and keyboard handler.
- **Master controller** — `displayMain()` picks which scene to render from a single `scene` counter (10 internal stages), `timerMain()` ticks the active scene every 30 ms, and `keyboardMain()` routes input and handles the `N` hand-offs.
- **State machines** — multi-stage animations are phase-based, e.g. *walk → stand → sit* in the classroom and *thought bubble → match* in the football scene.
- **Reusable drawing functions** — helpers such as `drawBench()`, `drawStudent()` and `human()` build repeated objects (8 benches, 12 seated classmates) efficiently.
- **Bézier ball trajectory** — the football follows a curved path from the striker to the goal.

### Graphics concepts demonstrated
- Primitive-based modeling (`GL_QUADS`, `GL_POLYGON`, `GL_LINES`, `GL_TRIANGLES`)
- 2D transformations: `glTranslatef`, `glScalef`, `glRotatef`
- Timer-driven and phase-based animation
- Keyboard-driven interaction
- Camera zoom effects
- Bézier-curve motion

## 📁 Project Structure

```
.
├── src/
│   └── main.cpp                  # All scenes + master controller
├── docs/
│   ├── screenshots/              # Output screenshots used in this README
│   └── report/
│       └── Graphics_project_report.docx   # Full project report (graphs, object & animation IDs)
├── CG_FinalMergedPro.cbp         # Code::Blocks project
├── .gitignore
└── README.md
```

The full report in [`docs/report`](docs/report/Graphics_project_report.docx) includes the hand-drawn and GeoGebra design graphs, a numbered list of every object and drawing function, and a list of animation functions with IDs.

## 👥 Team — Group 03

| Member | Scene |
|--------|-------|
| **Farhana Tabassum Saheli** | Outdoor entrance (Scene 1) |
| **Samia Afruz Asha** | Corridor & classroom door (Scene 2) |
| **Munish Sarker** | Classroom entry, seating & daydream (Scenes 3 & 5) |
| **Rinko Rani Vadra** | Teacher's classroom (Scene 4) |
| **Shammi Binte Mottaleb** | Football dream match (Scene 6) |

Equal contribution (20% each). Merged into a single program by the whole team.

## 🙏 Acknowledgements

Built for **CSC 4118: Computer Graphics**, Department of Computer Science, Faculty of Science and Technology, American International University-Bangladesh.

## 📄 License

No license has been chosen yet. Add a `LICENSE` file (for example MIT) before making the repository public if you want others to reuse the code.
