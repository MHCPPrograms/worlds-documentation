# Blender to Horizon Worlds: Your Import Guide

This guide provides a comprehensive workflow for creating a 3D model in Blender, preparing it for import, and bringing it into the Horizon Worlds desktop editor. By following these steps, you can create custom assets with specific material properties, enhancing the visual appeal and complexity of your worlds.

- - -

## Part 1: Preparing Your Asset in Blender

This section focuses on the steps you need to take within Blender to ensure your model and its materials are ready for Horizon Worlds.

### 1\. Checking Model Statistics

*   Before you begin, it's important to check your model's vertex count to stay within the **400,000 vertex limit** for Horizon Worlds.
*   To do this, enable the `Statistics` overlay in Blender. Go to the top-right corner of the 3D viewport, click the dropdown arrow next to the overlay icons, and check the box next to `Statistics`.
<img width="357" height="671" alt="image" src="https://github.com/user-attachments/assets/7f771d58-4e19-49f9-b2b7-40e87ad7900e" />

*   This will display the `Verts` (vertices) count in the bottom-right corner of the viewport, giving you real-time feedback on your model's complexity.
<img width="407" height="328" alt="image" src="https://github.com/user-attachments/assets/dab1f901-4c35-4851-9114-f5d2132837a9" />

### 2\. Deciding on Static vs. Animated Models

*   **Single-Mesh:** If your model is a single, static object (e.g., a rock or a building), it's best to **merge all the meshes into one**. This helps with optimization.
*   **Multi-Mesh:** You may need a multi-mesh model if you have a large scene you want to rearrange in Horizon, or if you want to animate specific parts of it.
    *   If your model has separate, moving parts (e.g., a treasure chest with a lid that opens), you need to keep those meshes separate. This allows you to animate each piece individually in Horizon Worlds.
    *   **Caution:** To maintain the original pivot point for each separate object, you must export them as separate FBX files. Horizon Worlds only supports one pivot point per imported mesh.

### 3\. Texturing Your Model

Once you've determined your model's purpose, the next steps in the workflow are to prepare your textures and materials.

*   **Creating and Naming Materials:**
    *   Start with a mesh in Blender.
    *   Create a new material and name it. The name is crucial because it must match the name of your texture files. For example, if you name your material `metal`, your texture files must also start with `metal`.
*   **Baking and Creating Textures:**
    *   To simplify complex materials and ensure they render correctly, you should **bake** your Blender materials into a single texture. Navigate to the `Render` properties, set your render engine to `Cycles`, and find the `Bake` panel.
    *   Horizon Worlds uses a specific naming convention to interpret different texture properties. You can create these textures in Blender or in external software like Photoshop.
    *   **`_br` (Base Color and Roughness):** This texture controls the base color and the roughness of your object. The RGB channels define the color, and the Alpha channel controls the roughness (a higher alpha value means a shinier surface). Name the file `[material_name]_br.png`.
    *   **`_meo` (Metallic, Emission, Occlusion):** This texture controls metallic, emissive, and ambient occlusion properties. The Red channel controls `Metallic` (fully red for metallic surfaces), the Green channel controls `Emission` (for glowing objects), and the Blue channel controls `Occlusion`. Name the file `[material_name]_meo.png`.

### 4\. Exporting the FBX File

*   **Combine Objects:** If your model is static, combine them into a single object before exporting.
*   **Export as FBX:** Go to `File > Export > FBX`.
*   **Adjust Export Settings:** Ensure the `Forward` axis is set to **negative Z**. This is a critical step to ensure your model's orientation is correct when imported into Horizon Worlds.

- - -

## Part 2: Importing into the Horizon Worlds Desktop Editor

This section covers the final steps of bringing your prepared assets into Horizon Worlds.

### 1\. Importing the Assets

*   In the Horizon Worlds desktop editor, navigate to the `Assets` tab.
*   Select **Add New 3D Model** and then **Add Files on Your Device**.
*   Select your exported FBX file and all of its corresponding texture PNG files to upload them together.
*   **Preserve Offsets:** The videos recommend turning off the "Preserve Offsets" option during import unless you have a specific use case that requires it (e.g., an animated door hinge).

### 2\. Using Your Asset

*   Once the import is complete, your new model will appear in your asset library.
*   Simply drag it from the asset library into your world.
*   If you followed all the naming conventions correctly in Blender, the textures will be automatically applied, and the model will appear exactly as you designed it.

- - -

## Additional Tips from the Videos

*   **Optimization:** Use smaller texture sizes (e.g., 1K) to improve performance and reduce world loading times.
*   **Vertex Count:** Always keep an eye on your model's vertex count to stay within limits and ensure smooth performance.
*   **Double-Sided Meshes:** For thin objects like leaves or paper, enable double-sided rendering in Blender to ensure they are visible from all angles.

This guide combines the essential information from the provided videos into a single, comprehensive tutorial. It provides actionable steps, explains the importance of key settings, and includes valuable tips for optimization, making it a valuable resource for other creators.
