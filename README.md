# OS

## Arch

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
