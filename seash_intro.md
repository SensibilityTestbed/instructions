# An Introduction to `seash`, the Experiment Management Tool

`seash` is Sensibility Testbed's experiment management tool. It is a
Python 2 program that runs on your desktop or laptop, and uses
cryptographic keys to access the customized Sensibility Testbed app
installed on your Android smartphone or tablet.

This document provides a short overview of its capabilities and usage.

**Note:** If you haven't set up `seash` or the Sensibility Testbed app yet, please
follow the [setup guide](Setup.md).



### Starting `seash`

* Open a terminal
* Change into the directory where you unzipped `seash`
* Start `seash` using the Python interpreter.

This results in the following:

```
$ cd path/to/demokit
$ python seash.py
- You can press the Tab key to enable tab complete when typing commands.

Enabled modules: execute, factoids, geoip, modules, runtests, uploaddir, variables 

 !> 
```



### Set Up Your Experiment Session

In order to control your Android device, `seash` needs the cryptographic
keys configured for your Sensibility Testbed app installation. The default
user name is `user`. Load the key pair, enabled it, discover your Android
device, and set it the active target for the following control commands.
```
 !> loadkeys user
 !> as user
 user@ !> browse
 ['192.168.99.10:1224']
Added targets: %1(192.168.99.10:1224:v1)
Added group 'browsegood' with 1 target
user@ !> on browsegood 
user@browsegood !> 
```



### Sending Commands

With the `seash` session all set up, here are the most important control
commands.

* `run PROGRAM` uploads the named program to the device and starts it.
* `show log` prints the sandbox log that an experiment can write into.
* `stop` tells the sandbox to stop the current program.

Other useful commands include:

* `upload FILE` copies the file from the laptop to the sandbox.
* `start UPLOADEDFILE` executes a file that was previously uploaded.
* `download FILE` copies the file from the sandbox to the laptop.
* `reset` removes all files from the sandbox, and clears the log.

