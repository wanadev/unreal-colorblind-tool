# Unreal colorblind tool

The purpose of this project is to provide tools and demo projects to easily adapt your game to various types of colorblindness.
It uses standard color lookup tables (LUTs) to help detect problematic colors schemes and bring your game's colorspace to one more suitable for people with colorblindness.

Most of the technical stuff is based on [Unreal's LUT tutorial](https://docs.unrealengine.com/en-US/Engine/Rendering/PostProcessEffects/UsingLUTs/index.html).

## Unreal demo project

### Try it out

Start the scene (based on the FPS template), and press the numpad keys to enable the various LUTs.

### How it works

- An unbound PostProcessVolume is placed in the scene, which will receive the LUTs.
- A Blueprint named "LUTManager" handles the LUT and UI changes. This Blueprint is only an example and you should decide how to implement the PostProcessVolume changes depending on your project.

### Caveats

The PostProcessVolume only allows one LUT at a time, and the volumes' LUT parameters are overriden one by another, so you can't use two LUTs at the same time.
This means you can't have an aesthetic LUT combined with and colorblind LUT, or combine a colorblind simulation LUT with a colorblind correction LUT to see how the corrected result would look to a colorblind person.

The most elegant workaround would be to create a post processing material to apply the LUT.

You could also create a combination of the aesthetic and colorblind LUT in photoshop.

## Photoshop Tool

### Structure

- Simulation LUTs : 3D LUTs made to simulate what a colorblind person would see for each type of anomaly. The most common are already placed in the PS file, others can be found in the folder next to it (with the percentage of people affected written in the title). Enable one at a time.
- Correction LUT : the various effects which should be applied to the correction LUT to make the important parts of the image distinguishable. Enable the whole folder.
- Test Pictures : the screenshots of your game that will serve as a reference.

### How to use

- Place screenshots of your game in the Test Pictures folder.
- Enable the simulation LUTs one at a time to check for colors turning out similar.
- Tweak/add effects in the Correction LUT folder to separate those colors to different visible ones. Selective correction works great, and adding contrast often helps.
- If needed, make a separate Correction LUT folder for each anomaly.
- When you're happy with your correction, open the neutral_lut.jpg file in a separate PS tab.
- Copy the whole Correction LUT folder and paste it on top of the neutral_lut file.
- Export the result to a new jpg file.
- Import the file in UE4 and place it in a PostProcessVolume's LUT slot ([see this tutorial for detailed steps](https://docs.unrealengine.com/en-US/Engine/Rendering/PostProcessEffects/UsingLUTs/index.html))

## Tips and tricks

- Warning ! The "simulation" LUTs are used to help people with a normal vision perceive the image as if they were colorblind. It does NOT fix the problem and should not be used in your final game.
- When your game mainly uses two colors, going for a blue and yellow replacement should do the trick for a large portion of colorblind people.
- When possible, do not only use color to convey meaning : patterns, shapes or text are great additions
- When possibile, let players choose their own colors on a palette for important information like teams, or positive/negative feedback.
- For more info, check out this video by GMTK about colorblindness and low vision : https://youtu.be/xrqdU4cZaLw