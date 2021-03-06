execInChroot provides some scripts that allow to transparently execute commands that run inside a chroot environment.

Prerequisites: a chroot environmit accessible with schroot.

###files
* enable.source   ... Sets up the environment to be able to execute commands located in the current directory in the configured chroot. Adjust the variable MAP_TO_CHROOT to the name of the schroot you want commands to be executed in.
* disable.source  ... Unsets MAP_TO_CHROOT and removes current directory from PATH.
* helpers.source  ... Some helper functions.
* gcc             ... Example command for gcc
* make 	          ... Example command for make

###usage
You can add a custom command by adding a bash script with the name same name then the command that you want to execute inside the chroot (see existing example commands "gcc" and "make"). The content of every command are the same 4 lines:

    #!/bin/bash
    DIR="$( cd "$( dirname "$0" )" && pwd )" # get directory of current file
    source ${DIR}/helpers.source
    execInChroot $0 "$@"

e.g.: you want the command "cmake" to be execute inside the chroot, just add a file called "cmake", add the 3 lines from above and give the file execute permissions. In the shell where you want to use the commands, just execute "source enable.source" once. Now, when you call cmake, the cmake inside your chroot is executed.

