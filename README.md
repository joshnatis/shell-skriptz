# shell-skriptz
## What is a shell script?
> "The real power of the computer is its ability to do the work for you. To get it to do that, we use the power of the shell to automate things. We write shell scripts." - [random site](http://linuxcommand.org/lc3_writing_shell_scripts.php)

## Setting up
As these are shell scripts, they're meant to be run in the shell (specifically a Unix shell). I'm using Bash on a Mac, so a few things may work differently for you (I'll remark on those differences if I can catch them). I don't think I have any 'bashims" in my scripts (i.e. features not defined by POSIX, which are specific to the Bash shell), so at least that shouldn't be an issue. 

To start, I suggest creating a directory titled *.scripts* in your home folder (~ on Mac), noteably including the '.' prefix so to not visually clutter up your working space (I've learned from my mistakes). This is where you'll be keeping all of the shell scripts you write/save. 

Next, you'll need to add this directory to your PATH. Essentially this gives you the ability to refer to any files within the directory simply by their name, even when you're working in a different directory (e.g. writing *example* vs something like **~/.scripts/** *example*). To do this, edit your **.bash_profile** or **.profile**, which are located in your home directory, and insert this line:   `export PATH=~/.scripts`. *Note: If you already have something similar, you can simply add* `:~/.scripts` *at the end of the line.*

The last step (once you have the scripts in your directory, of course), is to execute the command `chmod +x *example`for each file, thus making them executable. And that should be it!

## Documentation

### hmm
<pre> hmm </pre>
* This one simply clears the screen and then calls `ls` -- it's essentially a fidgeting command that I can call while I'm thinking about what to do next (hence the name). `hmm` is also shorter to write than `clear`, which saves me a few milliseconds :P. (*Note: ^L, aka CTRL L, clears the terminal screen as well, and can be used as an alternative to* `clear`)

### newcpp / newjava
<pre>newcpp hello
newcpp hello.cpp
newjava hello
newjava hello.java</pre>
  
* These scripts help bypass boilerplate code that wastes time and accelarates your impending carpal tunnel. Invoking the command opens your default editor/IDE with a new *.cpp/.java* file, already named and containing a few lines of code. The script checks whether you've included the extension for the file in your argument, so there's no need to write anything besides your desired file name. 
* (*Compatability note: these scripts use the* `open` *command, which is unique to MacOS -- it just uses the default program to open a file based on its extension. The Linux alternative to `open` is `xdg-open`. For other Unix systems, changing `open` to your desired text editor, e.g. `nano`, should do the trick.*). 

### run
<pre>run hello.cpp</pre>
* *(requires: [gcc/g++](https://gcc.gnu.org/))*


* Short and sweet -- this script compiles a *.cpp* file with `g++` (creating *a.out*) and runs the resulting out file.

### mp3
<pre>mp3 https://www.youtube.com/watch?v=dQw4w9WgXcQ</pre>
* *(requires: [youtube-dl](https://github.com/ytdl-org/youtube-dl))*

* I cannot recommend `youtube-dl` enough, both as an alternative to suspicious YouTube2MP3 websites, and to streaming services such as Spotify. Calling `mp3 <url>` downloads the requested file to your current directory. If you're using iTunes or a similar music player, you have to first open the file in the player manually in order for it to show up in your music library. For me, this process often looks like this: 
 1. Call `mp3 <url>` in my home directory (for as many songs as necessary)
 2. `open *.mp3` (at this point the songs will successfully be in iTunes)
 3. `mv *.mp3 ~/Downloads`(or to wherever you store your music files)
 4. Next time you play a song you moved, iTunes may or may not give you an error message claiming it cannot find the file (since you moved it to a new directory). Simply follow the prompts it gives you, locate the erroneous file in Finder, and the rest will be found automatically. This is, of course, a horrible solution, but the important thing is that you have the file readily accessible on your computer.
 5. Optionally, you can add points 2. and 3. to the script, but I prefer not to have iTunes open every time I download a file.
 
 *Suggestion: If you only need a snippit of some audio, rather than the entire file, download [Audio Hijack](https://rogueamoeba.com/audiohijack/), a great program with an indefinite free trial that allows you to record the audio directly from your computer.*
 
 *Suggestion #2: Play your music in style with my command-line music player, [teapot](https://github.com/joshnatis/teapot) :P*
 
 ### mp3crop
 <pre>mp3crop 1:00 2:08 https://youtu.be/DljBMflGdek</pre>

* *(requires: [youtube-dl](https://github.com/ytdl-org/youtube-dl))*

* This one is just like `mp3`, but with the added functionality of cropping a desired section of a YouTube video. The script would probably be better if it could be integrated into `mp3` and called like this: `mp3 --crop start-time end-time <url>`, if I have enough time and competency I'll implement that (or you can help me!).

### record
<pre>record                     #yields OUT.mp4
record --mov               #yields OUT.mov
record name                #yields name.mp4 
record --mov name          #yields name.mov (order doesn't matter)
</pre>
* *(requires: [ffmpeg](https://github.com/FFmpeg/FFmpeg))*

* Another indispensible tool in anyone's toolkit -- `ffmpeg`. If you've ever tried to record your screen on MacOS, then you've probably experieced the perils of QuickTime Player and *.mov*. Though I appreciate Apple providing a native screenrecorder, QuickTime is bulky, only works with files in *.mov* format (which happen to be huge and don't work well with YouTube), and is relatively featureless. Also, c'mon, having that QuickTime icon in your Dock while recording makes you look like an amateur! Lol. 

* With `record`, you can call the command whenever you're ready to start, and enter *q* or *^C* to finish recording. The resulting file will be titled *OUT.mp4*, or something similar if you provided some arguments. If you've accidentally messed up the video format, you can convert from *.mov* to *.mp4* (or vice versa) when finished by invoking this command: `ffmpeg -i input.mov output.mp4`.
* (*Compatability note: the arguments within this script strongly depend on your OS and even your specific setup -- make sure to visit [this](https://trac.ffmpeg.org/wiki/Capture/Desktop) site for info on how to properly configure for your system.*)

### concatv
<pre>concatv                                   #concatenates all .mp4 files in directory
concatv vid1.mp4 vid2.mp4 vid3.mp4        #concatenates .mp4 files listed as arguments
</pre>
* *(requires: [ffmpeg](https://github.com/FFmpeg/FFmpeg))*

* If you ever have multiple video files which you'd like to stitch together into one video, this script is the one to use. Invoking it will result in a file called *final.mp4*. Be ware that the order in which you list your arguments matters (they will be concatenated in that order). *Note: only meant to work for .mp4 files, but can very easily be changed to support any filetype supported by `ffmpeg`. Note 2: Apparently the video files are required to be in the same aspect ratio and size in order for this to work. In order to not run into issues with this, just record your full screen or assure that the videos are the same size. Hopefully I can find a fix for this.* 

### delayaudiov
<pre>delayaudiov     #Asks for input video, seconds to delay by, and output file</pre>
* *(requires: [ffmpeg](https://github.com/FFmpeg/FFmpeg))*

* If your audio and video are somehow out of sync (which has been happening to me a lot recently), you can try to remedy that with this script. If you don't know exactly how far the video lags behind the audio, you can keep delaying the audio by 1 second at a time until you're satisfied.

### changevolumev
<pre> changevolumev     #Asks for input video, decibels to change audio by (+/-), and output file</pre>
* *(requires: [ffmpeg](https://github.com/FFmpeg/FFmpeg))*

* If your audio is either too quiet or too loud, you can adjust that with this script. Again, if you're unsure of exactly how much to raise/decrease the volume by, incrementally call this script with small changes until satisfied.

### wiki
<pre> wiki     #Presents you with 10 random wikipedia articles to choose from</pre>
* *(requires: [Python](https://www.python.org/))*

* This script is actually written in Python, but since you can also do `chmod +x` on Python scripts (and even drop the .py), I figured it was still relavant to include here. To use, simple call `wiki` and then enter the index of the article you want to read (or -1 for 10 new articles) -- it'll be opened in your default web browser. The articles are fetched from [this Wikipedia API](https://en.wikipedia.org/w/api.php?action=query&list=random&rnnamespace=0&rnlimit=10&format=json).
* (*Compatability note: this script uses the `open` command to open the article in your default browser. If you're not on MacOS you can change that to `xdg-open` or to the name of your desired browser*)

### intro
<pre>intro     #Does colorful stuffs</pre>
* *(requires: [cowsay](https://en.wikipedia.org/wiki/Cowsay) and [lolcat](https://github.com/busyloop/lolcat))*

* This one's just for fun; it prints out some colorful things as well as a random ASCII art character using `cowsay`.
