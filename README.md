# FFmpeg_Composer
GUI interactive command-line composition and execution for the stock FFmpeg tool.

To outline what I want for version 1.x of this application:

  - A GUI that compiles and works on all significant operating systems (Win10, Linux, MacOS, Android, FreeBSD -!-) 
    
    - An interactive command string with drop-down lists for setting/replacing indivdual options.
    
    - Ability to save and load/recall command compositions made.
    
    - A preview option, utilizing ffplay to test as much as possible
    
    - Support for concatination lists (not streaming, just individual files and concatinated pseudo files)
    
    - Support for up to three inputs, but not with the same content type. i.e. just one of: video, audio, or subtitles.
    
    - Quick composition of simple, but verbose operations, like bit-stream filters and cuts (include option for cuts of raw copy or decode to uncompressed audio*)
    
    - A simple similar menu/drop-down button bar just above the command string for adding components to the command string, like: "+&nbsp;codec", "+ codec op", "+ file", "+ filter", "+ codec", "+codec op", "+ bitstr filter"
    
    - Support for -complex_filter, since anything complicated enough to need the use of this composer would benefit greately from this interactive and testable filter programming. **
    
    - A button/menu-item for examining the input and displaying the 'ffprobe' output for reference only (no parsing)
    
    - The default of "-v error", through menu/options may be instead "-v verobse".
    
    - Also through menu/options pre-configured command strings can be loaded or loaded as default.
    
    - Support for command string will be divided into three segments: One - Input files (including the -map option); Two - all filter, encoding, and muxing options; and Three - the output file.  Only the second segment will be save-able/restore-able.  The sections one and three will have to be reconfigured and typed every time FFmpeg_Composer is run.  This is a safety feature to ensure that a person individually observes the setting of every input/output file to avoid mischosen/mispelled/missing input files and accidental overwrites of outputfiles.
    
    - Default is to overwrite output file with "-y" option, to prevent requiring a prompt-relay feature and unnecesary delays.  Other default global options may be set in configuration, ffmpeg, ffprobe, and ffplay each having their own line of defaults.
    
    - To improve out-of-the-box functionality, default is to call a local, statically compiled copy of ffmpeg, but if missing just call "ffmpeg" in order to use the system path.
    
    - Also include with distribution some kind of shell/OS/library/executable if needed in order to facilitate the execution of the command string and reception of the corrisponding output.  Prefer an all Ada choice, or direct library loading and executing of ffmpeg/ffprobe/ffplay if at all possible.
    
Notes:

  * libopus and other very short segment formats might split nicely, but several very common codecs do not, and this means that when re-assembling cuts together the audio can fall out of sync with the video.  Even if the timing labels cause the player/encoder to fix
this, it can and has caused trouble with precision edits, so it becomes necessary to use some uncompressed stream, like PCM 16/24bit signed, that can split exactly in time with the video and produce perfect sync when re-encoding/concatinating.  Unfortunately, it is possible that a noticable amount of sound degredation will occur, even with the best settings.

  ** Support for complex_filters will not be generally source-importable, but will have defined limitations and automatic in-out labels to ensure the streams all come in and go out equally -- With the exception that there should be an irreversable option to make the complex_filter block of text manually customizable. Upon loading such saved/imported strings, the inconsistency should be detected and automatically be displayed in manual-edit mode.  If automatic labeling format is manually restored, it can only be detected upon re-loading the command string.
