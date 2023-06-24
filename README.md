# cdhist
cd history/subdir/locatedir navigation (bash / ksh / zsh / ash)
(compatible macos / debian / centos / solaris / ish ...)

* simple cd history, alias builtin cd to add cd history  
  * rapidily swich to already visited directories

* can use locate (mlocate/plocate) to rapidly cd to any directory

* display / choose subdirectories of cwd

![cdhist](https://github.com/joknarf/cdhist/assets/10117818/694e021e-e49e-4f93-8ede-228fc179e996)

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
$ cdl [<pat>]...
=> use locate -r and get list of directories to switch
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
1:./apache/hieradata
2:./apache/manifests
3:./os_prereq/hieradata
4:./os_prereq/manifests
cd: 
user@host:~/puppet/modules $ cdl usr syslog
1:/usr/lib/rsyslog
2:/usr/lib/x86_64-linux-gnu/rsyslog
3:/usr/share/rsyslog
4:/usr/share/doc/rsyslog
5:/usr/share/doc/rsyslog/examples/rsyslog.d
cd: example
user@host:/usr/share/doc/rsyslog/examples/rsyslog.d $
```

# environment variables

`CDHISTFILE` : path to history file (default to ~/.cd_history)

`CDNBDIRS`   : Number of directories in history to display (default 10)

`CDINITDIRS` : Directory list (\n separated) to initialize CDHISTFILE if empty

`cd -- -a` or `cd-- -a` will display full history
