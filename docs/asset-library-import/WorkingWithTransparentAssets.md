<!-- The title of your document -->
# Working With Transparent Assets

<!-- Put your name, at least your Horizon Name, as the author -->
Wojciech Lorenc (voytek.lorenc)  
<!-- IMPORTANT: Put the date this document was last updated! This is
important information for people to tell how 'stale' this info might 
be.-->
September 1st, 2025  

## Introduction

<!-- This section should describe what this document is going to cover. Try to provide some background and motivation as to why a creator would want to read your document. -->

This tutorial introduces a foundational workflow for importing semi-transparent assets into Horizon Worlds. As a case study, we will demonstrate the process by creating a sheer curtain and refining its transparency settings.

[PHOTO]

### Prerequisites and Expectations

<!-- This section should indicate any expectations you have of your readers, such as other materials or concepts they should already be familiar with in order to get the most out of your document. -->

This tutorial assumes a basic familiarity with Adobe Photoshop, Blender, and the Horizon Worlds Desktop Editor.

### Document Organization

<!-- This s an optional section, but possibly useful if your document has unusual document structure, or needs a table of contents with internal links because it is very long. 

Note that github automatically creates a clickable Outline from your section headings. Make sure you properly 'nest' your headings by using ##, ###, ####, #####, etc for sub sections so that the outline has a good hierarchy and makes navigating your document easier. I recommend only using # for the initial title, as the font for H1 renders very large. -->

This document has three main parts, covering texture prep, model prep and importing. Additionally there is a reference section at the end. 

* [Topic One: Preparing Your Texture in Adobe Photoshop](#topic-one--preparing-your-texture-in-adobe-photoshop)
* [Topic Two: Preparing Your Textured Model in Blender](#topic-two--preparing-your-textured-model-in-blender)
* [Topic Three: Importing Your Model to Horizon Worlds](#topic-three-importing-your-model-to-horizon-worlds)
* [References](#references)

## Topic One : Preparing Your Texture in Adobe Photoshop

We’ll start by creating a 2K (2048 x 2048 px) document.  

[PHOTO]

Add the image of your choice.  Here I pasted a photo of an actual curtain that I plan to recreate in 3D.  

[PHOTO]

Using the Opacity Slider in the Layers Window, set the desired transparency value.  In practice you might need to come back to this step as you iterate on your asset.

[PHOTO]

Export a transparent PNG file of your texture and name it MATERIAL_BA.png

File>Export>Export As>
Format: PNG
Transparency: Checked

![OG MHCP](../../images/MHCP_OG_image.jpg)

## Topic Two : Preparing Your Textured Model in Blender

Open your 3d model in Blender.  

Appropriate naming of the material is a crucial step of this workflow.  Make sure that your material is named MATERIAL_Blend

[PHOTO]

Import MATERIAL_BA.png (created in the previous section) and connect it to Base Color in Principled BSDF

Using the UV Mapping tools assure that the material is placed on your 3d object appropriately. 

[PHOTO]

Export your 3d object as an FBS file.  
Select your object and go to File > Export > FBX
Here make sure to select Selected Objects, Mesh, and Apply All Transforms

[PHOTO]


I named my file curtain.fbx


## Topic Three: Importing Your Model to Horizon Worlds

Open the Horizon Worlds Desktop Editor, click on Asset Library, and navigate to My Assets.
Once you select the desired location click on “Add New” and choose 3D Model

[PHOTO]

In the Import Model(s) window, click on “+ Choose files on your device” and select the files you saved in TOPIC 1 and TOPIC 2: MATERIAL_BA.png and curtain.fbx

[PHOTO]

Once the Desktop Editor finishes processing your asset, you should be ready to use it in your world.

[PHOTO]

If you are not satisfied with the transparency value, return to Step 1, adjust the opacity in Photoshop, and export a new version of MATERIAL_BA. Repeat this process as needed.

## References

<!-- this is the place to put useful supplementary information, such as references to other websites or documents in the github repo that are relevant to your topic -->

- https://medium.com/shecodeafrica/a-guide-to-technical-writing-7efcd0e70166
  - an article on writing good technical documentation
- https://docs.google.com/presentation/d/14pFo4zP9LvEP5-bG9i-iwCVK0kyMZwrl5VuuxEwtHJI/edit?usp=sharing
  - slidedeck presentation of "Fast-track your Docs with GitHub Templates" Build Along Workshop
