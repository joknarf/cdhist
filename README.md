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
```
instead of `cd -- <opts>` you can use `cdd <opts>`

## example

```shell
user@host:~ $ cd ~/puppet/modules/apache/manifests
user@host:~/puppet/modules/apache/manifests $ cd ../hieradata
user@host:~/puppet/modules/apache/hieradata $ cd ../../os_prereq/manifests
user@host:~/puppet/modules/os_prereq/manifests $ cd ../hieradata
user@host:~/puppet/modules/os_prereq/hierdata $ cd --
1:/home/user/puppet/os_prereq/manifests
2:/home/user/puppet/apache/hieradata
3:/home/user/puppet/apache/manifests
cd: 2
user@host:~/puppet/modules/apache/hieradata $ cd -- manif
1:/home/user/puppet/os_prereq/manifests
2:/home/user/puppet/apache/manifests
cd :
user@host:~/puppet/modules/apache/hieradata $ cd -- os_pr /man
user@host:~/puppet/modules/os_prereq/manifests $ cdd apa hiera
user@host:~/puppet/modules/apache/hieradata $
```

# environment variables

`CDHISTFILE` : path to history file (default to ~/.cd_history)

`CDNBDIRS`   : Number of directories in history to display (default 10)

`cd -- -a` or `cdd -a` will display full history
