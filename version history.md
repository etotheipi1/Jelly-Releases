# JELLY IS STICKY VERSION HISTORY

## v0.9.0
August 2, 2020

This minor release adds a few more graphical improvements that were missed in the last version.

### New Features
* Shadows are now colored.
* Glitters have been added to jellies.
* Mouth and mouth animation added.
* Jelly has varying transparency depending on its z-jiggle.
* Vignette postprocessing has been added.

### Changes/Bug fixes
* Wall are jellies now! They jiggle on start, push, and click.
* Added 'More Bonus Levels' world with ~50 more levels.
* Some bonus levels have been minorly adjusted.
* Bloom performance has been improved by making the convolution kernel bigger and reducing the number of pingpong blur iterations.
* Face animation no longer initiates if the player is moving jellies around.
* Face animations have been adjusted.
* Fixed a bug that prevented saving a level from editor sometimes.

## v0.8.1
July 20, 2020

### Changes/Bug fixes
* Meta mechanics went through a design iteration:
    - Meta state is reverted to be remembered based per stack, for now.
    - "Get to the left" is no longer solvable with the new rule and is deleted.
    - Fixed a bug with 100% completion star, where it could spawn arbitrary number of jellies.
* Fixed a bug that crashed the game when the level editor was entered in 64-bit version.
* In the shape where three burners in a bent trinomino forming a square with a wall, burner now continues below the rounded corner of the wall.
* Added minimum time between two jelly fragments dropping.
* Minor change to "Worm yet again" bonus level.
* Fixed a bug that disabled level intro animation for all levels.
* Fixed a bug where changing size of a level in the editor broke spawn location.
* Fixed a bug that skipped jelly drop simulation on the first frame, resulting in synced drop for all jelly fragments dropped in the same frame.

### Known issues/bugs
* Preview is sometimes showing some jellies darker.

## v0.8.0
July 13, 2020

This minor release finishes nearly all graphical implementations needed before shipping. It also adds meta mechanics such as recursing levels and 100% completion stars.

### New Features
* Burner graphics has been added. It is depicted as a lava pool, with scrolling Perlin texture and particles.
* Vertical jiggling added. Jelly mesh can be squizzed vertically on click, drop, and movement. Normal is not modified yet.
* Added animation where jellies drop when levels begin.
* Added various animations for eyes.
* Meta mechanics have been added:
    - Meta state is now remembered based per level, not stack, which is a relevant distinction for recursive levels.
    - Meta levels now keep track the entering smiley, instead of red-eyed smiley. Spawn floor type has been added, along with various error checks regarding loading, saving, entering, leaving, and editing.
    - 100% completion star added. 100% completion wire power added.
    - Editor functions to support recursing levels and stars have been added.    
* A world for demonstrating meta mechanics have been added.

### Changes/Bug fixes
* Fixed a bug where the level preview was showing a wrong level if 1) entered the level editor 2) new level was assigned to a door 3) new level was entered within the editor 4) player got back to playing in the new level 5) and came back to the new level.

### Known issues/bugs
* Meta mechanic implementation is still in flux and still in develoment. There are known corner cases that feels wrong.
* Z-ordering on jellies are sometimes wrong when drop happens.
* Multi-resolution screenshot test is broken since postprocessing was introduced.
* Framerate can be low. Next minor version should have huge improvement on performance.
* Supporting undo for meta operations (entering and leaving doors) was planned but didn't make it in time.

## v0.7.3
March 19, 2020

### Changes/Bug fixes
* Fixed a bug where pressing reset twice blanks the level state.

## v0.7.2
March 17, 2020

### Changes/Bug fixes
* Depth of field strength was reduced. It is tweened down on level entry.

## v0.7.1
March 17, 2020

### Changes/Bug fixes
* Shadow map depth test issue has been fixed.
* Shadow map has been slightly expanded to always cover everything in view.
* Added a color grading step for postprocessing.
* More lighting constants have been tuned.
* Got rid of the snap zoom from the main level.

## v0.7.0
March 16, 2020

This minor release adds various graphical effects such as HDR, bloom, depth of field, and shadow mapping.

### New Features
* Postprocessing implementation has been completed.
    - Postprocessing works with multisampling.
    - Postprocessing works with screen resizes.
    - High dynamic range is implemented.
    - Bloom is implemented.
    - Fake depth of field is implemented. It doesn't actually measure the depth, but approximates it based on screen position.
* Shadow mapping has been added.
* Frame buffers can be viewed in the ImGui dev tool.
* State in meta levels are saved even after entering and leaving decendent levels.
* Snap zoom feature has been added: some "rooms" has fixed camera.

### Changes/Bug fixes
* Jelly jiggle behaves more smoothly under low frame rate.
* Various lighting constants have been tuned.

### Known issues/bugs
* Adding postprocessing has made the performance quite worse. I'll be working on optimizations soon.
* Shadow map currently has a depth test issue, which results in wrong shadow in some corners.
* Postprocessing has not been tested on Android, so it is turned off in Android version.

## v0.6.2
January 5, 2020

### Changes/Bug fixes
*  Added fallback to request a window with OpenGL context instead of OpenGL ES context, because on some machines, a window cannot be created with a OpenGL ES context (especially Windows with AMD graphics using WGL). I'm hoping to implement a proper fix using EGL or ANGLE in the future.

## v0.6.1
January 2, 2020

### Changes/Bug fixes
* Various level design/curation changes were made:
    - Mashup, Stag and Doe, Tetrominoes, Leash was given more room for maneuver.
    - Repel was given less room.
    - Deform, Pancake Die was iterated on.
    - Pick and Choose was renamed to Multiple Choice. Katamari was renamed to Cluster.
    - Orange levels were reordered.
    - Four more bonus levels from Elyot!
