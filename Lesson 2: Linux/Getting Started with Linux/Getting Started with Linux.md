# Getting Started with Linux

It can be overwhelming to use a new operating system when you don't have any experience using it. To get experience, it is best to download and use it. Most of these sections assume you have a computer that is already running Windows or MacOS.

Here are a few ways to get started with Linux:

* Use a VM
* Use Docker
* Use WSL
* Use the cloud
* Dual boot
* Install on bare metal


## Use a VM
### Overview:
Using a VM is probably the easiest way to get started. To do this, you will need to install a hypervisor on your computer. VMWare Workstation Player is a good choice, and should be free for personal use. It is easy to use, and works well for most desktop virtualization needs. It can be downloaded from their website [here].(https://www.vmware.com/content/vmware/vmware-published-sites/us/products/workstation-player/workstation-player-evaluation.html.html). Look at the lesson on virtualization for more information on installing and using a VM. Other hypervisors are available if desired.

### Pros:
* Free
* Reversable
* Can share files with the host OS
* Most realistic experience

### Cons:
* Somewhat difficult if you're not experienced setting up VMs
* Can take up a significant amount of hard drive space
* There is a bit of a performance hit when running in a virtual environment. This is generally only 1-3%, and shouldn't affect most workloads.
* Disk files can consume a significant amount hard drive space

## Use Docker
### Overview:

### Pros:
* Easy to use
* Easy to reset if broken

### Cons:
* May be command line only (I haven't tested)
* Easy to accidentally delete
* May require WSL

## Use WSL
### Overview:

### Pros:
* Extremely easy installation
* Most CLI based tools can be installed and used normally

### Cons:
* Only works on Windows (not MacOS)
* Some things just don't work the way they should on WSL. Many things that require a GUI just don't work.
* Setting up a GUI requires configuration for a remote desktop connection which increaces latency (it is kind of laggy)

## Use the Cloud
### Overview
The cloud is a great way to get started with Linux without any risk of messing up your own computer. The setup is very similar to setting up a VM. A servcie like AWS EC2 (Amazon Web Services Elastic Compute Cloud) is a good option for this.
### Pros:
* Easy setup and removal
* You can use more powerful hardware than you normally could
* You can access it from anywhere
* Requires no hardware resources

### Cons:
*  It costs money. Realistically, you can get a low-spec VM in EC2 for pretty cheap, and they even give you free credits when you make an account. It is easy to leave one on accidentally one day, then get a bill every month until you remember to shut it down.
* It is exposed to the internet by default and needs to be secured

## Dual Boot
### Overview: 
Dual boot *can* be a good option, but I'd generally recommend using a VM if you can. If you use a VM, you don't have to reboot to use Linux and you can share files with your VM which can make life much easier. A VM has almost all of the pros of dual boot, but negates most of the cons. This is technically a bare metal install as well, so many of the pros and cons listed there also apply. 

### Pros:
* You get all of the Pros of installing on bare metal without needing to get rid of any existing OSs.

### Cons:
* Easy to mess up and accidentally wipe your existing OS
* You need to reboot whenever you switch OSs
* You have to share your hard drive space between two OSs

## Install on bare metal
### Overview
Installing Linux on bare metal can be a little risky. If you botch the install on your only working computer, it can be hard to fix (since it is difficult to look up how to fix it without a working computer). If you plan on installing Linux on your only computer, I'd recommend getting a replacement hard drive so you don't get left in a bad spot if you mess up the install or decide to switch back to your old OS. That being said, if you have an old computer that has no more valuable data on it or if you have a Raspberry Pi, this is not really a concern and can be a great and inexpensive way to go.
### Pros:
* You get all of the benefits of running Linux in a way that pretty much just works and is well supported
* No performance overhead
* Linux desktop OSs are actually *really* nice to use most of the time

### Cons:
* Bleeding edge hardware may not be supported for a few weeks
* This can be destructive if you plan on repurposing an existing laptop or desktop (you may end up wiping a Windows or MacOS installation)