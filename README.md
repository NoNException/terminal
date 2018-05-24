Terminal
========

This script (`terminal.py`) allows you to open a new terminal window and execute
some commands on Windows, Cygwin, Ubuntu and OS X. And prompts you "press any key to continue ..." before exit.

Programming in desktop text editors (atom, gvim, sublime and gedit) always requires executing your code in a new interactive shell window. But a lot of editors is lack of such feature, the only thing they can do is executing shell commands in their bottom panel, or in a silent background job.

Opening a new terminal window to execute commands in different operating systems is a tricky thing: arguments must be carefully escaped and passed in the correct way, intermediate script (shell script, AppleScript or batch script) must be carefully generated and passed through pipe, and different terminal in all systems must be invoked in different methods.

Therefor, `terminal.py` is created to get these dirty stuff down, in a single script file and provide a unique interface for all operating systems. 

Calling it in your favorite editor to open a new window and execute your programs just like running a command line application in visual studio.

Features
========

- **Windows**:
	- Open a new `cmd` window to execute Windows commands.
	- Open a new `cygwin` bash/mintty window to execute Cygwin commands.
	- Run `cygwin` commands directly in the current Windows shell (without open a new window).
	- Open a new `WSL` (Windows Subsystem for Linux) bash window to execute linux commands.
	- Run `WSL` bash commands directly in the current Windows shell (without open a new window).
- **Cygwin**:
	- Open a new cygwin `bash` window to execute cygwin commands.
	- Open a new cygwin `mintty` window to execute cygwin commands.
	- Open a new `cmd` window to execute Windows commands.
- **Linux / Ubuntu**:
	- Open a new `xterm` window to execute commands on Linux Desktop.
	- Open a new `gnome-terminal` window to execute commands on Linux Desktop.
- **Mac OS X**:
	- Open a new `Terminal` window to execute commands in Mac OS X
	- Open a new `iTerm2` window to execute commands in Mac OS X
	- Open a new `xterm` window to execute commands in Mac os x (require xquartz)
- **Misc**:
	- After commands finished, prompts user to **press any key to quit** (optional).
	- Specify initial working directory (optional).
	- Read commands from both arguments or stdin.
	- Run some other commands before quit (after waiting user pressing key).
	- Set terminal profile (only enabled in Terminal/iTerm/gnome-terminal).
	- Set the title of the terminal window (not available in some terminal).

Manual
======

```text
$ python terminal.py
Usage: terminal.py [options] command [args ...]

Execute program in a new terminal window

Options:
  --version             show program's version number and exit
  -h, --help            show this help message and exit
  -t TITLE, --title=TITLE
                        title of new window
  -m TERMINAL, --terminal=TERMINAL
                        available terminals: terminal (default), iterm
  -p PROFILE, --profile=PROFILE
                        terminal profile
  -d CWD, --cwd=CWD     working directory
  -w, --wait            wait before exit
  -o POST, --post=POST  post action
  -s, --stdin           read commands from stdin 
```

Windows 
-------

Open a new cmd window to execute command:

	python terminal.py d:\hello.exe

Open a new cmd window to execute command and pause after finish:

	python terminal.py --wait d:\hello.exe

Open a new cmd window and set title:
    
	python terminal.py --wait -t mytitle d:\hello.exe 

Open a new cmd window to execute command in a given working directory:

	python terminal.py --wait -d d:\ dir
	
Open a new cmd window and execute commands which is passed from stdin:

    python terminal.py --wait --stdin 
	dir c:\
	echo Hello from a new cmd window !!
	^Z

Linux (ubuntu)
--------------

Open a new window (xterm by default) to execute command:

	python terminal.py --wait ls -la
	
Open a new gnome-terminal to execute command:

	python terminal.py -m gnome-terminal --wait ls -la
	
Open gnome-terminal in given profile (create a new profile in gnome-terminal's settings):

	python terminal.py -m gnome-terminal -p myprofile --wait ls -la
	
Open a new window to execute command in a given working directory:

	python terminal.py --wait -d /tmp ls -la
	
Open a new gnome-terminal and execute commands which is passed from stdin:

	python terminal.py --wait -m gnome-terminal --stdin
	ls -la
	echo "Hello from a new gnome-terminal"
	^D

Mac OS X
--------

Open a new Terminal window to execute command:

	python terminal.py --wait ls -la
	
Open Terminal in given profile (create a new profile in Terminal's preferences):

	python terminal.py --wait -p DevelopProfile ls -la
	
Open a new window to execute command in a given working directory:

	python terminal.py --wait -d /tmp ls -la
	
Open Terminal and execute commands which is passed from stdin:

	python terminal.py --wait --stdin
	ls -la
	echo "Hello from a new Terminal window"
	^D

Open iTerm and execute command:

	python terminal.py --wait -m iterm ls -la
	
Open Terminal window in a given profile and activate MacVim after exit:

	python terminal.py --wait -o "open /Applications/MacVim.app" -p myprofile ls -la
	
This is very useful when you are executing terminal.py inside MacVim, because after 
terminal window closed OS X will not bring MacVim to the front. And you need a new 
terminal profile because you can enable "Close window when shell exists" in myprofile 
to avoid closing window manually after exists.

You can use Terminal or iTerm2 in Mac OS X as you like.
	
Run Cygwin commands from Win32
------------------------------

Open cygwin bash window in win32:

	python terminal.py --wait -c c:\cygwin -m bash ls -la
	
Open cygwin mintty window in win32:

	python terminal.py --wait -c c:\cygwin -m mintty ls -la

Run cygwin commands in the same terminal without creating a new window by using `cygwinx` option:

	python terminal.py -c c:\cygwin -m cygwinx ls -la
	
Open cygwin mintty window in win32 from given working directory:

	python terminal.py --wait -c c:\cygwin -m mintty -d d:\ ls -la
	
Inside Cygwin
-------------

Open cmd window to run win32 command from cygwin:

	python terminal.py --wait -m cmd dir
	
Open mintty window to run cygwin shell command from cygwin:

	python terminal.py --wait -m mintty ls -la
	
Open bash window to run cygwin shell command from cygwin:

	python terminal.py --wait -m bash ls -la
	

Run WSL Linux commands on Windows
---------------------------------

Open a new bash window to run linux commands:

	python terminal.py --wait -m wsl ls -la

Run linux commands in the current windows shell window:

	python terminal.py -m wslx ls -la

Run debian and ubuntu1804 via wsl:

    python terminal.py -m wslx -p debian ls -la
    python terminal.py -m wslx -p ubuntu1804 ls -la


Credit
======

......
