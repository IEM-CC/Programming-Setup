# Programming-Setup
## Setup for C++

### Installation
- Install [MinGW Compiler](https://osdn.net/projects/mingw/releases/)
- Install [Sublime Text](https://www.sublimetext.com/)
### Setup PATH 
- Setup environment variables for mingw
  - Go to your MinGW installation folder. For me it was something like this: 
    ```
    C:\MinGW\bin
    ```
  - Go to `Edit the system environment variables`
  - Add to new path, address of your MinGW folder
- Setup environment variables for Sublime Text
  - Go to your Sublime Text installation folder. For me it was something like this: 
    ```
    C:\Program Files\Sublime Text 3
    ```
  - Go to `Edit the system environment variables`
  - Add to new path, address of your Sublime Text folder
### Configure Sublime Text
- Open Sublime Text
- Press `Ctrl+Shift+P` to open Command Palette
- Search for `Install Package Control` and press `Enter`
- Again open Command Palette and search for `Terminus` and install it
- Similarly install `SublimeAStyleFormatter` and `AvancedNewFile`.
- **Configure `SublimeAStyleFormatter`**
  - Go to `Preferences -> Package Settings -> SublimeAStyleFormatter -> Settings-Default`
  - Change to `"autoformat_on_save": true`
- **Make Interactive Build System for C++**
  - Go to `Tools->Build System -> New Build System`
  - Paste this code and save
    ```
    {	
          "target":"terminus_exec",
          "cancel":"terminus_cancel_build",
          "focus":true,
          "shell_cmd": "g++ \"${file}\" -o \"${file_path}/${file_base_name}\"",
          "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
          "working_dir": "${file_path}",
          "selector": "source.c++",

          "variants":
          [
            {
              "name": "Run",
              "shell_cmd": "g++ \"${file}\" -o \"${file_path}/${file_base_name}\" && \"${file_path}/${file_base_name}\""
            }
          ]
       }
      ```
     - Save it with extension `.sublime-build`. You can use `C++ Terminus.sublime-build`.
  - **Set keyboard shortcuts**
    - Go to `Preferences -> Keybindings`
    - In `Default(Windows).sublime-keymap- User` file paste this code
      ```
       [

          // Togle Terminus panel (at the bottom of the screen) Open/Closed when Alt+' is pressed
          {
            // The key press to look out for
            "keys": ["alt+`"],

            // Toggle the panel
            "command": "toggle_terminus_panel"
          },

          {
            "keys": ["alt+c"],
            "command": "terminus_open",
            "args" : {
                  "cmd": "cmd.exe",
                    "cwd": "${file_path:${folder}}",
                    "title": "Command Prompt",
                    "panel_name": "Terminus"
                }
          },
          {
            "keys": ["alt+b"],
            "command": "terminus_open",
                 "args" : {
                  "cmd": ["C:\\Program Files\\Git\\bin\\bash.exe", "-i", "-l"],
                    "cwd": "${file_path:${folder}}",
                    "title": "Git Bash",
                    "panel_name": "Terminus"
                 }
          },

          {
              "keys": ["alt+shift+n"],
              "command": "set_layout",
              "args":
                {	
                  "cells":[
                        [ 0, 0, 1, 2 ],
                        [ 1, 0, 2, 1 ],
                        [ 1, 1, 2, 2 ]
                    ],
                    "cols": [ 0.0, 0.7578125, 1.0 ],
                    "rows": [ 0.0, 0.5, 1.0],

                }
          },
        ]
     ```
