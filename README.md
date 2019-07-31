# skriptz
## What is a shell script?
> "The real power of the computer is its ability to do the work for you. To get it to do that, we use the power of the shell to automate things. We write shell scripts." - [random site](http://linuxcommand.org/lc3_writing_shell_scripts.php)

## Setting up
As these are shell scripts, they're meant to be run in the shell (specifically a Unix shell). I'm using Bash on a Mac, so a few things may work differently for you (I'll remark on those differences if I can catch them). I don't think I have any 'bashims" in my scripts (i.e. features not defined by POSIX, which are specific to the Bash shell), so at least that shouldn't be an issue. 

To start, I suggest creating a directory titled ".scripts" in your home folder (~ on Mac), noteably including the '.' prefix so to not clutter up your working space (I've learned from my mistakes). This is where you'll be keeping all of the shell scripts you write/save. 

Next, you'll need to add this directory to your PATH. Essentially this gives you the ability to refer to any files within the directory simply by their name, even when you're working in a different directory (i.e writing *example* vs something like **~/.scripts/** *example*). To do this, edit your **.bash_profile** or **.profile**, which are located in your home directory, and insert this line:   **export PATH=~/.scripts**. *Note: If you already have something similar, you can simply add* **:~/.scripts** *at the end of the line.*

The last step (once you have the scripts in your directory, of course), is to execute the command **chmod +x *example*** for each file, thus making them executable. And that should be it!

## Documentation

### hmm
* *(accepts no arguments)*

* This one simply clears the screen and then calls **ls** -- it's essentially a fidgeting command that I can call while I'm thinking about what to do next (hence the name). **hmm** is also shorter to write than **clear**, which saves me a few milliseconds :P. (*Note: ^L, aka CTRL L, clears the terminal screen as well, and can be used as an alternative to* **clear**)

### newcpp / newjava
* *(accepts name of file, optionally with extension)*
  * *i.e* **newcpp** *helloworld*, **newcpp** *helloworld.cpp*, **newjava** *eww.java*, *etc.*
  
* These scripts help bypass boilerplate code that wastes time and accelarates your impending carpal tunnel. Invoking the command opens your default program to open *.cpp/.java* files with a new file, already named and containing a few lines of code. The script checks whether you've included the extension for the file in your argument, so there's no need to write anything besides your desired file name. (*Compatability note: these scripts use the* **open** *command, which is unique to MacOS (as far as I know) -- it just uses the default program to open a file based on its extension. For other Unix systems, changing* **open** *to your desired text editor, i.e* **nano**, *should do the trick*).
