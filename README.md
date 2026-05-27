# Solar System Orbit Simulation

A real-time, interactive 2D orbital physics simulation of the inner solar system (Mercury, Venus, Earth, and Mars orbiting the Sun) built in Python using the Pygame library. This simulation uses Newton's Law of Universal Gravitation to dynamically compute the gravitational forces between all celestial bodies, updating their velocities and orbital trajectories in real-time.

---

## 🌌 Features

- **Realistic Physics Engine:** Implements Newtonian gravitational attraction dynamically between all bodies (not just planet-to-sun, but planet-to-planet gravitational interactions as well).
- **Dynamic Orbit Tracking:** Renders custom colored orbital paths for each planet to visualize their trajectories over time.
- **Real-time Metrics:** Displays the live distance of each planet from the Sun in kilometers, updating as they move along their elliptical orbits.
- **Inner Solar System Scale:** Accurately scaled representation of:
  - **Sun** (Yellow)
  - **Mercury** (Gray)
  - **Venus** (Cream)
  - **Earth** (Blue)
  - **Mars** (Red)

---

## 🧮 Physics & Math Model

The simulation relies on Newton's Law of Universal Gravitation:

$$F = G \frac{m_1 m_2}{r^2}$$

Where:
- $F$ is the gravitational force between two masses.
- $G$ is the gravitational constant ($6.67428 \times 10^{-11} \, \text{m}^3\,\text{kg}^{-1}\,\text{s}^{-2}$).
- $m_1, m_2$ are the masses of the two interacting bodies.
- $r$ is the distance between the centers of their masses.

### 📐 Force Breakdown & Vector Mathematics
For each planet, the total gravitational force is calculated by summing the individual force vectors from all other bodies:

$$F_x = F \cos(\theta), \quad F_y = F \sin(\theta)$$

Where $\theta = \operatorname{atan2}(\Delta y, \Delta x)$.

The acceleration is then calculated using Newton's Second Law ($F = m a \implies a = F / m$), and the velocity and position are updated via **Euler-Cromer integration**:

$$v_{new} = v_{old} + a \cdot \Delta t$$
$$x_{new} = x_{old} + v_{new} \cdot \Delta t$$

Where $\Delta t$ (`TIMESTEP`) is set to **1 day** ($3600 \text{ seconds} \times 24$) per iteration.

---

## ⚙️ Scale & Configuration

Because celestial distances and masses are astronomical, the simulation employs scaling factors to fit the render window ($800 \times 800$ pixels) while preserving relative proportions:
- **Distance Scale:** $1 \, \text{AU}$ (Astronomical Unit $\approx 149.6 \times 10^6 \, \text{km}$) is represented as **200 pixels** on screen.
- **Time Step (`TIMESTEP`):** 1 day per frame update (fast-forwards time so orbital motions are visible).
- **Frame Rate:** Capped at 60 frames per second using Pygame's internal clock.

---

## 🚀 Getting Started

### 📋 Prerequisites

To run this simulation, you need **Python 3.x** and the **Pygame** library installed on your system.

If you don't have Pygame installed, you can install it via `pip`:

```bash
pip install pygame
```

### 🏃 Running the Simulation

Clone this repository or navigate to the directory containing `solarSys.py`, and run the following command in your terminal/command prompt:

```bash
python solarSys.py
```

---

## 📂 Code Structure

The simulation is contained entirely within `solarSys.py`:

- **`Planet` Class:** Represents each celestial body.
  - `__init__`: Initializes the coordinates ($x, y$), radius, color, mass, initial velocity, and orbital path history.
  - `draw(win)`: Draws the planet, its orbital trail, and its distance reading from the Sun.
  - `attraction(other)`: Calculates the gravitational force components exerted on it by another `Planet` instance.
  - `update_position(planets)`: Iterates through all other bodies, aggregates total forces, updates velocity vectors, and calculates new coordinates.
- **`main()` Function:** Sets up the Pygame window, instantiates the Sun and the inner planets with their correct starting physical values (mass, distance, orbital velocity), and runs the animation/physics update loop.

---

## 🎨 Visualization Details

- **Elliptical Orbits:** Since planets are given their actual average orbital velocities (e.g., Earth at $29.783 \, \text{km/s}$), you can observe their naturally forming, stable, slightly elliptical orbits.
- **Kepler's Laws in Action:** Observe that planets closer to the Sun (like Mercury) travel significantly faster and complete orbits much quicker than planets further out (like Mars).
