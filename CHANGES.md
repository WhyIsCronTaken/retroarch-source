**Core Updates**

FBNeo, LRMAME2003 Plus, UAE and VICE have seen the regular weekly updates/improvements. We can't list all the changes there, so we just suggest you go to the respective Github repositories and check out the chanes there.

**LRMAME**

LRMAME updated to version 0.242 (latest). LRMAME is now also available for ARM Macs now. You can get it from the Core Downloader.

**Nestopia**

FourScore support (4 player multitap) has been added for the following games:

    Spacey McRacey
    NNNNNN
    Arkade Rush
    Justice Duel
    BMX Simulator
    Way of the Exploding Fist 

**PCSX ReARMed**

This core has a new auto frameskip mode (based on free audio buffer space).

The Lightrec dynamic recompiler has been updated, and it should fix several crashes and bugs that occurred before. This would only affect users on x86/x86_64 and MIPS architecture processors, as ARM architecture-based systems continue to use the Ari64 dynarec instead.

There has been a GunCon overhaul, the following input descriptors have been added:

    Add Trigger, Reload, Aux A, and Aux B as mappable buttons in RetroArch menu for players 1 and 2.
    GunCon trigger, A, and B buttons are mapped to Gun Trigger, Gun Aux A, and Gun Aux B instead of hard coded to left click, right click, and middle click.
    Force cursor to corner of screen for offscreen reload so that reloading works on all four edges of the screen.
    Allow Gun Reload RetroArch input to emulate an offscreen shot.
    Switch gun coordinates from "Pointer" type to "Lightgun" type. 

**GW (Game & Watch)**

The GW (Game & Watch) Libretro core is now available for the MSVC 2005 and 2010 Windows versions. These versions can run on older Windows OS versions than the regular version.

**gpSP**

The gpSP Libretro core now uses a small translation cache for the Miyoo platform.

**Cap32**

An emulator of the Amstrad CPC 8bit home computer range. This has seen several improvements.

    DB: new games from retroachievements
    UI: added DB icon DSK to status bar
    DB: you could add direct tokens using $ (for joystick keybinds or cleans)
    DB: added DB v1 using clean-cpc-db info
    CORE: added model 664 to allow DSK and BASIC 1.0
    CORE: detect some configurations from filename
    VIDEO: minor fixes (requires more work) 

**SMS Plus GX**

The SMS Plus GX Libretro core should now be more stable on RetroArch PSP. We achieve this by avoiding unaligned memory access. Previously, after starting a game, the console would have a tendency to locks itself and shut down.

Other related changes - we replaced ALIGN_LONG with ALIGN_DWORD for Miyoo and RetroFW to match the standalone versions. This fixes Master System background rendering. It was dropped from 3DS as ARMv6 allows unaligned memory access and defining that macro had no effect anyway. ALIGN_DWORD was dropped from Raspberry Pi (ARMv6/7/8), Classic (ARMv7), OS X non-PPC (x86, ARMv8), Vita (ARMv7) and Switch (ARMv8) as those platforms support unaligned memory access.

**Beetle Virtual Boy**

Fixed a couple inaccuracies in the VSU modulation emulation, fixing a few sound effects in "Virtual Boy Wario Land".

**Mesen**

The Nintendo Entertainment System emulator core has seen a couple of improvements.

Before, the core would upload audio by using the audio batch callback multiple times per frame, unduly 'stressing' the frontend audio buffer and leading to poor AV synchronisation.

We now ensure that the audio batch callback is only used once per frame (unless the frontend does not support batches of sufficient size, in which case the samples will be split appropriately).

We also did the following:

    Sets the default audio sample rate to 48000 Hz. The previous default of 96000 Hz is so high that RetroArch is required to flush the audio driver twice per frame, which is bad for AV synchronisation.
    Removes the 192000 and 384000 sample rate options, since these are in fact unsupported by the underlying emulator code... 

Add 4:3 (Preserved) & 16:9 (Preserved) aspect ratios Mesen by default preserves the aspect ratio in all cases when cropping the overscan, which results in a difference between the core provided 4:3 and 16:9 ARs, and RetroArch's own 4:3 and 16:9 ARs, which doesn't always results in a ideal image (specifically 16:9 on a 16:9 display will look weird when cropping is applied).

