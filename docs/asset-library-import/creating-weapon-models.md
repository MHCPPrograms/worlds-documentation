# Creating Weapons in Blender and using the Horizon Worlds: Royal axe.

Sahil (thesloppyguy)

September 4, 2025

---

## Introduction

This tutorial will walk you through **using blender to create a weapon**, creating textures and using the same in Horizon worlds.

By the end, you’ll understand:

- How to easiry use templated to create Weapons.
- How to create textures and materials for the assets.
- How to prepare and optimize the asset for export(fbx).
- How to import and use the asset in Horizon World.

### Prerequisites and Expectations

You should be familiar with:

- General tools and UI of blender.
- (Optional) Any Photoediting or painting tool.
- (Optional) Install 3D viewer on windows to view 3D models like image Thumbnails

## Topic One: Setting up the Environment

You can install blender, and an editing tool of your choice. I will be using **Blender 4.4.2**. Once completed go to `Edit` -> `Preference` -> `Addons`. If you are new to blender this should be empty and we will guide you through the process of add some good to have addons and their features.

## Topic Two: How to create a weapon (Axe) in blender?

### Step 1: Finding Refernce

1. Find or Create a 2D Reference Image for your weapon. This will act as a template for our project
2. In My Case I have a Template of an AXE. if have one with color and design that is also fine we can use it for textures and coloring the asset.
3. Once you have the image, drag and drop it, then center and flatten the image into your viewport.
4. On pressing 1 on you numpad the template should appear flat.

### Step 2: Create the Asset Body

1. There should a cube at the center of your viewport you can resize and move it to be inside your template borders.
2. Go to `Addons` and add the following Plugin - [Auto Mirror](Add link)
3. Select the block and press `N` go to edit and select Auto Mirror.
   1. Add a X Positive Mirror and a Y Negative Mirror.
   2. With this you will only need to work on a quarter of the asset and the rest will be automatically handled.
4. This is the starting point of our weapon modeling. Enter editmode (Tab) and Extruted and Resize it to cover the template.
5. Following are some easy shortcuts
   1. E to Extrude
   2. G to Grab
   3. B for Box Select
   4. Ctrl B for Bevel
   5. Use the 3 selection modes to make your life easier (point, edge, face) during selection.
   6.
6. By the end of this Step you should have a single mesh that looks like a Weapon (Axe).
7. You can apply both the mirror function to the asset to finalize the structure.

### Step 4: Optimizing you Asset

1. Turn on the staticits and analyse the number of Vertex, Triangles and Faces.
2. The bigger the number the worse the performance. Always try to use low poly asset of VR or Horizon worlds for better performance and user experience.
3. You can use the following techniques to reduce the numbers and get better performance.
   1. Desemate (Easy but not always good)
   2. Re Mesh (Easy but not always good)
   3. Manually merging Edges Vectors and Faces. (Slow but Best Result)

**Note:** There are some other ways to optimize the assets but they require either addons or additional know how. the above is good enough for now.

### Step 5: Adding Colors and Texture to your Model

1.

### Step 6: Preparing Textures and Materials

#### Naming Standards

