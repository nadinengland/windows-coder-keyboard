# Coder - Programming Keyboard Layout

> Motive: keyboards have a numpad which results more `Shift+NumberRow` key presses than `NumberRow` ones.
>
> Be prepared to retrain your muscle memory.

Windows Keyboard Layout Creator project to create a programmering keyboard layout. The layout switches the number rows `1-0` with the symbols `!-)` on shift. It also does so for `[]` and their shift characters `{}`. **NOTE** `@` and `"` are also switched around as I typically code on a Mac enviroment, this can be easily changed in the editor.

## Install

 - Install [Windows Keyboard Layout Creator 1.4](https://www.microsoft.com/en-gb/download/details.aspx?id=22339).
 - Open `Coder.klc`.
 - Create installer `Project -> Build DLL and Setup Package`.
 - Run the installer `Coder/setup.exe`.
 - Restart Windows
 - Change to use Keyboard Layout through Windows Language settings in Control Panel. You'll find it called `Coder` under the `English (United Kingdom)`.

## Uninstall

 - Remove the registry keys by either:
   - Rerunning `Coder/setup.exe` and using the uninstall tool.
   - manually removing them from `HKEY_LOCAL_MACHINE/SYSTEM/ControlSet001/Control/Keyboard Layouts/{GUID}`. You'll have to poke around to find the right guid folder, look out for the "Coder" description.
 - Remove the System .dll file from `%SystemRoot%/System32/Coder.dll`. On 64bit there will also be one at `%SystemRoot%/SysWOW64/Coder.dll`.

## Thar be Dragons

At the time of writing v1.4 of the Keyboard Creator has a few bugs. Things to note if you want to make changes:

 - Parsing of the name field incorrectly reads the first 8 character of the file's name. This field is used for the .dll and as such can't use non-alpha symbols. If you do rename the file be sure to correct the name field in `Project -> Properties...` everytime the project is opened.

   A project file named `IncorrectDllName.klc` with the following contents:

   ```
   KBD	CorrectDllName	"Coder"
   ...
   ```

   Will populate the name field with `Incorrec`.

 - The uninstaller doesn't remove the `%SystemRoot%` files it creates on install.
 - The the .klc seems to have two description fields. The first one is editable in `Project -> Properties...` and is used for the Project's name (i.e. title bar of Creator when the project is open).

   The other field is located at the bottom of the .klc file itself, under `DESCRIPTIONS`. This is used for the Windows Language description. This is only editable through the Creator on the very first save of the project (just after `File -> New/Load Existing Keyboard.../etc`); subsequent changes to this field only effect the first descriptions field.

   If you want to change this you must do it manually. Its advisable to use the Creator to change the field first, as there is validation on the input string, then copy and paste it over the `DESCRIPTIONS` section of the file. Note that the latter does not have surrounding quotes.
