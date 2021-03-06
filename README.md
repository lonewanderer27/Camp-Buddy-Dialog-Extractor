# Camp Buddy Dialog Extractor [![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

## About

Camp Buddy Dialog Extractor is a tool that extracts dialog from Camp Buddy and Camp Buddy Scoutmasters Edition.
It can also be embedded inside another program by using its class.



## Prerequisite
Download and use [Shizmob's rpatool](https://github.com/Shizmob/rpatool) to extract Camp Buddy assets to a folder  <br>
*<sub>you should end up with a folder full of .rpy files, we are going to be extracting the character dialogs from those files.</sub>*



## Character Aliases
Use these in chosen_chars parameter. You may pick as many as you want as illustrated in the examples after this section.

I only included the characters that would make sense for someone to get the dialogs of.
Character aliases such as 'all' and 'Aiden & Goro' are not included here.

An error would occur if someone were to extract a character who's alias is not included here.

| Character | Alias |  | Character | Alias |  | Character | Alias |  | Character | Alias |
|---|---|---|---|---|---|---|---|---|---|---|
| Aiden | a |  | Natsumi | n |  | Felix | f |  | Keitaro | k |
| Andre | u |  | Naoto | na |  | Eduard | e |  | Hunter | hu |
| Goro | g |  | Guest | nag |  | Lee | l |  | Hiro | h |
| Yoshinori | yo |  | Stripper | nas |  | Kieran | ki |  | Vera | v |
| Yuri | yu |  | Bellboy | r |  | Rayne | ra |  | William | w |
| Lloyd | l |  | Masseur | m |  | Toshu | to |  | Architect | ar |
| Darius | d |  | Bartender | bt |  | Ichiru | ic |  | Hina | hm |
| Hyunjin | j |  | Reimond | r |  | Connor | co |  | Yuki | k |
| Emilia | e |  | Justine | ju |  | Jirou | ji |  | Heather | he |
| Yoichi | yi |  | Officiator | o |  | Avan | ha |  | Archer | ar |
| Taiga | t |  | Doctor | ol |  | Yuuto | yt |  |  |  |
| Haruki | hr |  | Noah | no |  | Chiaki | ch |  |  |  |

## Command Line Usage
```
usage: cb_dialog_extractor.py [-h] [-r EXCLUDE_ROLEPLAY_DIALOGS] [-e EXPORT_TO_FILE] [-d DESTINATION_FILE] [-D DESTINATION_DIRECTORY]
                              [-H [HEADER [HEADER ...]]] [-m DELIMETER] [-v VERBOSE_LEVEL]
                              source_directory game [chosen_chars [chosen_chars ...]]
```



### Options
| Positional Argument | Description                                        |
|---------------------|----------------------------------------------------|
| source_directory    | Folder Containing .rpy Files                       |
| game                | 1 = Camp Buddy 2 = Camp Buddy Scoutmasters Edition |
| chosen_chars        | Characters to extract dialogs of                   |

| Optional Argument | Description |
|---|---|
| -h, --help | show this help message and exit |
| -r, --exclude_roleplay_dialogs | Exclude roleplay dialogs <br>(default: True) |
| -e, --export_to_file | Export the dialogs to file. If False then dialogs would be exported to directory<br>(default: True) |
| -d, --destination_file | Export destination file path. Used if export_to_file is True. Ignored if export_to_file is False<br>(default: None) |
| -D, --destination_directory | Export destination directory. Used if export_to_file is False. Ignored if export_to_file is True<br>(default: None) |
| -H, --header | Header columns (default: ['name', 'dialog']) |
| -m, --delimeter | Symbol to separate the character name and their dialog (default: ;) |
| -v, --verbose_level | 0 = no output to terminal<br>1 = shows message when dialogs extraction has started and finished and where it was saved<br>2 = shows the percentage progress and the current file being worked on<br>3 = shows the character name and their dialog in real time as they get extracted<br><br>(default: 2) |
| -s, --show_stats | At the end of extraction, show the stats detailing the amount of .rpy files processed and total dialog lines per character are exported (default: True) |



###  Examples
#### Extract Keitaro's dialogs from Camp Buddy:
```
cb_dialog_extractor.py "/path/to/folder" 1 k --destination_file "/path/to/dialog.csv"
```
#### Extract Taiga's dialogs from Camp Buddy:
```
cb_dialog_extractor.py "/path/to/folder" 1 t --destination_file "/path/to/dialog.csv"
```
#### Extract Taiga and Keitaro dialogs from Camp Buddy:
```
cb_dialog_extractor.py "/path/to/folder" 1 k t --destination_file "/path/to/dialog.csv"
```
#### Extract Yoshinori's dialogs from Camp Buddy Scoutmasters Edition:
```
cb_dialog_extractor.py "/path/to/folder" 2 yo --destination_file "/path/to/dialog.csv"
```
#### Extract Yoshinori and Aiden dialogs from Camp Buddy Scoutmasters Edition:
```
cb_dialog_extractor.py "/path/to/folder" 2 yo a --destination_file "/path/to/dialog.csv"
```



## Library Usage:
### Extract Keitaro's dialogs from Camp Buddy:
```
cbdialogextractor = CBDialogExtractor(source_directory='folder that contains .rpy files', game=1, chosen_chars=['k'], destination_file='Taiga_Dialogs.csv')

cbdialogextractor.extract()
```
### Extract Taiga's dialogs from Camp Buddy:
```
cbdialogextractor = CBDialogExtractor(
                        source_directory='/path/to/folder', 
                        game=1, chosen_chars=['t'], 
                        destination_file='/path/to/dialog.csv')

cbdialogextractor.extract()
```
### Extract Taiga and Keitaro dialogs from Camp Buddy:
```
cbdialogextractor = CBDialogExtractor(
                        source_directory='/path/to/folder', 
                        game=1, chosen_chars=['k','t'], 
                        destination_file='/path/to/dialog.csv')

cbdialogextractor.extract()
```
### Extract Yoshinori's dialogs from Camp Buddy Scoutmasters Edition:
```
cbdialogextractor = CBDialogExtractor(
                        source_directory='/path/to/folder', 
                        game=2, chosen_chars=['yo'], 
                        destination_file='/path/to/dialog.csv')

cbdialogextractor.extract()
```
### Extract Yoshinori and Aiden dialogs from Camp Buddy Scoutmasters Edition:
```
cbdialogextractor = CBDialogExtractor(
                        source_directory='/path/to/folder', 
                        game=2, chosen_chars=['yo', 'a'], 
                        destination_file='/path/to/dialog.csv')

cbdialogextractor.extract()
```



### Class Parameters
| Parameter                | Type   | Description                                                                                                                                                                                                                                                                                                |
|--------------------------|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| source_directory         | str    | Folder Containing .rpy Files                                                                                                                                                                                                                                                                               |
| game                     | int    | 1 = Camp Buddy, 2 = Camp Buddy Scoutmasters Edition                                                                                                                                                                                                                                                        |
| chosen_chars             | list   | Characters to extract dialogs of. Refer to chars_aliases dictionary for the alias of each character                                                                                                                                                                                                        |
| exclude_roleplay_dialogs | bool   | Exclude roleplay dialogs. Default is True                                                                                                                                                                                                                                                                  |
| export_to_file           | bool   | Export the dialogs to file. Default is True                                                                                                                                                                                                                                                                |
| destination_file         | str    | Export destination file. Used if export_to_file param is True. Ignored if export_to_file param is False                                                                                                                                                                                                                             |
| destination_directory    | str    | Export destination directory. Used if export_to_file param is False. Ignored if export_to_file param is True                                                                                                                                                                                               |
| header                   | list   | Header columns. Default is ['name', 'dialog']                                                                                                                                                                                                                                                              |
| delimeter                | str    | Symbol to separate the character name and their dialog. Default is ;                                                                                                                                                                                                                                       |
| verbose_level            | int    | 0 = no output to terminal<br>1 = shows message when dialogs extraction has started and finished and where it was saved<br>2 = shows the percentage progress and the current file being worked on<br>3 = shows the character name and their dialog in real time as they get extracted. <br><br>Default is 2 |
| show_stats               | bool   | At the end of extraction, show the stats detailing the amount of .rpy files processed and total dialog lines per character that are exported   |
| cb_toolbox_window        | object | Camp Buddy Toolbox PySimpleGUI Window object. Only used when embedded in Camp Buddy Toolbox program<br>Default is None                                                                                                                                                                                     |


<!-- LICENSE -->
## License

Camp Buddy Toolbox is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

Camp Buddy Toolbox is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program. If not, see <https://www.gnu.org/licenses/>.



<!-- LEGAL NOTICE -->
## Legal Notice
                                
<div id="legal">
I created this tool, as a fan of Camp Buddy, for others who are also a fan (like you) to be able to create your own Discord Chatbot. 
  
However having the tool doesn't mean you have the right to share any dialog line scripts generated by this program to others online (especially the ones who did not even paid for the game) without permission from the game developer and company.  

By doing so, you're infringing on BLits Games Intellectual Property and you are subject to legal repercussions!
</div>



<!-- CONTACT -->
## Contact

Adriane James - adrianejames27@gmail.com

Project Link: [https://github.com/lonewanderer27/Camp-Buddy-Toolbox](https://github.com/lonewanderer27/Camp-Buddy-Toolbox)