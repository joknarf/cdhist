# cdhist
cd history (bash / ksh / zsh / ash)
(compatible macos / debian / centos ...)

simple cd history, alias builtin cd to add cd history
rapidily swich to already visited directories

display / choose subdirectories of cwd

![cdhist](https://github.com/joknarf/cdhist/assets/10117818/694e021e-e49e-4f93-8ede-228fc179e996)

# usage

```
$ . ./cdhist
$ cd <dir>
=> change to <dir> and add <dir> to $CDHISTFILE
$ cd --
=> display current history / choose dir to change
$ cd -- <pat>
=> search pattern <pat> in current history, change to dir if unique, display / chose dir either
$ cd - <pat>
=> search pattern <pat> in cd history, change to dir first matched
$ cd + [<pat>]
=> display immediate subdirectories of cwd, search / choose dir to change (except dot dirs, like .git/*)
$ cd ++ [<pat]
=> display subdirectories until depth 4, search / choose dir to change (except dot dirs, like .git/*)
```


`cd - <opts>` `cd -- <opts>` `cd + <opts>` `cd ++ <opts>` are aliases to `cd- cd-- cd+ cd++`


## example

```shell
user@host:~ $ cd ~/puppet/modules/apache/manifests
user@host:~/puppet/modules/apache/manifests $ cd ../hieradata
user@host:~/puppet/modules/apache/hieradata $ cd ../../os_prereq/manifests
user@host:~/puppet/modules/os_prereq/manifests $ cd ../hieradata
user@host:~/puppet/modules/os_prereq/hierdata $ cd--
1:~/puppet/os_prereq/manifests
2:~/puppet/apache/hieradata
3:~/puppet/apache/manifests
cd: 2
user@host:~/puppet/modules/apache/hieradata $ cd-- manif
1:~/puppet/os_prereq/manifests
2:~/puppet/apache/manifests
cd :
user@host:~/puppet/modules/apache/hieradata $ cd-- os_pr /man
user@host:~/puppet/modules/os_prereq/manifests $ cd-- apa hiera
user@host:~/puppet/modules/apache/hieradata $ cd--
1:~/puppet/modules/os_prereq/manifests
2:~/puppet/modules/apache/hieradata
3:~/puppet/modules/os_prereq/hieradata
cd: prereq
1:~/puppet/modules/os_prereq/manifests
2:~/puppet/modules/os_prereq/hieradata
cd: hiera
user@host:~/puppet/modules/os_prereq/hieradata $ cd- manif
user@host:~/puppet/modules/os_prereq/manifests $ cd- modules$
user@host:~/puppet/modules $ cd++
1. ./apache/hieradata
2. ./apache/manifests
3. ./os_prereq/hieradata
4. ./os_prereq/manifests
cd: 
```

# environment variables

`CDHISTFILE` : path to history file (default to ~/.cd_history)

`CDNBDIRS`   : Number of directories in history to display (default 10)

`cd -- -a` or `cd-- -a` will display full history
