# IMPORTANT!

**I am not the Readarr Developer. I will try my best to fix all bug requests in a timely manner.**
**THIS BUILD IS NOT AN OFFICIAL READARR BUILD. I AM BUILDING THESE OFF THE GITHUB BELOW**

[Official Readarr Github](https://github.com/Readarr/Readarr)

**BY GITCLONING**
**I WILL ATTEMPT TO FIX THESE BUGS IN A TIMELY MANNER. IF YOU WANT SOMETHING MORE STABLE PLEASE DOWNLOAD THE OFFICIAL READARR APP THAT WERE CREATED BY THEM AT THE ABOVE GITHUB**
# Readarr
[![Build Status](https://dev.azure.com/Readarr/Readarr/_apis/build/status/Readarr.Readarr?branchName=develop)](https://dev.azure.com/Readarr/Readarr/_build/latest?definitionId=1&branchName=develop)
[![Docker Pulls](https://img.shields.io/docker/pulls/hotio/readarr)](https://hub.docker.com/r/hotio/readarr)
[![Backers on Open Collective](https://opencollective.com/readarr/backers/badge.svg)](#backers) [![Sponsors on Open Collective](https://opencollective.com/readarr/sponsors/badge.svg)](#sponsors)

### Readarr is in early stages of development, alpha/beta binary builds are not yet available. Use of any test builds isn't recommend, and may have detrimental effects on your library.

Readarr is an ebook (and maybe eventually magazine/audiobook) collection manager for Usenet and BitTorrent users. It can monitor multiple RSS feeds for new books from your favorite authors and will grab, sort and rename them.

## Major Features Include:

* Support for major platforms: Windows, Linux, macOS, Raspberry Pi, etc.
* Automatically detects new books
* Can scan your existing library and download any missing books
* Automatic failed download handling will try another release if one fails
* Manual search so you can pick any release or to see why a release was not downloaded automatically
* Fully configurable book renaming
* Full integration with SABnzbd and NZBGet
* Full integration with Calibre (add to library, conversion)
* And a beautiful UI

## Support

[![Discord](https://img.shields.io/badge/discord-chat-7289DA.svg?maxAge=60)](https://readarr.com/discord)
[![GitHub](https://img.shields.io/badge/github-issues-red.svg?maxAge=60)](https://github.com/Readarr/Readarr/issues)
[![Wiki](https://img.shields.io/badge/servarr-wiki-181717.svg?maxAge=60)](https://wiki.servarr.com/Readarr)

## Contributors

This project exists thanks to all the people who contribute. [Contribute](CONTRIBUTING.md).
<a href="https://github.com/Readarr/Readarr/graphs/contributors"><img src="https://opencollective.com/Readarr/contributors.svg?width=890&button=false" /></a>



## Backers

Thank you to all our backers! 🙏 [Become a backer](https://opencollective.com/readarr#backer)

<img src="https://opencollective.com/readarr/backers.svg?width=890"></a>

## Sponsors

Support this project by becoming a sponsor. Your logo will show up here with a link to your website. [Become a sponsor](https://opencollective.com/readarr#sponsor)

<img src="https://opencollective.com/readarr/sponsors.svg?width=890"></a>

## Mega Sponsors
<img src="https://opencollective.com/readarr/tiers/mega-sponsor.svg?width=890"></a>


&#x200B;

First off i want to say thank you to reddit user u/Guinness for the starting point for CentOS non docker install. Sorry if this is not allowed. Please let me copy this to the appropriate section. I worked very hard on this and had to start over because i didnt save the original draft. I didn't see a flair for documentation so i apologize ahead of time.

Secondly you Will need a couple of neccessary dependencies

First if you are on Windows 10 You need WSL2 and a Debian or Ubuntu Distro. You can look that up as this tutorial is for installing Readarr and not WSL. But everything in here should apply to both.

# Setting up Dependencies:

**IMPORTANT:**

**IM NOT SURE IF THIS IS APPLICABLE FOR EVERYONE I HAVE GENIE INSTALLED WHICH IS WSL2 EQUIVELANT TO SYSTEMD. I WOULD HIGH RECOMMEND INSTALLING IT**

(I personally found the github genie documentation very frustrating and overwhelming)

**Genie (WSL2 Systemd Alt.)**

Please follow this tutorial posted [here](https://gist.github.com/djfdyuruiry/6720faa3f9fc59bfdf6284ee1f41f950)

Once Done test it to make sure it is working

    wsl genie -s 

**Installing Git:**

    sudo apt install git -y

**Installing Curl:**

    sudo apt install curl -y

**Yarn Install:**

Next We need to Install Yarn

Way #1 PPA: **(RECOMMENDED)**

    curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
    
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
    
    sudo apt update && sudo apt install yarn

Way #2 **NPM (Recommended):**

I personally dont like using NPM mainly because of how big the package is to download but if thats your cup of tea here you go!

    npm install -g yarn

Once you have installed using either method run the command below to check it.

    yarn --version

**Installing .NET 5 Runtime to only run Programs:**

Run the Below Command if  you are using Ubuntu 20.04 Terminal:

    wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
    
    sudo dpkg -i packages-microsoft-prod.deb

Install the SDK:

    sudo apt-get update; \
      sudo apt-get install -y apt-transport-https && \
      sudo apt-get update && \
      sudo apt-get install -y dotnet-sdk-5.0

Install the Runtime:

    sudo apt-get update; \
      sudo apt-get install -y apt-transport-https && \
      sudo apt-get update && \
      sudo apt-get install -y aspnetcore-runtime-5.0

FOR ALL OTHER PLEASE USE DOCUMENTATION HERE TO INSTALL ON ANY OTHER LINUX OPERSATING SYSTEM

[Documentation for All Linux Install of .NET 5](https://docs.microsoft.com/en-us/dotnet/core/install/linux)

Also I would recommend you install the Windows Native .NET 5.0 EXE at the below link

[.NET 5 Windows Installers and Scripts](https://dotnet.microsoft.com/download/dotnet/5.0)

&#x200B;

**NOTE: YOU NEED TO INSTALL THE .NET SDK AND .NET RUNTIME FOR THIS TO WORK!**

# Building Readarr:

So if you are using WSL2 on Windows 10 you should open a new tab in Windows Terminal Windows in your Debian or Ubuntu based distro.

ie. Ubuntu 20.04

**Directory Setup**

it will most likely bring you to directory like this `/mnt/c/Users/(Your Windows Account)`

Once in that directory we have to make a couple of new directories

    sudo mkdir apps
    
    cd apps
    
    sudo mkdir build
    
    cd build

**Gitcloning the Repo**

     git clone https://github.com/Readarr/Readarr

**Running the Build:**

We first need to navigate inside the build directory to the Readarr directory that just pulled from github

    cd readarr

Now check to see if the build.sh is in the Readarr directory

    ls

If it is now run the build

If you want to build all Windows, Linux, and MacOS run below

    bash build.sh

Now go to the subfolder and collect the outputs if your on Windows using WSL2 you can just go to 

`C:\Users\(YourWindowsUser)\apps\build\Readarr_output\`

and select the latest netx.x folder for example below mine is net5.0

ie.  `/mnt/c/Users/DemonWarrior/apps/build/Readarr/_output/net5.0`

Inside that folder you will have all the built files to run on any system.

ie. `C:\Users\DemonWarrior\apps\build\Readarr\_output\net5.0\win-x64\publish`

Once you have this folder you can either move it to another destination anywhere on the OS.

I have copied mine to `C:\Tools\\Readarr`

then execute inside the folder you moved it to for example on Windows 10 x64 I ran ServiceInstall.exe as an administrator and now the service for Readarr on Windows 10 x64 is installed.

You can also run Readarr.console.exe as a service using NSSM

Enjoy and Rejoice!

If anyone is too lazy to do this i have already uploaded the pre-built working folders for the different Operating systems on the releases.

&#x200B;
### License

* [GNU GPL v3](http://www.gnu.org/licenses/gpl.html)
* Copyright 2010-2021
