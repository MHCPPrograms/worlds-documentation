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

Once the texture has been opened, click on the Mask button in the Layer panel to add a white layer mask. This white mask means the image is totally opaque, as it is to start with, or full rough once imported into Horizons.

<img width="131" height="139" alt="Layer Mask Button" src="https://github.com/user-attachments/assets/0eb8823e-079d-43d2-b2e7-b6a78f27a07f" />

In order to edit this layer mask, hold “Alt” and then click on it. This will change the current mode from editing the image layer to instead editing the layer mask.Remember this shortcut, as we’ll be using it a couple of times!

<img width="545" height="380" alt="Viewing Layer Mask" src="https://github.com/user-attachments/assets/7fb61a4f-c66d-45a0-879b-aac603bfd352" />

To get a starting point that more closely matches our texture and isn’t just a solid color, I’m going to open the Channel palette (Window > Channels) and click on one to view it. I'm choosing the green channel - sort of at random, but also because I want something that has good mid-range values to start with.

<img width="128" height="143" alt="Channel Panel" src="https://github.com/user-attachments/assets/bac7cad4-ac1e-463d-b87e-ce3b0ccc9ee7" />

Remember, brighter values mean higher roughness and less of a shine, and darker values will mean lower roughness, and more of a shine. I’m going to pick the green channel, as it has a good value separation between the different elements of the leaves. With the green channel active, I’m going to press Ctrl+A to select the entire channel, and then Ctrl+C to copy it.

Next, I’m going to alt+click back over to the layer mask, where I will Ctrl+V to paste the copied channel into the layer mask. If we simply left-click back on the main layer itself, we can see now that the image has taken on some transparency.

<img width="549" height="371" alt="Image with Transparency" src="https://github.com/user-attachments/assets/d422c11f-7243-4270-b904-4d27013fa206" />

Now to actually adjust these values to our liking. The first of which will be the flower petals: I don’t want those to have any shine, so I am simply going to fill in that area with white. This will remove any transparency from this area, and will later also tell Horizons that this area is to be matte and not have any shine. 

Next, I am going to open the Curves editor via Image > Adjustments > Curves. This will allow me to easily select and edit individual values of the image (i.e. the light parts, the dark parts) separately from each other. In the bottom left corner of the Curves editor, there is a hand icon with some arrows - click on this to enable the interactive curves adjustment mode.

<img width="80" height="68" alt="Interactive Toggle for Curves" src="https://github.com/user-attachments/assets/f9c2278f-e0ff-484b-8771-f58d6df0f434" />

Now with this active, I can simply click and drag on any area of the image, and the corresponding value on the curve histogram will adjust accordingly. 

The first thing I’m going to do is simply click once on a gray medium-value area to create an “anchor point” on the curve histogram - this will prevent this value range from changing, and make it easier to isolate the lights and darks for further adjustments.

<img width="490" height="265" alt="anchor point" src="https://github.com/user-attachments/assets/d8f3f7f0-598d-4788-808c-288e3f41ac6a" />

Here’s how I’ve adjusted the curve: brightening the middle veins of the leaf, darkening some of the middle areas, and then brightening some of the variegation, keeping in mind that darker values will equate to gloss and shine. 

<img width="719" height="365" alt="Edited Curves" src="https://github.com/user-attachments/assets/1d1935bc-0f9d-42da-b221-73c67873ee53" />

The last thing I’m going to do is brighten the entire mask. I want the shine to be fairly subtle, so I’m going to use Image > Adjustments > Brightness/Contrast and further adjust the entire image, which will ultimately lower the amount of shine displayed in Horizons. 

<img width="185" height="185" alt="Adjusted Layer Mask" src="https://github.com/user-attachments/assets/5ade839d-be46-4769-aa87-032ce588a8f1" />

If we switch back to the main color layer, we’ll see that it now looks like this, with odd transparency - exactly what we want! Save this image, making sure that it’s PNG format, and again, with the “_BR” suffix. I also suggest saving a copy of this file in your application's native format (for me, .PSD) so that it can easily be edited later. Since we're essentially just guessing at the roughness values currently, it's likely that this may need some corrections once we see how it's applied. 

<img width="192" height="192" alt="Final Image with Transparency" src="https://github.com/user-attachments/assets/103c86b7-6076-43d0-98cd-3cea4c2985bb" />

## Mesh Creation

Onto the fun part - creating the mesh! For this next part, I’ll be creating my mesh using Blender. (Any software that can export .FBX can be used, though.)

Upon opening Blender and being met with the default scene, remove it all by press “A” to select all, and then press “Delete” on your keyboard. 

To start, let’s add a plane. (“Shift+A” and then select Mesh > Plane.) With the plane selected (it should have an orange outline - if it doesn’t, simply left-click on it) open the Material tab. This is the red ball icon on the panel to the right side of the screen:

<img width="109" height="50" alt="material panel" src="https://github.com/user-attachments/assets/bb442369-5a8d-45f7-8e9b-a818f0b4c6e7" />

Here, click the big “New” button to add a new material. A single material entry will be added into the panel at the top, simply named “Material.” Click on the box underneath that panel where the name is displayed, and we’re going to rename it. Remember, this material name you are assigning in Blender MUST match the name of your texture in order for Horizons to process your assets correctly. Since my texture is saved as “Plant_BR.png,” I need to name my material “Plant” to match. (Simply remove the texture-type suffix, in this case “_BR” to find out what the material name needs to be.)

<img width="222" height="176" alt="Naming the Material" src="https://github.com/user-attachments/assets/440a2d48-5c19-4e00-b0e2-1cbc31c06749" />

Then down in the material settings, find the entry for “Base Color” and click on the yellow dot next to it. This will open a menu - we’re going to change the material so that the base color value will use a texture instead of only a color. Select “Image Texture” as the type.

<img width="466" height="239" alt="Importing a texture into the mateiral" src="https://github.com/user-attachments/assets/f6dfda03-6949-428b-a88c-40339c90a837" />

Underneath that Base Color property, after setting it to an Image Texture, you’ll now have the option to “Open” a texture. Click on the “Open” button and select the _BR texture we created earlier. 

We’re going to repeat that same thing for the “Roughness” value - click on the gray dot to the left of the entry, and change the type to “Texture Image.” Since we’ve already imported our image, we can simply click on the image thumbnail dropdown to the left of the “new” and “Open” buttons, and then select our BR texture to reuse it. Because the roughness channel is a single value, Blender will automatically know to use the alpha channel.
 
Now in order to see the texture on the mesh, we need to change material mode to display the texture. We’re going to change the rendering mode to “Material Preview.”

<img width="220" height="70" alt="material shading" src="https://github.com/user-attachments/assets/70fd9861-3f49-4a06-af54-01a79ef10a02" />

This will now allow you to see a mostly-accurate representation of how your asset will look in the Worlds Desktop Editor with roughness applied. Keep in mind that it will not be a perfect 1:1 match, because the two programs are using entirely different rendering engines - but it is extremely close. At this point, you may want (or have) to go back and make more edits to your alpha channel mask to correct the roughness as previously mentioned. 
