# Niagara Terrain-Based Particle System

## Watch the Presentation Video
[![Niagara Terrain-Based Particle System](https://img.youtube.com/vi/TG4g-KtS0PE/maxresdefault.jpg)](https://youtu.be/TG4g-KtS0PE)  

This **Niagara System** enables particles to move randomly along the terrain, while respecting **climbability rules**, staying **within movement bounds**, and **falling** when encountering excessively steep slopes.

## 🔹 Parameters
- **`BoundRadius`**: Controls the maximum movement range of the particles.
- **`BoundCenter`**: Passes the Niagara system’s position as a parameter into Niagara via Blueprint.
- **`ClimbThreshold`**: Controls the maximum height difference that particles can climb directly.
- **`FlowmapStrength`**: Controls the overall speed of the particles.
- **`ZHeightOffset`**: Sets the offset value for the particle’s Z-axis position.

---

## 📌 System Overview

This system primarily leverages **RVT (Runtime Virtual Texture)** to achieve **random movement** of particles along the terrain surface.  
When particles encounter **overly steep surfaces**, they will **fall to the ground** before continuing their movement.

### 1️⃣ Adding Random Movement
- A **Curl Noise Force** is applied to introduce **randomness** into particle motion.

### 2️⃣ Flowmap Influence (`SampleRVT_Flowmap` Script)
- This script calculates the **local terrain gradient vector** after the particle moves a certain distance using the **RVT Heightmap**.
- The resulting force is accumulated into the current `PhysicsForce`.

### 3️⃣ Movement Constraints (`MovementBounds` Script)
- Checks whether a particle **exceeds the defined movement range**.
- If a particle **goes out of bounds**, a force is applied toward the **center**, pushing it back **within the valid area**.

### 4️⃣ Climbability Check (`ClimbBehavior` Script)
- Predicts the **height** at the particle's next position based on its **current velocity**.
- If the **height difference** between the predicted position and the current position **exceeds the climbable threshold**, the particle **cannot climb** and must **change direction**.

### 5️⃣ Surface Conformity (`ConformToZHeight` Script)
- Ensures that the **particle’s Z-axis height matches the terrain height**, keeping the particle **moving along the terrain surface**.

---

