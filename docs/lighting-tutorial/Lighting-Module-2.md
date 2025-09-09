# Module 2 — Working with Dynamic Light Gizmos

Welcome to Module 2. Now that you understand static lighting, it's time to explore the more powerful and flexible **Dynamic Light Gizmo**. These lights can move, change color, and react in real-time, making your worlds feel alive and interactive.

---

## 🎯 What You'll Learn in This Module
- How to add and configure a Dynamic Light Gizmo.
- The meaning and use of its unique properties: **Light Type**, **Falloff Distance**, and **Spread**.
- How to create a simple animation using the editor's built-in tools.
- The performance implications of using dynamic lights.

---

## 🛠️ Prerequisites
- Completion of **Module 1**.
- The same simple scene with a cube and a dark environment. You can continue from where you left off.

---

## ⚙️ Step-by-Step Guide

### 1. Add a Dynamic Light Gizmo
Let's start by adding a dynamic light to our scene. The process is very similar to adding a static one.

- Navigate to **Build > Gizmos**.
- In the search bar, type "**dynamic**" to find the **Dynamic Light Gizmo**.
- Drag it into your scene and position it near your cube.

You'll notice it looks different from the static gizmo, often appearing as a wireframe sphere or cone.

*[Image: The Gizmos menu showing the Dynamic Light Gizmo being added to the scene.]*

### 2. Configure the Core Properties
In the **Properties** panel, you'll see some familiar settings under the **Light** section.

- **Color**: Set the light's color just like you did for the static light.
- **Intensity**: Adjust the brightness. Note that the dynamic light's range is typically smaller (e.g., 0-10) than the static light's.

Set these to a visible color and intensity so you can see the effects of the next steps clearly.

*[Image: The Properties panel for the Dynamic Light Gizmo with Color and Intensity highlighted.]*

### 3. Explore the Unique Dynamic Properties
This is where the Dynamic Light Gizmo truly differs. Let's explore its unique settings.

- **Light Type**: This defines the light's shape and behavior.
  - **`Point`**: An omnidirectional light that shines in all directions, like a bare lightbulb.
  - **`Spot`**: A cone-shaped light that shines in a specific direction, like a flashlight or a stage light. **Select `Spot` for now.**

- **Falloff Distance**: This controls how far the light travels before it fades out completely. A low value creates a small, intimate pool of light, while a high value can illuminate distant objects.

- **Spread**: *This property only affects `Spot` lights.* It controls the width of the light's cone, from a very narrow, focused beam to a wide, soft spotlight.

**Experiment!** Try switching between `Point` and `Spot` types. Adjust the `Falloff` and `Spread` sliders to get a feel for how they change the light's appearance.

*[GIF: A screen recording showing the user adjusting the Light Type, Falloff, and Spread properties and observing the real-time changes on the cube.]*

### 4. Create a Simple Animation (No Scripting Needed!)
To see the "dynamic" nature in action, we can use the Animation Editor to make the light pulse.

1.  Select the **Dynamic Light Gizmo**.
2.  Open the **Animation Editor** panel.
3.  Create a new animation clip named "Pulse".
4.  At frame `0`, add a keyframe for the **Intensity** property at a low value (e.g., `1`).
5.  Move the timeline cursor to the middle (e.g., frame `30`), change the **Intensity** to a high value (e.g., `8`), and add another keyframe.
6.  Move to the end (e.g., frame `60`), set the **Intensity** back to `1`, and add a final keyframe.
7.  Set the animation to **Loop** and press **Play**.

Your light should now be pulsing, growing brighter and dimmer on its own! This is an effect that is impossible to achieve with a static light.

*[Image: The Animation Editor panel showing keyframes for the Intensity property of the Dynamic Light Gizmo.]*

---

## ⚠️ A Note on Performance
Dynamic lights are powerful, but they come at a cost.
- **They are resource-intensive** because the engine has to calculate their light and shadows every single frame.
- **There is a limit** of **20 Dynamic Light Gizmos** per world to ensure good performance.

Use them where they have the most impact—for special effects, interactive objects, or to guide the player's attention. For general scene lighting, always prefer static lights.

---

## ✅ Module Recap
You've now worked with both types of lighting gizmos!

In this module, you learned how to:
- Add a **Dynamic Light Gizmo** and configure its basic settings.
- Differentiate between **Point** and **Spot** light types.
- Use **Falloff Distance** and **Spread** to shape your light.
- Create a simple lighting animation directly in the editor.
- Understand the performance trade-offs of dynamic lighting.

---

## 🚀 Next Steps
You've seen what a dynamic light can do, but its true potential is unlocked when you control it with code. In the next module, we'll dive into the **DynamicLightGizmo API** to create a fully interactive lamp.

👉 Continue to **Module 3: Scripting with the DynamicLightGizmo API**.
