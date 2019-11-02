# JELLY IS STICKY VERSION HISTORY

## v0.5.2
November 1, 2019

This is a minor release for the Indie Megabooth submission. Some features (such as postprocessing) I'm working on for v0.6 is turned off for the time being.

### New Features
* Particle effect has been implemented.
    - Color interpolation in CIELCH color space have been implemented.
    - Particle spawn position/speed/size/lifespan distribution, acceleration, default emission rate and color tint gradient can be adjusted during run-time at F4 > Mown > Particles.
    - Particle system is still work in progress, and is only used for doors at this moment.
* Postprocessing has been implemented.
    - The whole scene is now rendered with HDR.
    - Multisampling has been enabled for postprocessing.
    - Tone mapping has been implemented and its parameters can be adjusted in F4 > Mown > Graphics.
    - In order to use postprocessing, Jelly now requires OpenGL ES 3.1 instead of 2.0. Renderer fall-back has not been implemented yet.
    - Postprocessing is disabled in the configuration, as this feature is not well tested yet. To try it out, edit postprocess_fragment.glsl and config_default.yaml.

### Changes/Bug fixes
* Meta level structures have been completely revamped.
* Number of levels in the main game have been adjusted based on feedback.
    - "Middleman" and "Get in There!" have been removed from the main game.
    - "Moving Walls" and "Move Over" have been changed.
    - "Three Sticks" and "Fat Coconut" have been added to the main game.
* There is a new level pack, which is the collection of all old and rejected levels.
* Wire power up now accelerates and guarantees completion within constant time.
* Level preview no longer pops up right after exiting from a level.
* Culling has been implemented for rendering performance on large levels.

## v0.5.1
August 26, 2019

### Changes/Bug fixes
* Door and wire power up with animation at level begin when coming out of a fresh solve.
* Added a new world for footage shooting.
* Replaced the first meta puzzle.
* Changed behavior of UI when a level is solved. It now asks you in a modal whether to continue or stay.
* Loading a save now places you back at the door you entered last in the overworld.
* Fixed a bug where jelly geometry intersected when moving against another jelly due to jiggling.
* Fixed a bug that made level preview sizing and positioning weird with UI scaling.
* Fixed a bug that introduced one frame of delay for level preview positioning and content.
* Fixed a wrong mesh in one of the marching square cases.
* Fixed a bug where editor lost track of coconut index if a fruit goal was drawn below.
* Renamed the release file name to "Jelly is Sticky" as well

## v0.5.0
August 25, 2019

This is the biggest minor release yet. This version has hundreds of new levels, a whole new structure and mechanics for navigation between levels and meta puzzles, a level editor built for shipping, and graphics update on top of that.

Next focus is to do another pass on graphics: environment design, burner graphcis, new goal sprites, experimenting with shadows and reflections, and so on. Marketing will be another focus. This includes finalizing the name of the game, making an announcement trailer, Steam page, website, social media accounts etc.. More levels will be continued to be made and tuned as well.

### New Features
* Temporary level selection screen is out and meta level structure is in!
    - Progress through the game by solving child puzzles and thawing licorice blocks.
    - Level solve no longer takes you back automatically. You can review the level from here by undoing without losing progress.
    - Camera can now zoom in and move around with your jelly. They only work in meta-levels with single strawberry smilies.
* Over 100 new and updated levels!
    - Elyot made levels throughout June and July at a constant pace, contributing nearly hundred levels.
    - I also made dozen or so levels.
    - There are also some new meta levels.
* A level editor has been added
    - Press F6 to enter the editor from any levels
    - Blocks and tiles can be placed using pencil and rectangle tool.
    - Levels can be resized simply by drawing/deleting blocks/tiles.
    - Implemented mouse picking.
    - Editor has its own camera logic. Mouse scroll to zoom in and out. Space+left mouse or middle mouse to pan. Direction keys to move the camera.
    - Child levels can be added or deleted within the editor using the third tool.
    - There is no copy/paste as of yet. I might add this later.
* More graphics update!
    - Dynamic point light sources have been implemented. You can play with them using F4 > Jelly > Lighting.
    - Point lights are also used in level doors. Lights on unsolved doors pulse.
    - Floor and walls are now using color and normal textures.
    - Lighting and materials have been tuned again to fit with these changes.

