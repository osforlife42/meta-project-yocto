# yocto course 

## part 2 
### git projects
SRCREV  - the revision of the git project 
to use always the latest revision use: 
SRCREV = "${AUTOREV}"

## part 3
much needed bitbake variables are in: 
poky/meta/conf/bitbake.conf

do not add the same file to two packages. it will go only into one of them. 

### dependencies
specific versions of recipes can be defined like this: 

```
DEPENDS = "recipe-b (>= 1.2)"
RDEPENDS_${PN} = "recipe-b (>= 1.2)"
```
=, <, >, >=, <= operators are available

to generate dependency information for a recipe, run :
$ bitbake -g recipename

for dependency explorer gui : 
bitbake -g -u taskexp recipename

### autotools 
for out-of-tree builds (build directory is different than source directory) use: 
inherit autotools-brokensep (vs inherit autotools)



### devshell 
a development shell that runs in the same context as the bitbake task engine
the commands execute just as if the build system was executing them.
bitbake -c devshell <recipename>

for example we can view the system variables 
in the temp folder of the workdir there are all (among other things) all the commands the yocto has executed, so in the devshell you are able to repeat them. 

IMPORTANT POINT - 
the changes in the devshell are local to the build it is executed in. 
one way to keep track of these local changes outside is to create a git repo of the files being wworked on and commiting on every change and then using: 
git format-patch 

to create auto-patches using git outside the build environment

### files path
when a file is included in SRC_URI bitbake searches for FILESPATH and FILESEXTRAPATH variables


## part 4 
### introduction 
setscene - a task which helps reusability for bitbake. 

SSTATE_DIR - the location of the state cache directory

types of clean - 
bitbake -c clean - removes all output files for a target from the do_unpack task onwards

bitbake -c cleanall - removes all output files and shared state cache and downloaded source files for a target 

bitbake -c cleansstate - removes all output files and shared state cache for a target


