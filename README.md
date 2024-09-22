# OS

## Arch 
![Shell Script](https://img.shields.io/badge/shell_script-%23121011.svg?style=for-the-badge&logo=gnu-bash&logoColor=white)

### screen recording
install recordmydesktop using
```bash
sudo pacman -S recordmydesktop
# and to record screen start the program with

recordmydesktop

# this will record screen in .ogv format.
# it can be converted to any other format using ffmpeg
# the output will probably be called out.ogv,and
# output (here - recording.mp4) video can be any name
ffmpeg -i out.ogv recording.mp4

```

### Programming

<em> Stay on VS Code</em>

The Aur version of VS-Code, can be cloned or 

```shell
$ yay -S visual-studio-code-bin
```
#### Python

Installing extensions for python is enough without further hussle

#### C / C++

Check if gcc, g++, and gdb are installed.

```shell
# check versions

$ gcc -v
$ g++ -v
$ gdb -v
```
gdb won't probably be installed, so install it with

```shell
# dont know if gdb-common is needed. try without it next time
$ sudo pacman -S gdb gdb-common
```
and then in VS-Code install the extension for C/C++ and done! well, not quite.<br>
Some libraries that are in code may be compiled because they are included (imported) but linker just doesn't know they are required. hence, we must tell linker to link them. and we do this by adding `"-lm"` to `"Args":[] ` in task.json like the following.
```json 
		
"args": [
	"-fdiagnostics-color=always",
	"-fopenmp",
	"-g",
	"${file}",
	"-o",
	"${fileDirname}/${fileBasenameNoExtension}","-lm"
            ],
```

to tasks.json file

and not to forget, since most of the time there will be multiple files to compile in a project. make sure to tell gcc to compile all of them. this can be done by replacing the `"${file}` tag with  `"${fileDirname}/*.c"` tag. and in the end, tasks.json file should look like the following.
```json
{
	"tasks": [
		{
		    "type": "cppbuild",
		    "label": "C/C++: gcc build active file",
		    "command": "/usr/bin/gcc",
		    "args": [
			"-fdiagnostics-color=always",
			"-g",
			"${fileDirname}/*.c",
			"-o",
			"${fileDirname}/${fileBasenameNoExtension}","-lm"
		    ],
		    "options": {
			"cwd": "${fileDirname}"
		    },
		    "problemMatcher": [
			"$gcc"
		    ],
		    "group": {
			"kind": "build",
			"isDefault": true
		    },
		    "detail": "Task generated by Debugger."
		}
	],
	"version": "2.0.0"
}
```
# Valgrind

The Valgrind tool suite provides a number of debugging and profiling tools that help you make your programs faster and more correct. The most popular of these tools is called Memcheck. 
It can detect many memory-related errors that are common in C and C++ programs and that can lead to crashes and unpredictable behaviour. [source](https://valgrind.org/docs/manual/quick-start.html)

Valgrind can be installed from arch official repos and to use valgrind
we use the valgrind command like the following

```shell
# Assuming the executable is called program and we are in the directory
valgrind --leak-check=yes ./program

# For lists of detected and suppressed errors, rerun with: -s as follows
valgrind -s --leak-check=yes ./program
```


# Bios

you may forget bios password. if this happens, refer to [this](https://bios-pw.org/) page to get password. it helped me reset mine.
