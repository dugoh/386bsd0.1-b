# 386bsd0.1-b

This is part II of an automated redo of http://gunkies.org/wiki/Installing_386BSD_on_BOCHS. Due to time constraints within Travis it is not possible to redo the full guide in a single repository. For part I see https://github.com/dugoh/386bsd0.1.

Prebuild binaries for bochs and qemu are pulled in together with the bochs disk image from part I. The first patchkit is installed and GENERICISA is compiled using bochs. After this a full buildworld is done with an old version of qemu, as bochs is too slow and modern qemu fails to boot 386BSD.

For hints on how to build qemu 0.11 on a modern system see https://github.com/dugoh/oldqemu

All artifacts are pushed to https://dugoh.github.io/386bsd0.1-b/. The disk is bzip2 compressed and then split into 50MB parts. Grabbing the disk is simple.

```
for i in a b c; do \
  wget -O - https://dugoh.github.io/386bsd0.1-b/qdisk.part-a${i};\
done|bunzip2 >qdisk.img
```

386BSD with the first patchkit should run in qemu 0.11 with:

```
qemu -L /usr/local/share/qemu/ \
     -curses                   \
     -hda qdisk.img            \
     -M isapc                  \
     -net nic                  \
     -no-reboot                \
     -m 64                     \
     -startdate "1994-04-22"'
```

The second patchkit is already on the filesystem and you can pick up the guide at [Sixth_boot, patched and recompiled system](http://gunkies.org/wiki/Installing_386BSD_on_BOCHS#Sixth_boot.2C_patched_and_recompiled_system).


# Warning

This is being maintained with github and travis-ci as the IDE, I don't do branches and have no qualms using master as a scratch pad. Hic Sunt Leones, here be dragons, buyer beware, sorry for the ugly commit messages and all that.

# Current build status

-    Part I    
[![Build Status](https://travis-ci.org/dugoh/386bsd0.1.svg?branch=master)](https://travis-ci.org/dugoh/386bsd0.1)

-    Part II   
[![Build Status](https://travis-ci.org/dugoh/386bsd0.1-b.svg?branch=master)](https://travis-ci.org/dugoh/386bsd0.1-b)