We now separate Mesen's preserved 4:3 and 16:9 ARs into their own selections for the core provided aspect ratio so people can choose whenever or not they want the aspect ratio to be preserved when using either one of the selections as their core provided aspect ratio.

**bsnes Mercury/bsnes C++98**

The Super Nintendo Entertainment System emulator core has seen a couple of improvements.

Before, the core(s) would upload audio in packets of 64 samples - which means the audio batch callback is used multiple times per frame, unduly 'stressing' the frontend audio buffer and leading to poor AV synchronisation.

We now ensure that the audio batch callback is only used once per frame.
REminiscence

This Flashback game engine core has now been added for the Miyoo platform as well.

**ScummVM**

Several serious crashes should be fixed now as a result of us updating the libco coroutines middleware library.

**FCEUmm**

This Nintendo Entertainment System emulator core has seen several improvements.

More mapper additions and improvements Improve mappers 49, 215/258, 340, 341, 351 and 444. Add newly-(re)assigned mappers 294 and 310. Add new mapper 467.

Expose internal audio RF filter option The core already contains a low pass audio filter designed to recreate the 'muted' sound of the NES when connected to a television via the RF modulator - but for some reason this functionality is not enabled/exposed.

We have simply wired it up to a new Audio RF Filter core option. When enabled, the (subjective) improvement in audio quality is quite dramatic. The filter has a negligible performance impact.

