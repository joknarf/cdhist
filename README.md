As another project called cdhist on github, decided to rename this project `seedee`
Now, the updated tool can be found [here](https://github.com/joknarf/seedee)
This repository won't we updated anymore

# cdhist

Navigate interactively through directories / history of visited directories using arrow keys from command line.  
Compatibility : bash / ksh / zsh  
(compatible macos / debian / centos / solaris / alpine ...)

* rapidily switch to already visited directories using interactive menu
* use locate (mlocate/plocate) to rapidly cd to any directory
* navigate interactively into directories/history using left/right arrow keys in menu
  * directly from command line without any cd command using shift-arrow keys (bash/zsh)
* cd autocompletion with interactive menu (bash)

for a complete next-gen shell experience, see also these projects:
* [nerdps1](https://github.com/joknarf/nerdps1) : auto-transportable dynamic PS1 prompt (you can see it in the demo)
* [redo](https://github.com/joknarf/redo) : replacement of shell history command search (Ctrl+R or Esc+/) with interactive menu
* [complete-ng](https://github.com/joknarf/complete-ng) : nextgen bash completion with interactive menu

![demo](https://github.com/joknarf/cdhist/assets/10117818/ad3dc445-ba78-401e-9e46-ca87e73fdb3b)

* using bash/zsh in emacs or vi mode, key binding is available as shortcuts:
  * default key binding with <kbd>Shift</kbd>+<kbd>Arrows</kbd> or <kbd>Ctrl</kbd>+<kbd>Arrows</kbd> (can be overridden using CD*BIND variables)

<div align="center">
 
|Left                     | Up/Down                             | Right                       |
|:-----------------------:|:-----------------------------------:|:---------------------------:|
|                         |  previous dir in history            |                             |
|                         | <img width="50px" src="https://github.com/joknarf/cdhist/assets/10117818/10ac2573-49fc-4ed5-8a6e-cce931c55ae2">| |
| <img width="50px" src="https://github.com/joknarf/cdhist/assets/10117818/015131c5-8d8d-4c0d-8d44-a876fa6f2fb5"> |  <img width="50px" src="https://github.com/joknarf/cdhist/assets/10117818/fe034fdc-dea5-49fa-be30-8f0bd9341208"> | <img width="50px" src="https://github.com/joknarf/cdhist/assets/10117818/1d254f15-050e-4ff9-9f5d-002e9ff4802f"> |
|  parent dir (..)         | dir history browser                | dir browser                 |

directory pattern can be put on command line before hitting shortcut to filter result  
putting on command line : `work` and hitting <kbd>Shift</kbd>+<kbd>⇧</kbd> will bring you to last visited directory containing `work`

|key                                           | action                                               |
|----------------------------------------------|------------------------------------------------------|
|<kbd>Shift</kbd>+<kbd>⇩</kbd>                 | cd history menu                                      |
|<kbd>Shift</kbd>+<kbd>⇧</kbd>                 | return to last directory in history matching pattern |
|<kbd>Shift</kbd>+<kbd>⇨</kbd>                 | navigate from current directory                      |
|<kbd>Shift</kbd>+<kbd>⇦</kbd>                 | go to parent dir (cd ..)                             |
|<kbd>Ctrl</kbd>+<kbd>Shift</kbd><kbd>⇩</kbd>  | search directories matching pattern in locate db     |

</div>

* using bash, `<tab>` cd auto completion can be enabled for `cd` command:
  * setting env variable `CDCOMPLETE=y` before sourcing `cdhist`

## keys when in menu

|key                             | action                                                |
|--------------------------------|-------------------------------------------------------|
|<kbd>⇩</kbd>                    | select next item                                      | 
|<kbd>⇧</kbd>                    | select prev item                                      |
|<kbd>End</kbd>                  | select last item                                      |
|<kbd>Home</kbd>                 | select first item                                     | 
|<kbd>⇨</kbd>                    | browse selected directory                             |
|<kbd>⇦</kbd>                    | browse parent directory                               |
|<kbd>Shift</kbd>+<kbd>⇨</kbd>   | browse selected directory with subdirectories depth 4 |
|<kbd>Shift</kbd>+<kbd>⇦</kbd>   | back to only show subdirectories depth 1              |
|<kbd>Shift</kdb>+<kbd>⇩</kbd>/<kbd>PgUp</kbd>/<kbd>Ctl</kbd>+<kbd>F</kbd>| next page    |
|<kbd>Shift</kdb>+<kbd>⇧</kbd>/<kbd>PgDn</kbd>/<kbd>Ctl</kbd>+<kbd>B</kbd>| previous page|
|<kbd>Del</kbd>/<kbd>F8</kbd>    | delete directory entry in history                     |
|<kbd>Esc</kbd>                  | exit                                                  |
|<kbd>Ctrl</kbd>+<kbd>A</kbd>    | use all screen to display menu                        |
|<kbd>Enter</kbd>/<kbd>Tab</kbd> | go to directory                                       |

* filter pattern can be applied entering text
* selection can be done entering item number


# usage

```
$ . ./cdhist
$ cd <dir>
=> change to <dir> and add <dir> to $CDHISTFILE
$ cd --
=> display current history / choose dir to change
$ cd -- <pat>...
=> search pattern <pat> in current history, change to dir if unique, display / chose dir either
$ cd - <pat>...
=> search pattern <pat> in cd history, change to dir first matched
$ cd + [<pat>]...
=> display immediate subdirectories of cwd, search / choose dir to change (except dot dirs, like .git/*)
$ cd ++ [<pat>]...
=> display subdirectories until depth 4, search / choose dir to change (except dot dirs, like .git/*)
$ cdl <pat>...
=> use locate -r and get list of directories to switch
```

`cd - <opts>` `cd -- <opts>` `cd + <opts>` `cd ++ <opts>` are aliases to `cd- cd-- cd+ cd++`


# environment variables

|Variable     | Description                                                       |
|-------------|-------------------------------------------------------------------|
|`CDHISTFILE` | path to history file (default to ~/.cd_history)                   |
|`CDNBDIRS`   | Number of directories in history to display (default 10)          |
|`CDINITDIRS` | Directory list (\n separated) to initialize CDHISTFILE if empty   |
|`CDPOWERLINE`| set to "n" to disable powerline symbol usage                      |
|`CDHISTBIND` | bind key to cdhist                                                |
|`CDDOTBIND`  | bind key to navigate from current dir                             |
|`CDLBIND`    | bind key to cdlocate                                              |
|`CDUPIND`    | bind key to cd ..                                                 |
|`CDLASTBIND` | bind key to cdhist last dir matching text                         |

