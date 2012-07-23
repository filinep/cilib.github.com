---
layout: post
title: "Getting Started for Developers"
description: ""
category: 
tags: []
---
{% include JB/setup %}

The following instructions will help you get CIlib running in a few simple steps.
Note that these instructions are for *nix environments.

### Step 1: Install the required programs

#### Install SBT version 0.11.3-2 or later

SBT (Simple-build-tool) is the build tool used by CIlib. Install it by
following the instructions on the SBT 
[Getting Started page](https://github.com/harrah/xsbt/wiki/Getting-Started-Setup).

Make sure SBT is setup correctly by typing the following on the command line:

    $ sbt --version

The output should be similar to "sbt launcher version 0.11.3-2."

#### Install Git

If you are going to be working with CIlib's source code you will need to install Git.
Follow the instruction [here](http://git-scm.com/book/en/Getting-Started-Installing-Git)
to install Git.

Make sure Git is setup correctly by typing the following on the command line:

    $ git --version

The output should be similar to "git version 1.7.9.5."


### Step 2: Get the source code

If you want to contribute to CIlib (\*Jedi mind trick\* "You want to contribute to CIlib")
you should get a [Github account](https://github.com/signup/free).

Once you have an account fork the CIlib repository by clicking the "Fork" button
on the top right of the [CIlib Github page](https://github.com/cilib/cilib)

Once you have forked the repository you need to clone it to your local machine.
Start by creating a folder where the source code be placed (`~` is your home folder):

    $ mkdir ~/cilib

then clone your repository (USERNAME is your Github username):

    $ git clone http://github.com/USERNAME/cilib.git

Once everything is downloaded, add the CIlib repository as an upstream remote repository:

    $ git remote add upstream http://github.com/cilib/cilib.git


### Step 3: Compile CIlib

Compile CIlib using SBT as follows by changing to CIlib's source directory:

    $ cd ~/cilib

run SBT and clean, compile and assemble CIlib:

    $ sbt
    > clean
    > assembly
    > exit

These steps will download all the dependencies and may take some time to finish.
The final assembled jar is placed in `~/cilib/simulator/target/` and is called 
`simulator-assembly-0.8-SNAPSHOT.jar`


### Step 4: Set up a running script and test

Create a file called `simulator.sh` and place the following in the file:

{% gist 3122738 %}

`${CILIB_ASSEMBLY}` is the location of the assembled CIlib jar file (in this case
`~/cilib/simulator/target/simulator-assembly-0.8-SNAPSHOT.jar` and `${JAVA_OPTS}` 
are options sent to java mainly for memory management e.g. `-Xms512m -Xmx2g`.

Make sure the file is executable and on the system path with the following:

    $ chmod +x path/to/simulator.sh
    $ export PATH=$PATH:path/to/simulator

Note that the export command is only applicable to your current session and will
be reset when you exit the command line. To make the change permanent consult the
documentation for your particular distro regarding setting variables.

Finally test the simulator script with the following:

    $ simulator.sh ~/cilib/simulator/xml/ga.xml

If no errors occurred CIlib has been successfully set up.


### Step 5 (Optional): Set up your IDE

TODO: add instructions (links?) to set up different IDEs/editors/kitchen sinks/etc


### Troubleshooting

TODO: accessing data folder
TODO: path issues
TODO: proxy issues

