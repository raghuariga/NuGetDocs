﻿# Setting up the NuGet Development Environment
So you want to hack on NuGet? These notes will help you get your development environment 
set up correctly so you can work on NuGet using Visual Studio 2010.

## Get and Build the code
1. **Install Git.** Install [Git for Windows](http://code.google.com/p/msysgit/downloads/list?can=3) and then optionally install [TortoiseGit](http://code.google.com/p/tortoisegit/downloads/list)
1. **Clone the repository.** From a command prompt, run the following command in a directory where you want the source code to be placed. 
This will create a folder named "nuget" with the source.

        git clone https://git01.codeplex.com/nuget
1. If you are using VS2010 then,
    1. **Download and install the <a href="http://visualstudiogallery.msdn.microsoft.com/en-us/25622469-19d8-4959-8e5c-4025d1c9183d?SRC=VSIDE">Visual Studio 2010 SDK</a>** 
    1. **Run build.cmd** from a Command Prompt
1. If you are using VS2012 then,
    1. Uninstall the existing NuGet Extension from Visual Studio.
    1. **Download and install the <a href="http://www.microsoft.com/en-us/download/details.aspx?id=30668">Visual Studio 2012 SDK</a>**
    1. **Run build.cmd** from a Command Prompt
1. For more information on using GIT, you may refer to <a href="http://think-like-a-git.net/">http://think-like-a-git.net/</a>

## Setup Debugging for VS2012/VS2010
To debug the console and UI during development, following these steps:

1. Launch Visual Studio as Administrator 
1. Make sure that the NuGet Extension is UNINSTALLED from your primary instance of VS so your newly compiled one can load into the experimental instance.
1. Set the **VsExtension** project as the startup project 
1. Ensure you rebuild the **VsExtension** project. 
1. Now you can run or debug the **VsExtension** project and this would launch a separate instance of VS2012/VS2010 (called the Experimental instance) 
with a copy of the NuGet vsix installed. What you do in this instance don't affect the main VS instance. 

## Setup Debugging for VS2013
To debug the console and UI during development, following these steps:

1. Launch Visual Studio as Administrator 
1. Make sure that the NuGet Extension is UNINSTALLED from your primary instance of VS so your newly compiled one can load into the experimental instance.
1. Set the **VsExtension** project as the startup project 
1. Ensure you rebuild the **VsExtension** project. 
1. Now you can run or debug the **VsExtension** project and this would launch a separate instance of VS2013 
with a copy of the NuGet vsix installed. What you do in this instance don't affect the main VS instance. 

More Info See http://docs.nuget.org/docs/start-here/installing-nuget

## Developing NuGet on Linux

### Developing on OpenSUSE
The easiest distribution to use is OpenSUSE. Install OpenSUSE 12.3, then follow these steps:

1. **Install Git**

        sudo zypper install git
1. **Install Mono**
Open firefox, go to <a href="http://software.opensuse.org/find">http://software.opensuse.org/find</a>. 
Search package "mono-complete". In the result page, click "Show other versions". 
Install version 3.2.3 from repository openSUE Factory. 

1. **Import Trusted Root Certificates**. By default, Mono trusts no one. 
The NuGet build needs to install some packages from https://www.nuget.org, 
and without neccessary root certificates this will fail. Run
this command to import trusted root certificates from Mozilla's LXR into 
Mono's certificate store:

        mozroots --sync --import
1. **Clone the repository** 

        git clone https://git01.codeplex.com/nuget

1. **Build NuGet**
Cd to the nuget source code direcotry, run

        ./build.sh
This will build NuGet.exe successfully.

### Developing on Debian

To build NuGet code on Linux Mint 14.1, follow these steps:

1. **Install Git**. 

        sudo apt-get install git
The git that I got is an old version (v 1.7.10.4) that will fail to clone the NuGet
repository. So I need to get the latest git source code and build it:
 
        sudo apt-get install libssl-dev libcurl4-openssl-dev libexpat1-dev
        git clone https://github.com/git/git.git
        cd git
        make prefix=/usr/local all
        sudo make prefix=/usr/local install
Then run `hash -r` to clear bash's cache so that the new version of git will get executed by bash.
1. **Clone the repository** 

        git clone https://git01.codeplex.com/nuget
1. **Build Mono**. Do not use apt-get to install Mono since the installed 
version is 2.X, which cannot build the NuGet code successfully. 
Building NuGet requires Mono >= 3.2.
  1. Get the Mono 3.2.3 source code tarball from <a href='http://download.mono-project.com/sources/mono/'>http://download.mono-project.com/sources/mono/</a>.
  1. Unzip the tarball using `tar -xjvf mono-xxx.tar.bz2`.
  1. Compile and install Mono.
    <pre><code>sudo apt-get install g++
cd mono-xxx
./configure --prefix=/usr/local
make
sudo make install
</code></pre>

1. **Import Trusted Root Certificates**. Import trusted root certificates from Mozilla's LXR into 
Mono's certificate store:

        mozroots --sync --import
1. **Build NuGet**
Now we can finally build NuGet. Cd to the nuget source code direcotry, run

        ./build.sh
This will build NuGet.exe successfully. 

 


