from ursina import *
import random

# --- ALCUBIERRE-BURGESS COEFFICIENT SIMULATION ---
# This script simulates a warp jump from rest to warp speed.
# Press 'SPACE' to engage.

app = Ursina()

# 1. THE ENVIRONMENT (Grid and Stars to see movement)
# We need reference points in space to see the "Blip"
for i in range(20):
    Entity(model=Grid(50, 50), rotation_x=90, y=-5, z=i*50, color=color.dark_gray)

# Starfield effect for depth
stars = [Entity(model='sphere', scale=.1, position=(random.uniform(-50,50), random.uniform(-20,20), random.uniform(0, 1000)), color=color.white) for _ in range(200)]

# 2. THE SHIP (Alcubierre Drive Vessel)
ship = Entity(model='cube', color=color.cyan, scale=(1.5, 0.7, 3), position=(0,0,0))
engine_glow = Entity(parent=ship, model='sphere', color=color.azure, scale=(1.2, 0.5, 0.5), z=-1.5)

# 3. WARP PARAMETERS
target_warp_speed = 600.0
current_speed = 0.0
charge_timer = 0.0
is_warping = False

def input(key):
    global is_warping, charge_timer
    if key == 'space':
        is_warping = True
        charge_timer = 0.0
        print("Alcubierre Drive: Charging Burgess Coefficient...")

def update():
    global current_speed, charge_timer, is_warping
    
    if is_warping:
        charge_timer += time.dt
        
        # PHASE 1: THE CHARGE (The "Rest" phase)
        if charge_timer < 1.8:
            # Physical vibration as the bubble forms
            shake_amt = (charge_timer / 1.8) ** 3 * 0.3
            ship.x = random.uniform(-shake_amt, shake_amt)
            ship.y = random.uniform(-shake_amt, shake_amt)
            current_speed = 0
            engine_glow.scale += Vec3(0.01, 0.01, 0.01) # Glow grows
            
        # PHASE 2: THE BLIP (The "Snap" phase)
        elif charge_timer < 2.0:
            # Massive speed spike and visual distortion
            current_speed = target_warp_speed * 3.0 
            ship.scale_z = 25.0 # The "Stretch"
            camera.shake(duration=0.1, magnitude=3)
            camera.fov = 120 # FOV stretch for speed perception
            
        # PHASE 3: SUSTAINED WARP
        else:
            current_speed = target_warp_speed
            ship.scale_z = 6.0 # Settle into a stretched cruising shape
            camera.fov = lerp(camera.fov, 90, time.dt * 2)
            ship.x = 0
            ship.y = 0

        # Apply velocity to Z position
        ship.z += current_speed * time.dt
        
        # Camera follows smoothly
        camera.position = lerp(camera.position, ship.position + Vec3(0, 8, -25), time.dt * 5)
        camera.look_at(ship)

# Setup Camera
camera.position = (0, 8, -25)
Sky()

print("Instructions: Press SPACE to engage warp.")
app.run()
