# Jupyter Lab Notebooks to create Oracle Docker Images and their testing.
These various Jupyter Lab Notebooks are focused largely around the Oracle Database and Docker. These notebooks will  document how I build out my Oracle Database environments to test new features. The notebooks cover the following areas

* Install of Jupyter Lab for use with Oracle and Docker and as a result Python, pip and virtual env.
* The creation of an Oracle Docker image from within Jupyter Notebooks using Python and Docker APIs
* The creation and of a Oracle Docker Container using the image created in the previous step again using Python and Docker APIs
* The creation of a standby database
* Installing a docker "swingbench" image to run against the created databases

I'm not saying this is the best or only way to do this... I use this method because it's simple, self documenting and trivial to change.

Happy to recieve feedback on how to improve the flow or any mistakes I've made.

## Installing Jupyter-lab and Docker environment on Mac
The following walk-through guides you through the steps needed to set up your enviroment to run [Jupyter-lab](https://jupyter.org/), [Oracle](https://www.oracle.com/database/technologies/) and [Docker](https://www.docker.com/) to build and run docker images for testing. This should work for either an on premises install or on Oracle's cloud using IaaS (Compute). This walkthough will serve primarily as a reminder to myself.

### Prerequisites
I tested this walkthrough on Mac with High Sierra but it should work on any moderately modern variant. I'm also assuming a few other things
* You have admin access.
* Comfortable using the [Terminal](https://macpaw.com/how-to/use-terminal-on-mac) utility.

#### Install
The install is pretty simple. It consists of Installing Homebrew, setting up python, installing Oracle Instant client, installing Git and then cloning this directory to the server. Lets start with setting up the Python Environment
#### Homebrew Install
[Homebrew](https://brew.sh/) is equivalent on Mac to ```yum``` or ```apt-get``` on Linux. The beauty of it is is that it enables you to install packages in "user" space rather than "admin". It's easy to use and incredibly simple to install. You can either visit the website yourself and follow their instructions or within the terminal run the following command
```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
It will prompt you through the install. **NOTE :** It's possible that it may prompt you to install the XCode command line tools. Say yes.
#### Python Setup
Mac has Python installed but it's 2.7 and comes with a whole lot of packages that are needed for this exercise. Mucking around with it's version can lead to awhole lot of trouble. The good news is we can use brew to install an upto date variant. To do this just run the command 
```bash
brew install python3
```
This might take a little while but it's worth doing. Brew should also install pip3 as part of the install but it's possible that this failed. To make sure it's usable simply run the following command
```bash
brew unlink python && brew link python
```
```pip3``` should now work and running a command like
```
pip3 list
Package    Version
---------- -------
pip        18.1 
setuptools 40.6.3
virtualenv 16.3.0
wheel      0.32.3 
```
Will show you the installed modules.

Next we can create a virtual environment and enable it.
```bash
virtualenv -p /usr/local/bin/python3 myvirtualenv
source myvirtualenv/bin/activate
```
This will create a directory called ```myvirtualenv``` (you can call it what you like) with it's own version of the python interpreter and pip. Once we "active it", any library we install will only be in this directory and won't effect the system as a whole.
#### Docker Install
You have a couple of choices here. You could just run homebrew to install docker
```
brew install docker
```
Which works fine or you might want to use the semi graphical version "Docker Desktop for Mac". This has the small advantage of notifying you of available updates. If so you can download it here

https://hub.docker.com/editions/community/docker-ce-desktop-mac

#### Git Installation
We now need to install Git which is useful for managing and versioning code. That might not be a requirement for you but it also makes it very simple to clone existing repostories. Installing it is very simple.
```bash
brew install git
```
We can now clone my IPython/Jupyter notebooks from github which provide you with the code for creating your own Oracle Docker Images.
```bash
git clone https://github.com/domgiles/JuypterLabWork.git
```
This will create a directory call ```JuypterLabWork```
#### Installing Oracle Instant Client
Installing the Oracle Instant client takes a few more steps on Mac than it does on Linux. Simply vist 

https://www.oracle.com/technetwork/database/database-technologies/instant-client/downloads/index.html

Select **Instant Client for Mac OS X (Intel x86) (32-bit and 64-bit)** and on the next page select the **Version 18.1.0.0.0 (64-bit) Basic Package**. When it's downloaded simply unzip it into your home directory.

#### Installing Jupyter-Lab
In the JupyterLabWork directory that was created when we ran the git clone command there's a file called ```requirments.txt```. This is a list of modules needed to run the notebooks in that directory. To install them all you need to do is to run the command
```
pip install -r requirements.txt
```
**NOTE :** You don't need to use pip3 when you have your virtual environment activated.

This will install all of the needed modules. From there all we need to do is to run the command
```
jupyter-lab
```
This should take you directly into a browser and the the jupyter environment.

![jupter lab image](http://www.dominicgiles.com/misc/jupyterlab_mac.png)

That's it.
