<!-- The title of your document -->
# Creating And Updating An Interactive (Scripted) Asset Template

<!-- Put your name, at least your Horizon Name, as the author -->
Metacrafters and voytek.lorenc
<!-- IMPORTANT: Put the date this document was last updated! This is
important information for people to tell how 'stale' this info might 
be.-->
September 10th, 2025  

## Introduction

<!-- This section should describe what this document is going to cover. Try to provide some background and motivation as to why a creator would want to read your document. -->

This tutorial guides you through the workflow for creating and updating an interactive asset template. To cover the widest possible range of use cases, we will work with an asset that includes multiple scripts, including a “SharedEvents” script that is not attached to any entities.

## Why use an Asset Template?
The primary advantage of using an asset template is the ability to efficiently update instances of an asset across multiple worlds. Rather than modifying the same asset individually in each affected world, you can update the asset definition once and then approve the changes in all impacted worlds.

![2d coutous assets can be used in horizon worlds](https://github.com/user-attachments/assets/86ac85c3-f296-4e6c-9199-f48c3091a026)


### Prerequisites and Expectations

<!-- This section should indicate any expectations you have of your readers, such as other materials or concepts they should already be familiar with in order to get the most out of your document. -->

Basic familiarity with Horizon Desktop Editor.


### Document Organization

<!-- This s an optional section, but possibly useful if your document has unusual document structure, or needs a table of contents with internal links because it is very long. 

Note that github automatically creates a clickable Outline from your section headings. Make sure you properly 'nest' your headings by using ##, ###, ####, #####, etc for sub sections so that the outline has a good hierarchy and makes navigating your document easier. I recommend only using # for the initial title, as the font for H1 renders very large. -->

This document has six main parts covering asset prep, creating an asset template, importing, updating, accepting changes, and unlinking the asset. Additionally, there is an advanced concepts section and a references section.  

- [Why use an Asset Template?](#why-use-an-asset-template)  
- [Topic One - Preparing Your Asset’s Elements Before Converting to an Asset Template](#topic-one---preparing-your-assets-elements-before-converting-to-an-asset-template)  
- [Topic Two - Creating an Asset Template](#topic-two---creating-an-asset-template)  
- [Topic Three - Importing an Asset Template](#topic-three---importing-an-asset-template)  
- [Topic Four - Editing the Template Definition](#topic-four---editing-the-template-definition)  
- [Topic Five - Accepting Asset Updates in Affected Worlds](#topic-five---accepting-asset-updates-in-affected-worlds)  
- [Topic Six - Unlinking an Asset from the Asset Template](#topic-six---unlinking-an-asset-from-the-asset-template)  
- [Advanced Concepts: Blend vs Transparent vs Masked](#advanced-concepts--blend-vs-transparent-vs-masked)  
- [References](#references)  

## Topic One - Preparing Your Asset’s Elements Before Converting to an Asset Template 
Make sure that you work with FBS (File-Backed-Scripts).  Full funtionality of Asset Templates is not guaranteed if you don't use File Backed Scripts. Create a parent object containing all elements of the asset. To keep your project organized and easily manageable, we recommend placing all elements of your asset within a single parent object.

[PHOTO]
 Connect scripts that are not attached to any entities. If your asset includes scripts that are not linked to any entities, such as a “SharedEvents” script, you must ensure the script is connected to an object. In this case, we recommend creating a “SharedEvents” empty object and attaching the script to it.

[PHOTO]

<img width="2778" height="1284" alt="why use 2d cutout assets" src="https://github.com/user-attachments/assets/5eefda17-08bb-47b8-8b94-ed4e634b6f42" />


## Topic Two - Creating an Asset Template

Select the parent object and choose “Create Asset” from the menu.
[PHOTO]

Fill out the Asset Name and Description and decide on the location of your asset.  Make sure to select Asset Template in the drop down box.
[PHOTO]

Click on Create.
[PHOTO]

Note that the SQUARE indicating a parent object turned into an icon indicating an asset.  Also, the letters turned from while to blue.
[PHOTO]



## Topic Three - Importing an Asset Template
 Bringing an asset into your world is a simple drag-and-drop operation. Drag the asset from your folder in the Asset Library and drop it into your world.

[PHOTO]

You may want to double-check whether the asset’s scripts depend on any specific script APIs, or if Custom Player Movement needs to be enabled in the Player Settings. Make adjustments as necessary.



## Topic Four - Editing the Template Definition

In order to edit the template definition, select the asset in your Asset library, and choose the “Edit Template Definition” option.

[PHOTO]

You will now be able to make changes to the asset definition.  Once you finish, click on the Save button.

[PHOTO]

Describe your changes and click on “Save & Publish”


## Topic Five - Accepting Asset Updates in Affected Worlds

Once you change the asset definition, the instances of that asset will NOT be automatically applied in the affected worlds.  You will need to visit each affected world, and accept changes there.  You can do so by clicking on the “View Available Asset Updates” button.

[PHOTO]


## Topic Six - Unlinking an Asset from the Asset Template
You may decide that you no longer want an asset in your world to remain linked to its Asset Template Definition. Unlinking the asset is simple: select the asset in the Hierarchy window and choose “Unlink Instance Root” from the menu.


[PHOTO]



## ADVANCED CONCEPTS:  Blend vs Transparent vs Masked

It’s worth noting that Horizon supports multiple methods of handling transparency, each with its own advantages and limitations:

### Blended (Unlit) Materials
	•	Do not receive or cast lighting or shading.
	•	Have no specular or reflection properties.
	•	The material name in the FBX must end with _Blend.

### Transparent Materials
	•	Allow light to pass through.
	•	Use a specular channel to control both specular and reflection levels.
	•	Support two textures, which provide finer control over PBR properties.
	•	The material name in the FBX must end with _Transparent.

### Masked Materials
	•	Control how two textures mix together.
	•	Respond to specular and roughness, but are always fully rough (roughness = 1).
	•	The alpha channel of the texture defines opacity (white = opaque, black = transparent).
	•	Alpha cutout occurs at 0.5, consistent with GLTF 2.0 and Unity defaults.
	•	The material name in the FBX must end with _Masked.


## References

<!-- this is the place to put useful supplementary information, such as references to other websites or documents in the github repo that are relevant to your topic -->

- https://developers.meta.com/horizon-worlds/learn/documentation/desktop-editor/assets/asset-templates
- Meta's Documentation Explaining Materials Guidance
