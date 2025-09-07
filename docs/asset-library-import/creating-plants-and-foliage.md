# Creating Stylized, Low-Poly Plants
In this guide, I'm going to go over the method I've learned for creating stylized, low-poly, and game-ready plants and foliage. This article assumes that you have some pre-existing knowledge of textures, 3D, and the Horizon Worlds Desktop Editor.

We'll start with design and conceptualization, moving on to creating a texture atlas, then creating a mesh and UVs, and finally, implementation into the Meta Horizon Worlds environment using the Desktop Editor. I will be using Blender for all 3D-related creation, and then 2D texture creation is split between Photoshop, and a mobile painting app called Sketchbook. 

## Concept & Planning
The first thing we’re going to cover is figuring out what style and design your plant should have. Does your world crave the graceful, creeping tendrils of a plant that feels dark and malevolent? Or perhaps the cheerfulness of bright colors and rounded shapes are more appropriate for your world!

I personally like to draw out some basic ideas using just a solid color to explore the shape and silhouette. These don’t have to be anything particularly detailed or spectacular at this point - just a general idea! If your world already has some kind of visual design language being used, this is a great opportunity to expand on that!

<img width="720" height="416" alt="Concept Sketches" src="https://github.com/user-attachments/assets/2daff30f-9ba3-4d92-84a3-1187ea23f6c1" />

Consider things like: mood and vibe, color palette, and where and how often the plant is going to be used in your world. Is it a unique asset, or do you want to reuse it around the world? This will help you decide on what size and shape your plant should be.

Intended placement is key! If your plant is destined to go in a corner, nestled against some rocks, growing along a cliffside, etc, these factors are important to know so that you can design the plant to minimize clipping through surrounding assets. 
<img width="720" height="416" alt="Visualizing Placement" src="https://github.com/user-attachments/assets/54eee2ec-0d75-4730-8636-5251ccabbdc5" />

## References
Once you know the general type of plant you intend to make, it’s time to find some reference! I’m going to look for references based on color and shape. I’ll be using the very first shape above as my intended plant, and I want something that’s themed for a darker color palette - enchanted, maybe magical? 

With a quick search for “dark plants,” I was able to easily pull together several images that fit the mood of the plant I want to make: 

<img width="720" height="416" alt="Dark Plants Moodboard" src="https://github.com/user-attachments/assets/f30ba28b-5d54-4ba8-8fd4-5a4a58f8bedf" />

## Textures

Because plants are organic shapes that can be a beast to UV unwrap after the meshes have already been shaped and duplicated many times, I find it is usually easier to work in “reverse order” with plants. This means we are going to *start* with creating a texture first, and then create the mesh to fit it afterwards. 

Since we’re creating a stylized asset, I am going to hand-paint my textures. The exact steps I am following will vary between different software and device pairings, so I’ll be showing this process as a progression rather than literal specific instruction. 

If you want to try to follow along, I suggest using a tablet with a pen stylus that supports pressure sensitivity. A pen tablet (such as a Wacom) connected to your computer and a program like Photoshop would be the standard, but any device/app that you can draw on and get the results onto your computer will work. I am using a Samsung Galaxy Tab with the Sketchbook app, and transferring my images to my computer via Google Drive. 

### Identifying Needed Components

The first step is to decide on how many unique parts and variations my final plant will need. You can think of this like a checklist: leaves, stems, flowers, etc. I suggest having at least 2 different leaf variations to avoid too much visual repetition - things like shape, size, and color can be varied slightly between them for a more natural appearance. 

I’ve decided that I’ll need **leaves**, **flower petals**, and **flower buds** as my main components. I have three variations of both leaf and flower petal, and a generic shape that I can use for the flower buds. The colors are just a starting point so that I can get basic shapes in, and refine the color palette as I add detail later.

<img width="256" height="256" alt="image" src="https://github.com/user-attachments/assets/6bc6ef39-19dc-4448-b74b-c3c4be922d4e" />

I’ve specifically not included any stems, as the stems for this type of plants very closely match the leaf, so I can just reuse areas of the leaf texture for that. On a plant where the stems are distinctly different, I’d include additional textures for those on here as well. (For example, something with woody stems like a bush or a tree.)

The next steps are to add in my base detailing:
* Simple shading and shadows
* Highlights and contours
* Central veins
* Overall color adjustment

<img width="1024" height="256" alt="image" src="https://github.com/user-attachments/assets/42ca8052-6266-4874-86d8-67cf368e39f0" />

My final detailing step is to add a contrasting border around the outer edge of the leaf:

<img width="256" height="256" alt="Final Texture" src="https://github.com/user-attachments/assets/106b594e-cff2-4f8f-b8d2-62f2348a9bcd" />

### Artistic & Design Notes
* For performance reasons, we will **not** use transparency. The overdraw caused by rendering transparency is very expensive to calculate, and according to the official Horizons documentation, should be avoided whenever possible.

* I've extended the color of the leaves and petals into the background. This serves two purposes:
  * Working with rough polygon shapes, this compensates for the fact that our leaves won't be a perfect match to the outline painted. If we cut a corner, literally, then the color appearing on the mesh will still match the texture.
  * The official Horizon documentation recommends 32 pixels of padding around UV shells to compensate for mipmapping.
 
* When painting values that represent light and shadow, using a layer blend mode like "overlay" or "multiply" with adjusted opacity can be helpful to ensure that all values on the texture are adjusted accordingly. Otherwise, value inconsistency can cause shadows and highlights to be visually misinterpreted as base color values rather than *adjustments* to those base color values.

In accordance with the Desktop Editor workflow, make sure that you’ve saved your texture with the “_BR” suffix and in PNG format. (For example, Plant_BR.png) Note that BR textures do not support traditional transparency, as the opacity is instead reserved for roughness. (Since we don't need transparency, this also allows for a simpler shader setup with fewer textures needed.)

## Adding Roughness

As mentioned above, the opacity of our _BR texture is going to be reserved for the roughness map. It would obviously be difficult to paint the transparency into the texture while creating it, so I suggest doing this as a separate step after the base colors are completed. 

I will be using Photoshop for this process in order to utilize layer masks and the curves editor.

The first thing to note is that a PNG image coming into or out of Photoshop does not support a traditional alpha channel, but rather, supports transparency directly within the pixels of the image itself. Utilizing a layer mask is the easiest way to access and edit this transparency with a value-based visualization.


