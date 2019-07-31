# skriptz
## What is a shell script?
> "The real power of the computer is its ability to do the work for you. To get it to do that, we use the power of the shell to automate things. We write shell scripts." - [random site](http://linuxcommand.org/lc3_writing_shell_scripts.php)

## Setting up
As these are shell scripts, they're meant to be run in the shell (specifically a Unix shell). I'm using Bash on a Mac, so a few things may work differently for you (I'll remark on those differences if I can catch them). I don't think I have any 'bashims" in my scripts (i.e. features not defined by POSIX, which are specific to the Bash shell), so at least that shouldn't be an issue. 

To start, I suggest creating a directory titled *.scripts* in your home folder (~ on Mac), noteably including the '.' prefix so to not visually clutter up your working space (I've learned from my mistakes). This is where you'll be keeping all of the shell scripts you write/save. 

Next, you'll need to add this directory to your PATH. Essentially this gives you the ability to refer to any files within the directory simply by their name, even when you're working in a different directory (i.e writing *example* vs something like **~/.scripts/** *example*). To do this, edit your **.bash_profile** or **.profile**, which are located in your home directory, and insert this line:   **export PATH=~/.scripts**. *Note: If you already have something similar, you can simply add* **:~/.scripts** *at the end of the line.*

The last step (once you have the scripts in your directory, of course), is to execute the command **chmod +x *example*** for each file, thus making them executable. And that should be it!

## Documentation

### hmm
* *(accepts: no arguments)*

* This one simply clears the screen and then calls **ls** -- it's essentially a fidgeting command that I can call while I'm thinking about what to do next (hence the name). **hmm** is also shorter to write than **clear**, which saves me a few milliseconds :P. (*Note: ^L, aka CTRL L, clears the terminal screen as well, and can be used as an alternative to* **clear**)

### newcpp / newjava
* *(accepts: name of file, optionally with extension)*
  * *i.e* **newcpp** *helloworld*, **newcpp** *helloworld.cpp*, **newjava** *eww.java*, *etc.*
  
* These scripts help bypass boilerplate code that wastes time and accelarates your impending carpal tunnel. Invoking the command opens your default program to open *.cpp/.java* files with a new file, already named and containing a few lines of code. The script checks whether you've included the extension for the file in your argument, so there's no need to write anything besides your desired file name. 
* (*Compatability note: these scripts use the* **open** *command, which is unique to MacOS (as far as I know) -- it just uses the default program to open a file based on its extension. For other Unix systems, changing* **open** *to your desired text editor, i.e* **nano**, *should do the trick*).

### run
* *(accepts: name of .cpp source code file, including extension)*
  * *i.e* **run** *hello.cpp*
* *(requires: [gcc/g++](https://gcc.gnu.org/))*


* Short and sweet -- this script compiles a *.cpp* file with **g++** (creating *a.out*) and runs the resulting object file.

### mp3
* *(accepts: YouTube url)*
* *(requires: [youtube-dl](https://github.com/ytdl-org/youtube-dl))*

* I cannot recommend **youtube-dl** enough, both as an alternative to suspicious YouTube2MP3 websites, and to streaming services such as Spotify. Calling **mp3** *\<url>* downloads the requested file to your current directory. If you're using iTunes or a similar music player, you have to first open the file in the player manually in order for it to show up in your music library. For me, this process often looks like this: 
 1. Call **mp3** *\<url>* in my home directory (for as many songs as necessary)
 2. **open \*.mp3** (at this point the songs will successfully be in iTunes)
 3. **mv \*.mp3 Downloads** (or to wherever you store your music files)
 4. Next time you play a song you moved, iTunes may or may not give you an error message claiming it cannot find the file (since you moved it to a new directory). Simply follow the prompts it gives you, locate the erroneous file in Finder, and the rest will be found automatically. This is, of course, a horrible solution, but the important thing is that you have the file readily accessible on your computer.
 5. Optionally, you can add points 2. and 3. to the script, but I prefer not to have iTunes open every time I download a file.
 
 *Suggestion: If you only need a snippit of some audio, rather than the entire file, download [Audio Hijack](https://rogueamoeba.com/audiohijack/), a great program with an indefinite free trial that allows you to record the audio directly from your computer.*

### record
* *(accepts: optional parameter of any word/digit of your choosing)*
* *(requires: [ffmpeg](https://github.com/FFmpeg/FFmpeg))*

* Another indispensible tool in anyone's toolkit -- **ffmpeg**. If you've ever tried to record your screen on MacOS, then you've probably experieced the perils of QuickTime Player and *.mov*. Though I appreciate Apple providing a native screenrecorder, QuickTime is bulky, only works with files in *.mov* format (which happen to be huge and don't work well with YouTube), and is relatively featureless. Also, c'mon, having that QuickTime icon in your Dock while recording makes you look like an amateur! Lol. 

* With **record**, you can call the command whenever you're ready to start, and enter *q* or *^C* to finish recording. The resulting file will be titled *out.mov*, or if you provided an argument, *out\<argument>.mov*. You can also record in *.mp4* or in some other formats, but when I tried *.mp4* my audio was constantly cutting out. In order to convert from *.mov* to *.mp4* when finished, invoke this command: **ffmpeg -i** example.mov example.mp4.
* (*Compatability note: the arguments within this script strongly depend on your OS and even your specific setup -- make sure to visit [this](https://trac.ffmpeg.org/wiki/Capture/Desktop) site for info on how to probably configure for your system.*)