### Changes/Bug fixes
* Changed name of the game to "Jelly is Sticky". I think this is the name that sticks with me the best so far.
* Removed the restriction on the number of smilies. Keeping track of number of smilies got tiring with the addition of the editor so I just got renderer to handle arbitrary number of eyes.
* Changed the behavior of input buffer. Instead of storing long sequence of buffered inputs, it now only stores one future directional input, which gets overwritten if another input is made.
* Above change also happens to fix a critical bug that crashed the game immediately when more than 256 directional inputs were buffered.
* Changed behavior of mouse interaction with UI. Only one UI can receive mouse input, and that input gets intercepted so that it doesn't leak below to gameplay code.
* Added user facing error messages. Try pressing options menu in the title screen to see this. Same system is also used to congratulate players when a level is solved.
* Undo history stack is taking up little more memory than the last version for half the size, because game state now comprises many more things to support editor undo. I'm thinking of adding compression later, but I need to farm usage data (just from myself) to build an offline Huffman tree.
* Fixed a bug where inverse of 4x4 matrix was transposed (this code had no coverage before mouse picking, so it wasn't tested well).
* Fixed a bug where jelly jiggle speed did not get preserved on the frame when jelly crossed the marching square transition threshold.
* Jelly movement code has been completely refactored as I added the editor. It is now much more defensively coded. The old code may have had potential to crash with an extremely long frame (like in seconds) although it might have been fine.
* Draw calls that contain zero triangles are no longer sent to GPU.
* YAML token limits have increased to 16384.

### Known issues/bugs
* Text UI component leaks memory whenever a new text is assigned. One could make the Mown allocator panic (thus crashing the game) by adversarially repeating certain inputs for an hour.
* The square licorice unthawing "dock" shows rendering artifact when moving.
* Jellies can intersect due to jiggle. This wasn't much of an issue before, but it is now very apparent when moving up against licorice.
* Level editor sometimes have trouble keeping coconut blocks intact. Draw it over again as a temporary fix.

## v0.4.0
June 9, 2019

Most noticable change is the look of the jellies. Adjustment to lighting and normal were made, and jiggle physics was implemented to sell the "jelliness". Android builds are now playable again.

Next focus is to work on title screen and world/level selection screens, and the associated meta puzzles. I'll also spend time on smoothing out the experience on Android. Level editor has been requested by some people, so I'm adding that as well.

### New features
* There was a second major aethetics pass on the look of jellies.
    - Lighting has been changed to directional from point.
    - Normals have been angled at jelly borders to create more distinct diffuse and specular.
    - Materials have been adjusted to fit better with these changes.
    - Normal offset textures are applied in order to avoid artifacts arising from the inevitable diagonal asymmetry of triangulation of jelly mesh.
* Jiggle physics have been added to jellies.
    - Jelly jiggles randomly on level start, reset, undo.
    - Smilies put jiggling force on itself when it attempts to move, even when it cannot move.
    - Jiggles propagate to neighbouring jelly blocks.
    - Jiggling is exaggarated on eyes.
    - Mown Engine now has a pseudorandom number generator. It uses a multiply-with-carry generator. It is able to pass TestU01. RNG is used to generate jiggles.
* Android build has been released, although the experience here is far from ideal yet.
    - Current control is to gesture a direction. Keep holding to continue moving in the same direction.
    - Android back button is bound to back button in jelly.
    - Save file location is moved to a proper place. It is "C:\Users\{YourUserName}\AppData\Roaming\drhee\jelly\" on Windows, "/home/{YourUserName}/.local/share/drhee/jelly/" on Linux, and "/data/data/org.libsdl.app/files/" on Android. Org name and app name will likely change in the future.
    - Proper shutdown sequence of modules and SDL is executed now, to appease Android.
    - For now, UI scaling exists, but is very preminary.
* This versions includes 19 new levels that were made by friends for a puzzle party on June 9.

### Changes/Bug fixes
* "Sheared edge" marching square case generated wrong border mesh. This is fixed.
* File saving implementation has changed from using cstuio's FILE to using SDL2's SDL_RWops.
* Fixed a bug where input buffer carried one move over to the next level.
* Fixed a bug where YAML serializer did not treat whitespace correctly if a dictionary was an entry of a list.
* Fixed a bug where setting a value of Mown dictionary with an existing key ended up with duplicate entry (can't believe this bug stayed undetected this far!)
* Fixed a bug where a Mown dictionary with exactly 5<<N entries did not insert the last entry (somehow my container tests missed this!)

### Known issues/bugs
* I'm having an enormous difficulty setting up Linux on my machine to run GPU accelerated programs. It seems to be a driver issue I just cannot resolve. As a result, the quality of the Linux version is still not clear.
* Android version is still very priminary and has many problems, which will be addressed with high priority.
    - Every other run of the Android build results in a crash. Some state from OpenGL context is persisting, even though I am destroying the context.
    - Touch release is sometimes not registered on buttons.
    - Sound playback is delayed.

## v0.3.1
May 19, 2019

### Changes/Bug fixes
* F11 fullscreen button is tentatively changed to only change window size and position to fake a fullscreen. This button doesn't even do borderless change and it must be set in F4 > Mown > Config. I just hate that fullscreen situation in Windows is worse than horrific.
* Frame drop logging can be relaxed in the configuration.
* Level loader now checks whether the block layer and the goal layer specified the same walls. Failing to do so was breaking checkerboard floor pattern in "TCAF bonus Poke" level.
* glEnable(GL_MULTISAMPLE) is gone. OpenGL ES 2.0 does not support that enum.

## v0.3.0
May 17, 2019

This is a small minor release. It adds a new gameplay feature: burner. It also has dozens of new levels created before and after TCAF, some using the new mechanic.

Level design will continue to be the focus, but 

1. finishing up Linux and Android version
2. fiddling around with graphics (messing with light and normals to have more clearly defined diffuse and specular) 
3. implementing title and world/level selection screen

are all in works as well.

### New features
* New gameplay mechanic: burner (actual name/graphics pending). It destroy jellies that step on it.
* As a consequence of burner, coconut code had to be changed:
    - Burner can fragment a single coconut chunk into a multiple chunks.
    - More than 10 chunks of coconuts can now be specified in a level. Thanks to the 4 Colour Theorem, you can specify any levels with coconut you want.
    - Coconut chunk index is kept tracked by the jelly control module.
    - Coconut chunk index is kept tracked by the history.
    - Coconut rendering is now O(1) instead of O(N) in terms of number of coconut chunks.
    - Coconut movement is now O(1) instead of O(N) in terms of number of coconut chunks.
* Couple dozen new levels!
* Added fullscreen (F11) and save-wipe (F8) button.
* Individual OpenGL calls can be logged for debugging (mostly added to figure out the Linux version crash). Press F1 to dump all OpenGL calls for a frame. Add "debug:\n  openGL_startup: true" to the config file to dump all OpenGL calls at startup.
    
### Changes/Bug fixes
* Adjusted camera zoom logic to behave better. Added camera_correction field to level yaml.
* Fixed a bug where pressing a direction button on the frame when jellies arrive at an integral coordinate buffers the input twice.
* Fixed a bug where hovering over a button with a mouse prevents the hotkey from working.
* Fixed a bug where having trailing whitespaces in the last row of blocks or goals of a level gave incorrect error message.

## v0.2.1
April 30, 2019

### Changes/Bug fixes
* Acceleration has been adjusted to allow about 50ms more time before the first movement is repeated. As a result, the movement becomes little more floaty than twitchy.
* Buttons can now be repeated on hold. This is used on the undo button.
* Changed one of the undo hotkeys from ctrl+Z to Z
* Added testing for various screen resolutions.
* Changed the version history file to markdown.
* There was a small refactor to remove old movement code. This removes the move cooldown field from the jelly > control dev tool.
* Fixed a bug where movement would snap to position when arriving at an integer position and lose the excess speed for that frame, resulting in a jerky movement.
* Fixed a bug where acceleration calculation did not factor in delta time.

---------

## v0.2.0
April 26, 2019

This minor release is the result of wrapping up most of major techinical work needed before shipping. We have most of the rendering tech needed, most of work on compilations to all the intended build targets, and first round of iteration on gameplay look and control.

In terms of aethetics, I experiemented with the look of jellies. I have decided on orthogonal camera with raised block. There is still a lot of polishing to do, but general direction is set.

Next focus will be on gameplay. I'm hoping to pump out a lot of levels and come up with a compelling slice for the presentation at TCAF on May 11-12. I'll also be putting in a proper title/world selection/level selection screen.

### New features

* Jellies have a new look! They have round edges with border and they are now 3D prism shape. They have Phong materials attached to them, which can be changed around by pressing F4 > Jelly > Color.
* Jellies now move continously instead of discretely. Input gets buffered in order to not drop input.
* New camera is orthogonal projection. You can control/switch the camera by pressing F4 > Jelly > Camara.
* Jelly gameplay, rendering code is refactored to clean up after various experiements.
* YAML serialization has been implemented. As a consequence, game progress and configurations can now be saved.
* A few new levels are added. They have been arranged into coconut and multiple smilies intro worlds.
* Jelly Factory can now be compiled to x64. I'm very close to getting Linux and Android working as well.
    
### Changes/Bug fixes
* There is now a limit on level size of 4096 after padding 1 on each direction (to keep render time/history stack size reasonable). At most 128 jellies can be controllable (to draw all eyes in one draw call). At most 10 coconut chunks can be placed (because I can't think of good scheme to specify it in ASCII in general, and it also affects update/render time). History stack is 1024 moves deep (to fit in memory budget). Maximum of 20 worlds are loaded, each with at most 20 levels (also for memory budget). These numbers are subject to change. The game will run fine if you violate these constraints (I added a lot of error checking to the level loader), but it will disable the level selection button for the offending levels.
* Undo has been reimplemented over to the new memory scheme. It can also now undo resets.
* Pressing F5 now refreshes the level selection screen, and keeps you on the same world.
* Level camera zoom is now determined smartly in order to fit within the HUD around it.
* Switched back grape blocks to blobs from individual blocks. Added more cases for marching squares because of this change.
* Normal mapping on jelly from the last version is unrolled for now.
* Jelly imgui menu is better organized.
* Images are now freed after it has been blitted into the atlas.
* Fixed a bug where renderer crashed if there were more than 65536 vertices in the jelly mesh.
* Fixed a bug where switching the camera in imgui did not change the camera position in shaders.
* Fixed a bug where changing the window title in imgui crashed the game.
* Fixed a bug where resizing the window did not resize the level.
* Fixed a bug where two key combination input actions never registered.

---------

## v0.1.0
Febraury 19, 2019

This minor release contains sweeping engine internal change and refactoring of the entire code. The previous code had been frankensteined from various old game engine experiments, so it was a mess. The refactoring is to solidify foundational code to make future development more mistake-free, productive, and enjoyable.

I'm also starting to experiment with the look of the game. Separation of rendering code, 3D rendering framework, marching squares, normal mapping, and Phong shading are implemented so I can start to mess around.

### New features
* Mown Engine now has its own allocator, list, hash table, and string implementation. All the engine and jelly code use this new allocator and containers, however SDL2 and imgui will make their own allocations separately.
* The entire program is now built in one compilation unit, in order to speed up compilation.
* Mown Engine now has input mapping feature. See the config file if you are interested in changing the input mapping.
* Marching squares is implemented to draw jellies with rounded corners.
* 3D camera/transform/render code is added. Press F4 -> Jelly -> view to play around with values.
* More levels using coconuts and multiple movable blocks are added.
* Game controller support have been now tested.
* The name of the game has been tentatively changed to "Jelly Factory".
    
### Changes/Bug fixes
* Built-in profiler is rolled back temporarily. In the next minor release, I'll refine it and put it back.
* A memory bug that often crashed the release build while loading levels at launch is fixed.
* Windows batch build can now build with log imgui window without crashing.
* ImGui offset was only doing half of the offset it promised. This is fixed.
* Keyboard and mouse inputs directed at ImGui no longer leaks below to the gameplay code.
* Movement should feel more tolerable for now. We will tune the movement more properly once the animation is in.
* Multisampling has been enabled.
* Text rendering should be better now. Glyphs were getting blitted into the atlas incorrectly, altering its pre-multiplied alpha value. I'm still not happy about the quality of the glyphs though. I'm pretty sure it's because stb_truetype doesn't support hinting. It's understandable that stb_truetype can't implement this in one header file; Truetype hinting is specified in a Turing complete programming language. I'm going to try switching to freetype sometime later.
    
### Known issues/bugs
* Some walls in a level may be missing a pixel.

---------

## v0.0.0
December 7, 2018

This is the first release version of Jelly Blocks (working name).

It's at a very early stage in terms of features or visual, but at least it's playable.

### New features
* This is the debut of Mown Engine, which provides services and modules for "Jelly blocks" game. It can do what most basic game engines can do:
    - make window
    - draw textures and texts on screen
    - play sound/music
    - get input from a mouse, a keyboard, and a game controller
    - serialize/deserialize stuff
    - and so on.
* Press F4 to open in-game "Dear ImGui"-based editor, where various aspects of the game can be viewed and tweaked.
* New block type added: Coconut. It sticks to nothing else, but it stays stuck together, resisting even shearing force.
* Multiple blocks can have eyes. They move simultaneously. Only the ones that can move will move.
* Various levels are playable:
    - Levels from the "Sticky Blocks" flash game
    - Some levels demonstrating newly added mechanics
    - Some test levels
    - a few previously unreleased levels
* Levels are loaded from asset/level/*.yaml, which can be edited to make your own levels. Pressing F5 in the level selection screen reloads these files.

### Known issues/bugs
* Avoid using non-ASCII characters anywhere for now. Unicode support hasn't been implemented yet.
* If the imgui editor has blurry text, turn off FXAA in your GPU setting. If it still looks bad, try adjusting imgui_offset in the "Mown - Config" window to either (0.5, 0.5) or (0.375, 0.375). See https://github.com/ocornut/imgui/issues/32 for more detail.
* Audio module decodes midi files, but doesn't seem to play anything for some reason. I won't work on this, since I don't plan to use midi files anywhere for Jelly Blocks game.
* Tree UI for performance profiler has incorrect collapsing behavior when new profile item is added or removed. I know what the problem is but I don't have a good solution for it yet.
* Yes it takes 0.5 seconds on my machine to start-up "windows" module. There is nothing I can do since my NVidia driver is taking that long to get back to me with a pixel format. See https://hero.handmade.network/forums/code-discussion/t/2503-%5Bday_235%5D_opengls_pixel_format_takes_a_long_time for more detail