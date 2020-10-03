---
title: "OneDrive VCS is the best VCS"
date: 2020-10-02T19:53:10-03:00
summary: A seemingly odd build error ends up being the biggest discovery in VCS made in the recent years.
---

Today's tale starts with a user requesting help with building the main repository and `mvn install` was returning an 'odd' error:
```
Failure to find net.runelite:client-patch:pom:1.6.24.2-SNAPSHOT in https://jcenter.bintray.com was cached in the local repository, 
resolution will not be reattempted until the update interval of central has elapsed or updates are forced
```
This already raises some eyebrows as the main repo does not have any dependencies from jCenter at all so something funky is
definitely going on. Upon being asked what the heck he's trying to build, the user simply replies that he's trying to update
a build that he modified himself, which, again, is odd because if he managed to get working in the past, then why can't he get it
working now?

Continuing the show, now it is requested that the user clones the current, clean, RuneLite repository and attempt to build it,
just to be double sure. After a brief moment, the user returns claiming that it successfully built it but when he attempts to 
`mvn install`, he encounters the following error: 

```
Failed to execute goal org.apache.maven.plugins:maven-compiler-plugin:3.6.1:compile (default-compile) on project http-service: 
Error reading old mojo status 
C:\Users\<removed>\OneDrive\Workspace\Java\runelite\http-service\target\maven-status\maven-compiler-plugin\compile\default-compile\inputFiles.lst
```

Which raises even more eyebrows as somehow maven is breaking? 

But, if you pay enough attention, you'll spot today's WTF, the user is actually building inside a OneDrive managed folder, which
explains why maven's temporary files are seemingly disappearing, OneDrive is probably going HAM trying to figure out what the fuck
is going on.

Upon asked on why the heck he's building it inside OneDrive the user simply claims that he periodically backs up everything to OneDrive.
You know, RuneLite uses Git for a reason, right? Also, let's not mention the fact the buttload of files inside the `.git` folder that
just take space & indexing time from OneDrive.

If you liked this post and have your own RuneLite WTF story, feel free to submit it through the repo [here](https://github.com/hex-agon/thedailyrunelite.wtf).