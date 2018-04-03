# PiFlex
8 bit greyscale camera using Raspberry Pi 2 model B

This software is intended to replicate the experience of using a super/standard 8 camera.

I had long dreamed of creating a super 8 cartridge with a small digital image sensor and recording power cammed to the original camera's crank. I'm sure this is possible now using a raspberry Pi zero W, but as it was early 2015 when I began this project and the Pi W did not yet exist, I went in another direction and built an entire interchangeable lens cine camera with all realtime anamorphic desqueeze, focus peaking, multiple exposure, backwinding, trigger start/stop with cable release, intervalometer, fully uncompressed greyscale video and real mechanical controls for all the functions found on real super 8/standard 8 cameras. 

I guess you could say this is like a low rent 8mm/8bit digital Bolex camera. It is not 4k or even HD. However the uncompressed video makes up for the lower pixel count, as does the sheer joy of using a camera one never needs to go into a menu to use properly. As it stands, the camera does implement all the functions I missed using the dslrs and mirrorless cameras within my budget. It needs streamlining however before I could say it would be anything like a simple project. It is not.



Features:

Multiple exposures
Multiple framerates
Live Anamorphic desqueeze for various aspect ratios

Hardware:

The prototype was built into a Zenit Quarz 8S-2 clockwork super 8 camera which is one of the only interchangeable lense 
super 8 cameras following the cine lens standards C and CS mount. A C to CS mount adapter is required for using the fantastic and fast C-mount zoom lenses available. 

It includes dedicated rotary switches for:
- Framerate

  -- 6fps
  -- 15 fps
  -- 20 fps
  -- 24 fps
  -- 48 fps
  -- 72 fps (without live preview)
  
  All frame rates record images at the same resolution and aspect ratio to allow multiple exposures 
  over different frame rates.
  
- Mode:
  -- Super 8 (continuous recording while trigger button is held)
  -- Intervalometer (with frame integration)
  -- Stop Motion (single frame triggered by cable release)
  -- Playback (fps control works in playback too, and the video can be reversed)
  
- A rotary encoder with switch for menu navigation and scrolling framewise through the recorded video, setting in/out points etc.

- A dedicated record trigger with working cable release.
  
- On/Off switch.

- Viewfinder either recycled from an old VHS-C camcorder or a pair of video glasses (Kopin type) with composite input.
  I used a small aluminium plate with slots for cable ties to attach the viewfinder.
  
  These hardware features are connected to the Pi by small pieces of stripboard with dupont pins, but I will get around to designing a proper Pi hat for this eventually.
  
  The camera operates on two 18650 cells and can be recharged during us with the addition of a seperate power control pcb.
  
  I am in the process of designing a dedicated case and lens mount for this camera which will integrate all the functionality of the prototype.
  
  I refuse to build in a flip out screen, this would detract from the experience and whole reason I built this camera in the first place, though it is of course possible to use an external HDMI monitor by plugging it in before power up. The viewfinder is automatically disabled in this case.
  
  The original lens of the Raspberry pi must be removed, a simple procedure. small shims are required for lining up the camera sensor with the external lens. I have used a small pcb in the prototype to mount the sensor where the gate reduction lens went in the super 8 camera.
  
  Software:
  
  The software is a mess as is. I am not a trained programmer but have been coding since I was a small child. It is haphazard and very optimised for speed and works as intended for the most part. That is not to say it could not be improved.
  
  The camera outputs uncompressed greyscale TIFF image sequences which are much nicer to edit and grade than nasty compressed h264 or other formats. 
  
  Live view features are:
  
   - Focus peaking
   - Realtime anamorphic de-squeeze
   - 'Film' loop readout
   - Realtime multiple exposure view.
   
   Menu features:
   
   - Save current loop
    Image sequences are saved in a folder named by current date/time and are named ditto with frame number also.
   
   - Text shader. 
    I am quite proud of this work. Eight character strings are converted to an RGBA texture of 8 pixels on a single line. Ascii character numbers are characterised as color values stored in the red channel. A seperate bitmap font is fed together with the scaling information to the text shader which extracts the color information out into the correct location on the bitmap font. The rendering is very fast and can be done many times over without affecting performance. The live view works in all modes except 72 fps and Playback of course. 
    
    - Film grain effect
      Not so great but there and realtime.
    
    - Many more I can't remember
    
   
   There is no shutter speed control. As this is supposed to be a simulation of a real chemical/mechanical camera system, the shutter speed is locked as closely as possible to twice the frame rate.
   Most of the controls needed for working with the camera are implemented in hardware. 
   Changing the aperture on the attached lens will not trigger the automatic gain in the Raspberry Pi camera sensor as I have found a hacky way to lock it, so this camera is as manual to operate as a true super 8 cine camera.
   
   Much of the work would have been impossible without the use of the PiCam library by Wibble82. 
   
   ToDo:
   
   I have been trying on and off to return to outputting DNG sequence files which will open in Davinci Resolve. This used to work but something in one of Resolve Free's updates broke this functionality, so I reverted to TIFF sequences which will open.
   
   Saving of smaller sections of the film loop (memory) to sequence folders. The naming and some other details has me procrastinating about how to do that efficiently.
   There are functions which have been detached from the menu system such as the ability to split the image memory into 3 segments so that multiple exposures can be split back out into seperate image sequences. I removed this function because it did not conform to the spirit of the project and complicated things, but it might be a feature in future.
   
   - Histogram
    Unfortunately pretty necessary with 8 bit greyscale digital images.
    
   - Better memory manipulation. I want to query the OS and find out how much memory is realistically available for the film loop and use that instead of an arbitrary number of frames.
   
   - Perhaps a more seamless saving functionality. I run the user input code in its own thread/core, perhaps saving could work in the background too.
   
   - Better dark frame implementation. The sensor is noisy and has a definite pattern. As I have bypassed just about every automatic function of the camera sensor, this must be done manually.
   
   - Live Preview of 72 fps mode. If I can use the preview stream for that or perhaps neon optimise the multi-exposure code it might be possible.
   
   - Extend the text shader's GUI code to stitch 8 character segment into sentences automatically, for the purposes of a future tutorial mode. There are people who have never used an old movie camera.
   
   
   
   
    
   
   
   
   
   
   
  
  
  
  
  

