# Setting up a Sensibility Testbed development environment

This document explains how to set up a development environment for
sensor-enabled experiments with Sensibility Testbed. You will run the
*experiment manager* program on a desktop or laptop computer, and the
*Sensibility Testbed app* whose sandbox hosts experiments on an
Android smartphone or tablet.


### Install Python 2.7
The experiment manager is written in the Python programming language.
Please make sure that you have Python 2.7 installed on your PC or laptop.
(You can download it from [the official Python website](https://www.python.org/downloads/release)).

### Download and Unzip the Experiment Manager

With Python 2.7 installed, download and unzip
[`seash`, the experiment manager](https://sensibilityclearinghouse.poly.edu/demokit/sensibility-testbed-demokit.zip)
to your computer.
Remember where you unzipped to, we will return to this directory soon.

### Configure and Install the Sensibility Testbed app

Proceed to install a customized version of the Sensibility Testbed app
that will be linked to your experiment manager:

On your laptop, browse to the [Sensibility Custom Installer Builder](https://alpha-ch.poly.edu/cib/fastlane).
Download the experimenter key zipfiles. They contain one file each,
`user.publickey` and `user.privatekey`. Put these files into the
`seash` directory created previously.

Now, using your Android device,
* Scan the QR code on the Custom Installer Builder page. This opens the Google Play app.
* Choose to "Install", then "Open" the app.
* Tap the app's "Install" button.

The app first installs Python on your Android device, then downloads
the custom installer you created previously, and finally sets up
the Sensibility Testbed nodemanager component so that sandboxes on your
device can be controlled from your laptop.

### Done!

The app shows check marks for every completed step. Four check marks
indicate that you are all set up and ready to go!
Your Android device can now run experiments under the control of your
laptop. See the [`seash` introduction](seash_intro.md) for details.