(This filter produces the effect discussed here: https://forums.libretro.com/t/lowpass-filtering-for-nes-rf/37258)

Add optional 'fake' stereo sound effect We added a new Stereo Sound Effect core option which may be used to simulate stereo sound by delaying the right audio channel (relative to the left) when upmixing the mono output from the NES. The delay can be configured from 1 to 32 ms.

The effect is identical to the fake stereo currently available in the Mesen core.

**minivmac**

minivmac is an emulator for the Mini vMac, a miniature Macintosh. We added this core now for ARM Macs. It can be downloaded from the Core Downloader.

**Genesis Plus GX**

Genesis Plus GX is a Sega Master System/Sega Game Gear/Sega Megadrive/Sega Genesis emulator core.

We are using the low memory codepath now for Miyoo systems. As this platform only has 32MB RAM, like the RS-90.

**xRick**

The Rick Dangerous game engine core has been added for the Miyoo platform.

**Snes9x 2005**

This Super Nintendo Entertainment System emulator core has seen several improvements.

Before, the core had bad audio sample pacing:

    Neither variant of the core sent a number of samples per frame that would match the nominal expected values given by the sample rate and fps set in retro_get_system_av_info()
    Due to integer rounding errors, the non-plus core always would send too few samples
    The 'plus' version of the core would send the 'correct' number of samples, in terms of actual emulation - but this does not tally with the sample rate reported to the frontend. Moreover, the 'plus' core would call the audio batch callback twice per frame, which unduly stresses the frontend audio buffer. 

As a result, the core had bad audio/video synchronisation, affecting frame pacing.

We fixed several issues:

    The audio sample rate is now reported as 32040 Hz
    The non-plus core uses an accumulator to ensure that 'fractional' audio samples are accounted for and sent when required
    The plus core now uploads audio samples only once per frame 

In addition, we did the following

    Fixed three memory leaks that were found in the core
    Modified the Console Region core option to require a restart (since it has never been possible to change this at runtime...) 

Snes9x2005 Non-Plus: Add optional low pass audio filter Apart from a substantial difference in audio emulation accuracy, probably the most obvious difference between the 'plus' and 'non-plus' versions of the core is that the latter has an inadequate level of low pass audio filtering, leading to tinny/scratchy sound.

We added a simple optional low pass filter at the output stage of the 'non-plus' core. When enabled, audio is more mellow/bassy, and the generated sound is closer to that produced by the 'plus' version - with only a negligible increase in performance requirements.

**Snes9x 2010**

This Super Nintendo Entertainment System emulator core has seen several improvements.

Use audio batch callback only once per frame

Before, the core would upload samples in batches of ~64, which means the audio batch callback is used many (~9) times per frame. This 'overstresses' the frontend audio buffer and leads to bad AV synchronisation.

We have fixed the issue by ensuring that the audio batch callback is used to send all available samples only once per frame.

Improve save state efficiency + fix save state size

At present, every time that retro_serialize_size() is called (i.e whenever save states are used), the core determines the save state size by allocating a temporary 5 MB buffer and writing into this an actual save state. Moreover, it then fails to report the actual size correctly due to a bug in the memory stream wrapper code - which means save states are always 5 MB in size. This represents a terrible inefficiency.

Now, the save state size is now calculated independently of regular save state creation. No temporary buffer is required, and there is no need to actually write a save state to memory - and save states now have the correct size (~830 kb)

**SwanStation**

This Sony PlayStation1 emulator core has been updated.

    Remove 'Force Pop'n Mode' & 'NeGcon Steering Axis Deadzone' options 

60Hz modes for > 60Hz emulated platforms

Big improvements for WonderSwan, Lynx and PokeMini emulator cores for the majority of systems that don't happen to have VRR displays!

**Beetle WonderSwan**

At present the core runs at ~75Hz, matching the native refresh rate of the WonderSwan hardware. This is fine if the core is run on a VRR display (or one that natively supports 75Hz...), but on regular 60Hz panels it can cause issues. In particular, screen tearing is very likely to occur. You can experience this on Linux (when not using a compositor and without vsync forced at the driver level) and on 3DS. The tearing is so bad on 3DS that we would previously consider the core to be unusable on that platform...

We now added a new 60Hz Mode core option, which can be used to force the core to run at 60Hz (actually 60.38Hz, but RetroArch handles this nicely via dynamic rate control). Note that the core still runs at the 'correct' speed when this option is enabled - internally, the core is running the nominal ~75 frames per second, but every 5th frame is 'dropped'. This reduces video smoothness, but then 75Hz on a 60Hz display is not smooth either. More importantly, enabling this option eliminates screen tearing.

In addition, we have also made the following minor changes:

    The frontend reported framerate is now set correctly in 75Hz mode (previously this was truncated, leading to a slight tendency for the frontend audio buffer to under-run)
    The internal audio samples buffer has been reduced from a ~64kb (!) static array to a tiny, dynamically created array of just the correct size
    On 3DS, the video buffers are now allocated in linear memory (for improved performance)
    The 96000, 192000 and 384000 audio sample rate options have been removed, because they are nonsensical and harm AV synchronisation 

Thanks to this 60Hz mode, Beetle WonderSwan is now perfectly playable on RetroArch 3DS. We have enabled this option by default. If you are using a VRR display or if you are running at a native 75Hz resolution and would like to change it back to the native refresh rate, you can just turn this option off in Quick Menu -> Options.

We have also added the core for RetroArch PS2, although it can't reach fullspeed. It's debatable whether it's worth including, but for now we keep it in.

There is also a new optional audio feature. The WonderSwan has a tendency to produce rather harsh/abrasive chiptunes. The low pass audio filter softens and 'mellows out' the generated sound.

**PokeMini**

At present the core runs at 72Hz, matching the native refresh rate of the Pokemon Mini hardware. This is fine if the core is run on a VRR display (or one that natively supports 72Hz...), but on regular 60Hz panels it can cause issues. In particular, screen tearing is very likely to occur. We could experience this on Linux (when not using a compositor and without vsync forced at the driver level) and on 3DS.

We have now added a new 60Hz Mode core option (enabled by default), which can be used to force the core to run at 60Hz. Note that the core still runs at the 'correct' speed when this option is enabled - internally, the core is running the nominal 72 frames per second, but every 6th frame is 'dropped'. This reduces video smoothness, but then 72Hz on a 60Hz display is not smooth either (and few Pokemon Mini games are 'smooth' to begin with...). More importantly, enabling this option eliminates screen tearing.

**Handy**

This Atari Lynx emulator core has seen several big improvements.

Fix frame pacing Before, this core had entirely broken frame pacing. The core reported a fixed refresh rate of 75Hz to the frontend, but the Lynx (and the internal emulation code) has a variable refresh rate of 0-75Hz; games can render at any rate they please. In retro_run(), the Lynx is always emulated until the next 'end of frame' event occurs - if a game renders at e.g. 25 fps, this means retro_run() will actually correspond to (1/25) seconds worth of Lynx runtime instead of the expected (1/75) seconds. In this case, the game is emulated too quickly - but it appears to run at the correct speed in the frontend because the core uploads an 'oversized' audio buffer (1/25 seconds worth of samples). RetroArch syncs on audio in such a way that when too many samples are received, the frontend runs in 'slow motion' - so the 'too fast emulation' + 'too many audio samples' effectively cancel out. But the results are awful. This is a significant violation of the libretro API, and it destroys the frontend's ability to properly synchronise audio and video, and to pace the frames correctly.

We now modified the run loop such that a fixed number of CPU cycles are emulated on each call of retro_run(), corresponding to the actual frontend output video refresh rate (which can be set via a new Video Refresh Rate core option). Thus the Lynx is always emulated at the correct speed, audio is always uploaded in batches of the correct size, and generated video frames are captured and output when available (and when the frontend can accept them).

The default Video Refresh Rate has been set to 60Hz, which provides smooth results for most games (and also eliminates screen tearing on 60Hz displays, which was an issue when the core only reported a 75Hz refresh rate). If a game has a higher frame rate than this (rare, but e.g. the intro and menus of California Games run at the full 75 fps), then 'excess' frames will be dropped. Users with 75Hz+ VRR displays can set higher refresh rates to improve video smoothness in these cases.

Improve save state efficiency Before, the retro_serialize() function determines the save state size by allocating a temporary ~310kb buffer, writing an actual save state into it, then fetching the resultant buffer occupancy. This is terribly inefficient - and retro_serialize() is called 3 times every time a state is saved or loaded...

We modified the serialisation memory stream code to allow a 'virtual' save state to be made - no buffer is required, and no data are copied. This means retro_serialize() can now fetch the save state size with no memory allocations and no wasted effort.

Add optional LCD ghosting filter

We added a new LCD Ghosting Filter core option which can be used to apply an LCD ghosting effect by blending multiple successive frames. The number of blended frames can be set from 2-4; using more frames improves the quality of the effect at the expense of increased performance requirements.

LCD ghosting is particularly beneficial for the Lynx because many games run at very low frame rates, and some blurring helps to smooth out the frequently 'jerky' screen updates.
RetroArch Updates

See the Changelog below for a detailed breakdown of all the changes that have happened.

One of the biggest changes for Steam users by far is the new Steam Discord Rich Presence support. NOTE: You will need to use the desktop client in order for this to work. It won't work with the webbrowser client.

**Changelog**

__1.10.3__

    ANDROID: Decouple Play Core dependency to bring app into compliance for F-Droid
    AI/SERVICE: Disable AI Service setting by default
    BLUETOOTH/LAKKA: bluetoothctl: add / modify pairing steps
    CHEEVOS: Disallow manual frame delay setting in Hardcore Mode
    DATABASE: Serial scanning for Wii now includes WBFS
    INPUT/MAPPING: Fix offset + crash when clearing input port binds
    INPUT/MAPPING: Fix saving of 'Analog to Digital Type' when configuration overrides are used
    LOCALIZATION: Add Valencian language option
    LOCALIZATION: Updates
    MENU/SETTINGS: Move 'Show Menu Bar' under 'Windowed Mode' settings
    MENU/SETTINGS: Add sublabels for 'Subsystems' and 'Input Deadzone/Sensitivity'
    MENU/SETTINGS: Move 'On-Screen Notifications' to top
    MENU/XMB: Unified the shadow alpha value to a slightly darker one for better readability
    MENU/XMB: Corrected the option label and sublabel for actual behavior
    MIYOO: Enable ALSA audio driver and default to it
    PSP: Take out extra languages/localization, adds about 4/5MB to the binary, and RAM is limited on PSP (32MB and 64MB RAM models)
    STATIC PLATFORMS: Populate all history list metadata when launching content from playlists
    STEAM: Introduce Steam Rich Presence
    VIDEO: Fast-Forward Frameskip improvement
    VIDEO/THREADED: Stability fixes
    WINDOWS/WINRAW: Fix multiple light guns
    WIIU: Fix USB get_device_name(), don't truncate to three chars 