# uipf

In general, I prefer to use [IceFloor 2.0](http://www.hanynet.com/icefloor/) when I'm editting and configuring `pf` policies on OS X systems. I also prefer to keep my local policy for filtering out of /etc because Apple.

So I'll do my best to keep this somewhat current and reasonably useful as a starting point for anyone that wants to do something similar. 

You'll find the rules and tables I've defined for routable and non-routable address space on campus live in `Library/IceFloor` and my startup script is in `etc/` and is spawned by a LaunchDaemon job that is added at boot, `Library/LaunchDaemons/com.hanynet.icefloor.plist`

Installing IceFloor will do that for you once you run it the first time and answer some questions, then you can insert my files or updated versions of your own. If this ever ends up being something more rigorously maintained I'll probably create a script to merge my recommended networks and tables into an existing policy. 

The stuff you probably care about are the defined networks and services. `paris` is an OS X Server host and runs an ssh daemon on an alternate port [^1]. It also uses multi-factor authentication for ssh connections but I don't filter outgoing traffic, only incoming, so it doesn't require anything special for that.


## NOTE

### MIND THE EGRESS INTERFACE

In `icefloor.tables` the table named `<_outbound_egress>` is defined as my local interface's ipv4 address for `paris.its`. You should make that match your own especially if you plan on doing anything with dummynet, monkeying with NAT or rate shaping, etc.


----

[^1]: I wrote about using alternate ports with ssh(1) if you're interested: [@incumbent.org](http://incumbent.org/post/alternate-ssh-for-osx/)
