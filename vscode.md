
# vscode

When you type a "tab" in the vscode editor, vscode in its default configuration converts the tab to 4 spaces!? Alas.

This causes problems for folks who are trying to use/create/modify Makefiles, which require tabs to be tabs, not spaces!

## Solution

* Q: Why should a text editor change the character that you type as it's default behavior?
  * Answer: There is no good reason. That's a rhetorical question. It's discussed in the documentation...
  * [vscode basics: indentation](https://code.visualstudio.com/docs/editor/codebasics#_indentation) -- visualstudio.com
* The solution: change the settings to modify the default behavior.
  * To change vscode settings...
* Windows/Linux
  * File > Preferences > Settings
  * Search for "indent"
  * When you find "Editor: Auto Indent:", change "full" to "none" in dropdown menu
    * GUI says "also modified elsewhere"
    * Scroll down and change another one...
  * When you find: "Editor: Detect Indentation", uncheck this box too
    * Controls whether Editor Tab size and Editor: Insert Spaces will be automatically...
* Mac
    * Code > Preferences > Settings
    * Search for editor.insertSpaces -- uncheck the box
    * GUI says "Also modified elsewhere"
      * Click on the "Editor: Detect Indentation" link and then...
      * Unselect the checkbox for "Controls whether Editor:Tab Size and Editor: Insert Spaces" will be automatically...
    * Change "true" to "false" in this line:  "editor.insertSpaces": true,

# settings.json

Configuration changes are stored in a JSON file called "settings.json"

It's probably not a good idea to change this file directly, but here's how it works...

* settings.json
  * [user and workspace settings](https://code.visualstudio.com/docs/getstarted/settings) -- visualstudio.com
  * Windows/Linux: File > Preferences > Settings
  * Mac: Code > Preferences > Settings
  * [settings.json](https://code.visualstudio.com/docs/getstarted/settings#_settingsjson) -- visualstudio.com
    * You can review and edit this file directly by opening it in the editor with the Preferences: Open Settings (JSON) command. 
    * Q: What is the "Preferences: Open Settings (JSON)" command?  A: I don't know
  * You need to click on the little icon on the upper right -- a page with a loopy arrow
    * This toggles between the GUI and direct editing of the JSON file
    * It also gives the pathname to the settings.json file
* settings.json
  * It's possible to change settings.json directly, but not recommended
  * When you change default configuration, settings.json records the changes
  * In my case, it changed from an empty file to the following...
  ``` 
  {
    "editor.autoIndent": "none",
    "editor.detectIndentation": false,
  }
  ``` 
* Where is "settings.json"?
  * Windows: this file is located in: C: > Users > p.bogden > AppData > Roaming > Code > User > settings.json
    * I inferred this from the GUI (seems that the > is supposed to be a substitute for \ and /)
  * Mac: this file is: ~/Library/Application Support/Code/User/settings.json

## vscode terminal can't find my python?

* My problem (on the mac): vscode's integrated terminal wasn't using my conda environment
* The solution (fixed after navigating 7-layers down in the vscode GUI):
* Find code->preference->setting->Features->Terminal->Integrated>Env:Osx
* Choose edit in settings.json
* Add the following
```
"terminal.integrated.env.osx": {  
          "PATH": null
 }
```
* Restart vscode (e.g., from the command line: vscode .) and `which python` is python in the conda environment
* This worked, but I'm not sure why. I suspect there's an easier way, in which case I'd like to know what it is.

## vscode (by microsoft) has trouble with mac in general

* [Possible explanation?](https://youtu.be/0eEG5LVXdKo?t=637)
