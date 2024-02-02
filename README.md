# cdhist

Navigate through directories / history of visited directories using arrow keys from command line.
Compatibility : bash / ksh / zsh
(compatible macos / debian / centos / solaris / alpine ...)

* cd history, alias builtin cd to add cd history  
  * rapidily swich to already visited directories

* can use locate (mlocate/plocate) to rapidly cd to any directory

* display / choose subdirectories of cwd

* navigate interactively into directories using left/right arrow keys (bash/zsh)

* cd autocompletion with interactive menu for bash

![cdhist2](https://github.com/joknarf/cdhist/assets/10117818/e8eb130c-9cc8-4a1d-904d-034b6d1f93b4)

* using bash/zsh in emacs or vi mode, key binding is available as shortcuts:

|key        | action                                                                    |
|-----------|---------------------------------------------------------------------------|
|<kbd>Shift</kbd>+<kbd>⇩</kbd>   | cd history                                           |
|<kbd>Shift</kbd>+<kbd>⇧</kbd>   | return to last directory in history matching pattern |
|<kbd>Shift</kbd>+<kbd>⇨</kbd>   | navigate from current directory                      |
|<kbd>Shift</kbd>+<kbd>⇦</kbd>   | go to parent dir (cd ..)                             |
|<kbd>Ctrl</kbd>+<kbd>⇩</kbd>    | search directories matching pattern in locate db     |

directory pattern can be put on command line before hitting shortcut

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
|<kbd>PgUp</kbd>/<kbd>Ctl-F</kbd>| next page                                             |
|<kbd>PgDn</kbd>/<kbd>Ctl-B</kbd>| previous page                                         |
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

