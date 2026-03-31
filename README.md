# WEAP-Entry-Sim
This repository contains a 3D simulation, built with the Ursina engine in Python,
# Alcubierre–Burgess Warp Entry Demo (Ursina)

This repository contains a small Ursina-based visualization of a warp jump from rest to effective warp speed using an Alcubierre–Burgess style coefficient. The simulation implements a three-phase “press SPACE to enter warp” sequence to make the warp-entry event (the “blip”) visually explicit.

## What this script does

The script sets up:
- A grid and starfield so motion and depth are visible.
- A simple ship entity with an engine glow.
- A three-phase warp sequence triggered with the SPACE key:

1. **Phase 1 – Charge (rest / bubble formation)**  
   The ship vibrates with growing amplitude while staying effectively at rest, and the engine glow slowly expands. This represents the warp bubble charging up.

2. **Phase 2 – Blip (snap / warp entry)**  
   For a brief interval the effective speed jumps to several times the target warp speed, the ship stretches strongly along its travel axis, the camera field-of-view widens, and a short camera shake is applied. This visualizes the “blip” moment where the Alcubierre–Burgess coefficient crosses its critical value.

3. **Phase 3 – Sustained warp**  
   The ship settles into a moderately stretched cruising shape at a constant target warp speed, with the camera smoothly trailing the vessel and the FOV relaxing back toward normal.

## Controls

- `SPACE`: Engage warp (starts the charge → blip → sustained warp sequence).

The camera automatically follows the ship and stays locked on during the entire evolution.

## Requirements

- Python 3.9+ (tested version may vary)
- [Ursina Engine](https://www.ursinaengine.org/)

Install Ursina via:

```bash
pip install ursina
```

## Running the demo

Clone the repository and run the script:

```bash
git clone https://github.com/<your-user>/<your-repo>.git
cd <your-repo>
python warp_entry_ursina.py
```

(Replace `warp_entry_ursina.py` with the actual filename if different.)

## Relation to the theory

This demo is a toy visualization of a warp jump in an emergent-medium warp framework, where:
- Phase 1 corresponds to the build-up of the warp field/bubble.
- Phase 2 corresponds to the critical “blip” at warp entry (e.g. the warp entropy apex point).
- Phase 3 represents a steady-state warp trajectory after the transition.

It is intended as an intuitive companion to the underlying theoretical work, not a full numerical solution of the Einstein field equations.
 “The WEAP transition is the brief Blip phase where the WEAP coefficient crosses its critical value, shown as a sharp spike in effective velocity, ship stretch, and camera distortion between 1.8–2.0 s.”
