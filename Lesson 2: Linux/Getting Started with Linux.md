# Getting Started with Linux

It can be overwhelming to use a new operating system when you don't have any experience using it. To get experience, it is best to download and use it. 

Here are a few ways to get started with Linux:

* Use a VM
* Use Docker
* Use WSL
* Use the cloud
* Dual boot
* Install on bare metal


## Use a VM
Pros:
* Free
* Reversable
* Can share files with the host OS
* Most realistic experience

Cons:
* Somewhat difficult if you're not experienced setting up VMs
* Can take up a significant amount of hard drive space

## Use Docker
Pros:
* Easy to use
* Easy to reset if broken

Cons:
* May be command line only (I haven't tested)
* Easy to accidentally delete
* May require WSL

## Use WSL
Pros:
* Extremely easy installation
* Most CLI based tools can be installed and used normally

Cons:
* Only works on Windows (not MacOS)
* Some things just don't work the way they should on WSL. Many things that require a GUI just don't work.
* Setting up a GUI requires configuration for a remote desktop connection which increaces latency (it is kind of laggy)

## Use the Cloud
Pros:
* Easy setup and removal
* You can use more powerful hardware than you normally could
* You can access it from anywhere

Cons:
*  It costs money. Realistically, you can get a low-spec VM in EC2 for pretty cheap, and they even give you free credits when you make an account. It is easy to leave one on accidentally one day, then get a bill every month until you remember to shut it down.

## Dual Boot
Pros:
* You get all of the Pros of installing on bare metal without needing to get rid of any existing OSs.

Cons:
* Easy to mess up and accidentally wipe your existing OS
* You need to reboot whenever you switch OSs
* You have to share your hard drive space between two OSs

## Install on bare metal
Pros:
* You get all of the benefits of running Linux in a way that pretty much just works and is well supported
* No performance overhead
* Linux desktop OSs are actually *really* nice to use most of the time

Cons:
* Bleeding edge hardware may not be supported for a few weeks
* This can be destructive if you plan on repurposing an existing laptop or desktop (you may end up wiping a Windows or MacOS installation)