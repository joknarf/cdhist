# cdhist
cd history (bash / ksh / zsh / ash)
(compatible macos / debian / centos ...)

simple cd history, alias builtin cd to add cd history

rapidily swich to already visited directories

# usage

```shell
$ . ./cdhist
$ cd <dir>
=> change to <dir> and add <dir> to $CDHISTFILE
$ cd --
=> display current history / choose dir to change
$ cd -- <pat>
=> search pattern <pat> in current history, change to dir if unique, display / chose dir either
$ cd - <pat>
=> search pattern <pat> in cd history, change to dir first matched
```
instead of `cd -- <opts>` you can use `cdd <opts>`

## example

```shell
user@host:~ $ cd ~/puppet/modules/apache/manifests
user@host:~/puppet/modules/apache/manifests $ cd ../hieradata
user@host:~/puppet/modules/apache/hieradata $ cd ../../os_prereq/manifests
user@host:~/puppet/modules/os_prereq/manifests $ cd ../hieradata
user@host:~/puppet/modules/os_prereq/hierdata $ cd --
1:~/puppet/os_prereq/manifests
2:~/puppet/apache/hieradata
3:~/puppet/apache/manifests
cd: 2
user@host:~/puppet/modules/apache/hieradata $ cd -- manif
1:~/puppet/os_prereq/manifests
2:~/puppet/apache/manifests
cd :
user@host:~/puppet/modules/apache/hieradata $ cd -- os_pr /man
user@host:~/puppet/modules/os_prereq/manifests $ cdd apa hiera
user@host:~/puppet/modules/apache/hieradata $ cdd
1:~/puppet/modules/os_prereq/manifests
2:~/puppet/modules/apache/hieradata
3:~/puppet/modules/os_prereq/hieradata
cd: prereq
1:~/puppet/modules/os_prereq/manifests
2:~/puppet/modules/os_prereq/hieradata
cd: hiera
user@host:~/puppet/modules/os_prereq/hieradata $ cd - manif
user@host:~/puppet/modules/os_prereq/manifests $
```

# environment variables

`CDHISTFILE` : path to history file (default to ~/.cd_history)

`CDNBDIRS`   : Number of directories in history to display (default 10)

`cd -- -a` or `cdd -a` will display full history