* Unreachable levels have been deleted from the main level file.
* Log is now appended to the existing log file, instead of overwriting it.
* Fixed a bug where entering editor screen for child level of Courtyard from Courtyard applied Courtyard lighting to the child level.

## v0.6.0
January 1, 2020

This is a minor release including a polishing pass on the level editor, jiggle physics, and movement code. Various meta levels have been adjusted and so did the curation of main levels. It also includes tons of small bug fixes. Postprocessing is delayed until the next minor release.

### New Features
* You can now fly in meta levels to cheat. Press F7 to toggle flying. Your jelly will go over walls and other jellies, and not stick to anything.
* Added a new tool in the level editor that allows you to quickly duplicate or delete row/columns. The hotkey '4' is bound to this tool.
* Added a button for entering editor screen for child level (before this patch, you had to leave the parent editor screen, move your jelly to the door, enter the child level, and then press F6 to enter this screen).
* Hotkey has been added to a few palette buttons:
    - 'R' for **r**ed strawberry jelly
    - 'B' for **b**lue grape jelly
    - 'Y' for **y**ellow orange jelly
    - 'C' for **c**oconut jelly
    - Press tab to switch to wall palette. If the wall palette is already selected, pressing tab switches the palette to floor tile.
* Jelly jiggle physics has been revamped.
    - Different jelly type have different jiggle parameters now.
    - Clicking on a jelly causes it to jiggle.
    - Orange jelly can be visually seen to be stuck to other sticky jelly.
    - Jellies now jiggle even when they fail to move but receives "pressure" from a controllable jelly.
    - Jelly jiggling propagation is now more physically accurate and behaves better than the hackier version before.
    - Jiggle force behavior when jellies start/attempt moving has changed to affect speed instead of position.
    - Straight edge jiggling behavior is changed so that the animation is continous even when marching square division changes.
* Restored grape-orange stickyness. Reverted all relevant levels.
* Added logging for entering/solving/editing level with timestamp (relative to when game started).

### Changes/Bug fixes
* If pencil tool is drawing coconut and started its drawing on top of an existing coconut, it now extends that coconut instead of overwriting it with a new coconut chunk.
* Deleting a blank cell with a wall pencil draws tiles.
* New level/rename level modal window now places focus on title textfield on open.
* Rename level modal window now populates the title textfield with the current title.
* Selecting a palette item changes tool to pencil if the current tool is 3 or 4.
* Pressing R in a meta level no longer brings up the level preview screen if the player started on a door.
* Android swipe input has been made slightly more sensitive.
* Added two more levels to the recycling bin (Minichess and Counting Gadget) because it was missing.
* Added test levels for lateral jiggling and power branching.
* Yellow-blue stickiness can now be toggled under F4 > Jelly > Control.
* Movement input buffer has been expanded back to hold 4 inputs.
* Buffered input now smoothly continue the last movement without staggering.
* Added logging for detecting unreachable levels.
* Fixed a bug where if you paint over a jiggling jelly with a wall, the wall gets the jiggling parameters and thus shows up with curved edges.
* Fixed a bug where if you solve a child puzzle, come out, and go into the editor, it loads the controllable jelly at the door.
* Fixed a bug where power-up sound played briefly even though it powered no power line.
* Fixed a bug where power-up sound played perpetually if the player left the level while the power-up animation is happening.
* Fixed a bug where pressing "enter" button made noise even when not standing on a door.
* Fixed a bug where pressing F6 on "solved" screen got one in the level editor but did not clear the "solve modal", so upon selecting "stay" one could control the jellies within the editor.
* Fixed a bug where the door enter input was dropped if the jelly was more than half cell away to the door.
* Fixed a bug where the door enter input was dropped in the time period of 150ms between arriving at a cell and level preview showing.
* Fixed a bug where the door color was sometimes incorrectly showing red on level preview.
* Fixed a bug where edit button in the editor preview did not account for changes made since last save.
* Fixed a bug where the configuration of multiple door powering a same set of wires would result in all doors turning green when one of the child level is solved.
* Fixed a bug where if you buffer a single movement input on the frame when jelly arrives at a cell, it moves twice.
* Fixed a bug where movement input was dropped during wire powering up.
* Fixed a bug where one could enter a level during wire powering up.
* Fixed a bug where cliprect didn't update when the game window size was changed in the level editor.
* Fixed a bug where middle mouse panning in the level editor on top of level preview had the camera jumping unpredictably.


### Known issues/bugs
* Jiggling system change brought out some problems in the marching square rendering and some discontinuity can be felt. Fixing these unsmooth animations is high on my todo list.
* Camera still jumps unpredictably if middle mouse panning is triggered on top of UI buttons. I understand the behavior but I haven't found an elegant fix yet.
* Placing more than 32 doors in one level crashes the editor.

## v0.5.3
November 5, 2019

There is a major game mechanic change that we are trying out. Blue jelly no longer sticks to orange jelly.

### Changes/Bug fixes
* Blue jelly no longer sticks to orange. Most levels have been adjusted to reflect this change.
* Many levels were re-balanced:
    - "Replace" has been made easier and is now called "Knead".
    - "Orange is Very Sticky" has been changed and is now called "Orange is Super Sticky".
    - "Expand", "Dig it Out", "Four Point Turn" has been made easier.
    - "Shear" has been made harder.
    - "Poke" and "Breakup" have been swapped.
    - Added walls for "French Curve" and "Keep it Alive".
* Camera zoom level is now consistent across different resolutions.
* Jelly lighting has been adjusted for dark levels, so that it is easier to tell them apart.
* Square bracket level browsing is back for testing purposes.

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