- Avoid using any special characters
- Use CamelCase for Primary name and append Suffix Type for Texture and Materials to the end of the name and before extensions like `Test_BR.png`
- Full Documentation can be found [here](https://developers.meta.com/horizon-worlds/learn/documentation/custom-model-import/creating-custom-models-for-horizon-worlds/materials-guidance-and-reference-for-custom-models).

#### Editing Textures (optional)

## Topic Three: Exporting and Importing: Assets and Textures

### STEP 1: Final Checks

1. Asset Should be in a single mesh.
2. Apply all transformations or unsaved changes.
3. Verify Material Name and Texture Name Suffix and Camel Case

### Step 2: Export into FBX

1. Go to `File` -> `Export` -> `FBX`

### Step 3: Importing Into Worlds

You can also preview your asset in 3D Viewer if you have the software installed (free from Microsoft store).

1. Launch the **Worlds Desktop Editor**.
2. Open the world where you want to use the asset.
3. In the **Asset Library**, click the **Add New** dropdown menu.
   1. Choose **3D Model**.
   2. In the Import window, click **Choose Files on Your Device**.
   3. Select your **FBX** _and_ all the necessary **textures**.
      - If the files are in different folders, you can add them one by one.
4. Once everything is listed, click the **blue Import button**.
5. If there are any warnings (Yellow Mark) or errors (Red Mark) you have missed a step.
   - The message can help you debug the issue.

### Accessing Your Imported Asset

- After import, your model will appear under **My Assets** in the Asset Library.
- Drag it from **My Assets** into your world to place it.
- If your materials and textures were named correctly, they will already be applied automatically.
- No extra setup is required.

[Insert screenshot: Asset visible in My Assets folder]

---

-

## Topice Three:

## Step 1: Prepare Your Textures

> ⚠️ If you are using **Vertex PBR materials**, you can skip this step.

Worlds materials only support a **maximum of two textures** per material.  
We’ll call these **TextureA** and **TextureB**.

---

### TextureA

- **RGB channels (Red, Green, Blue):** BaseColor values
- **Alpha channel:**
  - Roughness, **or**
  - Roughness + Metalness, **or**
  - Alpha (opacity)

👉 Which one you use depends on your chosen material type. See the [Meta documentation](https://developers.meta.com/horizon-worlds/learn/documentation/custom-model-import/creating-custom-models-for-horizon-worlds/materials-guidance-and-reference-for-custom-models) for details.

---

### TextureB

TextureB allows you to control additional PBR properties:

- **Red (R):** Metalness
- **Green (G):** Emissive
- **Blue (B):** Ambient Occlusion
- **Alpha (A):** Alpha (only for Transparent materials)

For Transparent materials:

- **Blue (B)** is used for **Specular** instead of Ambient Occlusion.

### Notes on TextureB Naming

- TextureB in **Double-Texture PBR Materials** → use the **\_MEO** tag
- TextureB in **Transparent Materials** → use the **\_MESA** tag
- TextureB in **Vertex Color Double-Texture PBR Materials** → use the **\_MEO** tag

---

### Edit Color Channels in GIMP

In this tutorial we’ll be using [GIMP](https://www.gimp.org/), a free and open-source image editor, to prepare textures.  
The same steps can be followed in other image editing programs such as Photoshop or Krita, but the menus and shortcuts may look slightly different.

1. **Open a texture in GIMP.**

2. Click **Channels**.  
   ![Channels](https://iili.io/K2ffu6v.png)

3. You should see your **Red, Green, and Blue channels**.

   - If you need an **Alpha channel** but don’t see one:
     - Click **Layers** to return to the layer selection.
     - Right-click the layer you need to modify, and choose **Add Alpha Channel**.

4. In this example, let’s assume we’re adding **Roughness values** to support our material.

   - By default, all color channels are selected.
   - Each color channel row will be highlighted black.
   - If you click on a channel, it will be deselected (turn grey).
   - Deselect **Red, Green, and Blue** by clicking on them.
   - Your Channels should look like the image displayed below.  
     ![Alpha Channel Selected](https://iili.io/K2fndOB.png)

5. Now you can define values for the Alpha channel:

   - Fill with **white** → Roughness = 1 (fully rough).
   - Fill with **black** → Roughness = 0 (fully smooth).
   - Fill with **grey** → A value in between.
   - Or paint custom values.
   - If you already have a roughness texture, copy it into the base texture using these steps:

   a. Open your **roughness texture** as a new layer, or as a new GIMP file.

   b. If the roughness texture is not already greyscale:

   - Go to **Colors > Desaturate**.
   - Select all (**Ctrl+A**) and copy (**Ctrl+C**).

   c. If you opened your roughness texture as a new layer:

   - Delete or hide it by clicking the **eye icon** in the Layers window.
   - Right-click your base texture and choose **Add Layer Mask**.
   - Click **Add** on the popup (default settings are fine).

   d. Your layer now has two preview icons. The mask layer should be selected by default.

   - Click between the icons if unsure—it should be clear which is active.  
     ![Mask Selected](https://iili.io/K2foLGe.png)

   e. Paste (**Ctrl+V**) the roughness texture.

   - It will appear as a floating layer.
   - Click the **green anchor icon** at the bottom of the Layers window to anchor it in place.
     ![Anchor Icon](https://iili.io/K2fxtVt.png)

   f. That’s it! If you look at the Alpha Channel, you’ll see the values match your roughness texture.

6. Save this file as your **TextureA**.
   - See the next section for how to properly name your textures.

--

## ✅ Texture Naming Rules

1. **Base name comes from the material name.**

   - Use the exact name of the material, but **strip underscores or suffix identifiers** that were added for organizational purposes.
   - Example:
     - Material name: `MyMarvelousMaterial`
     - Texture prefix: `MyMarvelousMaterial`

2. **Textures must always include an underscore and a type identifier.**

   - This tells you what kind of PBR data the texture holds.
   - Always use the identifiers consistently.

3. **File extension** should be standard (e.g. `.png`).

---

## 🔑 Identifier Keys

### TextureA

- **B** = Base Color (RGB channels = color)
- **R** = Roughness (Alpha channel often used for roughness if packed with Base Color)
- **A** = Alpha (opacity, when applicable)

📌 Example:  
`MyMarvelousMaterial_BR.png` → BaseColor (RGB) + Roughness (A)

---

### TextureB

- **M** = Metalness
- **E** = Emissive
- **S** = Specular
- **A** = Ambient Occlusion

📌 Example:  
`MyMarvelousMaterial_MESA.png` → Metalness (R), Emissive (G), Specular (B), Ambient Occlusion (A)

---

## ⚡ Final Examples

- `WoodPlank_BR.png` → Base Color + Roughness
- `WoodPlank_MESA.png` → Metalness, Emissive, Specular, AO
- `GlassPane_BA.png` → Base Color + Alpha (opacity)

--

## Step 2: Preparing Your Asset (Blender)
