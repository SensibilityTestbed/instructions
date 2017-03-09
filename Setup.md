# Setting up a Sensibility Testbed development environment

This document explains how to set up a development environment for
sensor-enabled experiments with Sensibility Testbed. A desktop or
laptop computer will serve as the *experiment manager*, and an Android
smartphone or tablet will run the *Sensibility Testbed app* whose
sandbox hosts experiments.


### Install Python 2.7
The experiment management tool is written in the Python programming language.
Please make sure that you have Python 2.7 installed on your PC or laptop.
(You can download it from [the official Python website](https://www.python.org/downloads/release)).

### Download and Unzip the Experiment Management Tool

With Python 2.7 installed, download and unzip
[`seash`, the experiment management tool](https://sensibilityclearinghouse.poly.edu/demokit/sensibility-testbed-demokit.zip).
Remember where you unzipped to, we will return to this directory soon.

### Configure and Install the Sensibility Testbed app

Proceed to install a customized version of the Sensibility Testbed app
that will be linked to your experiment management tool:

On your laptop, browse to the [Sensibility Custom Installer Builder](https://alpha-ch.poly.edu/cib/fastlane).
Download the experimenter key zipfiles. They contain one file each,
`user.publickey` and `user.privatekey`. Put these files into the
`seash` directory created previously.

Now, using your Android device,
* Scan the QR qode on the Custom Installer Builder page. This opens the Google Play app.
* Choose to "Install", then "Open" the app.
* Tap the app's "Install" button.

The app first installs Python on your Android device, and then sets up
the Sensibility Testbed nodemanager component so that sandboxes on your
device can be controlled from your laptop.

### Done!

Your Android device can now run experiments under the control of your
laptop. See the [`seash` introduction](seash_intro.md) for details.
