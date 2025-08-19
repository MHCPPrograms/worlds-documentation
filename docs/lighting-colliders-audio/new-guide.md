# Creating Atmospheric Worlds with Lighting Gizmo
*Details lighting techniques, collider setup for interaction, and audio integration.*

---

## 🎯 Introduction
Lighting in Horizon Worlds is not just a visual element—it is one of the most powerful tools to guide **player emotions** and **orientation**.  
In this tutorial, you will learn:

1. **Lighting Techniques** – Different types of lights and methods to create atmosphere  
2. **Collider Setup for Interaction** – How lights react to player movements  
3. **Audio Integration** – Adding sound effects to enhance the experience  

---

## 🔦 Section 1 – Lighting Techniques

### 1.1. Light Types
- **Ambient Light** → General scene brightness  
- **Directional Light** → Simulates distant sources like sun or moon  
- **Point Light** → Omnidirectional light from a single point (e.g., a bulb)  
- **Spot Light** → Cone-shaped light to highlight specific areas (e.g., a spotlight)  

### 1.2. Key Parameters
- **Intensity:** Light brightness  
- **Color:** Warm (yellow-orange) or cool (blue) tones for atmosphere  
- **Range & Falloff:** Light distance effect and softness  
- **Shadows:** On/off for realism (affects performance)  

📸 *Tip:* Include screenshots showing each light type in the same scene.  

### 1.3. Atmosphere Examples
- **Horror Scene:** Low ambient, red spot light  
- **Sunset:** Low-angle yellow directional + soft ambient  
- **Mysterious Cave:** Blue point lights + slight fog  

---

## 🎮 Section 2 – Collider Setup for Interaction

Lights can be **dynamic** and respond to player presence.  

### 2.1. Adding Colliders
- Add a **Box Collider** or **Sphere Collider** around the light source  
- Set it as a **trigger**  

### 2.2. Simple Interaction
- When the player enters the collider, the spotlight turns on  
- When leaving, it turns off  

**Pseudo-code example:**
```javascript
OnTriggerEnter(player):
    Spotlight.SetActive(true)

OnTriggerExit(player):
    Spotlight.SetActive(false)
