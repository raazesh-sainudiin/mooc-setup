# mooc-setup

Information for setting up for the Spark MOOC, and lab assignments for the course.

This fork is being adapted for *scalable-data-science-2*, a sequel of courses from Atlantis!


## Set up Spark Cluster in your laptop

### Step 1. Downloading and Installing VirtualBox

Go to the Downloads page linked below for VirtualBox and download the appropriate version for your operating system. 
	* [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads) 

### Step 2. Downloading and Installing Vagrant

Go to the Downloads page for Vagrant linked below and download the appropriate version for your operating system. 
	* [https://www.vagrantup.com/downloads.html](https://www.vagrantup.com/downloads.html)


### Step 3. Downloading and installing the virtual machine for the course

1. Create a custom directory (e.g., for windows users c:\users\marco\myvagrant or for Mac/Linux users /home/marco/myvagrant)
(Please note: 'VAGRANT_HOME' can be set to change the directory where Vagrant stores global state. By default, this is set to '.vagrant.d' under your user profile. This is where boxes (base VMs) are stored, so it can actually be quite large on disk - please make sure you have enough space)

* Download this file [https://github.com/raazesh-sainudiin/mooc-setup/archive/master.zip](https://github.com/raazesh-sainudiin/mooc-setup/archive/master.zip)
to the custom directory and unzip it.

* From the unzipped file, copy Vagrantfile to the custom directory you created in step #1 (NOTE: It must be named exactly "Vagrantfile" with no extension)

* Open a DOS prompt (Windows) or Terminal (Mac/Linux), change to the custom directory, and issue the following command:

```
$ vagrant up --provider=virtualbox
```

NOTE: On Microsoft Windows you may get a Windows Firewall exception popup regarding "vboxheadless".  Adding an exception is optional and does not seem to impact the Virtual Machine once it is installed.

When running "vagrant up" again, you may receive the following error:

bsdtar: Error opening archive: Unrecognized archive format

The solution is to first use the command:

vagrant box remove sparkmooc/base

Then, you can use the "vagrant up" command again.

#### FAQs for Windows

When you type "vagrant up", if you encounter the following error:

* Bringing machine 'sparkvm' up with 'virtualbox' provider...

* There was an error while executing 'VBoxManage', a CLI used by Vagrant for controlling VirtualBox. The command and stderr is shown below.

* Command: ["list", "hostonlyifs"]

* Stderr: VBoxManage.exe: error: Failed to create the VirtualBox object!

* VBoxManage.exe: error: Code E_NOINTERFACE (0x80004002) - No such interface supported (extended info not available)

* VBoxManage.exe: error: Most likely, the VirtualBox COM server is not running or failed to start.

First, make sure you installed VirtualBox using "Run as Administrator". If you did not, then you should follow the directions in the Installing Virtual Box section to uninstall and reinstall VirtualBox. Second, try starting command using "Run as Administrator" (right-click on command and select "Run as Administrtor").

#### FAQs for Linux

On Linux, if you encounter the following error message: 

* SSH:

	* The following settings shouldn't exist: insert_key

* vm:

	* The box 'sparkmooc/base' could not be found.

It means that your Vagrant version is out of date. Remove the vagrant install (apt-get remove). Then you'll want to download the latest version from the vagrant site: [https://www.vagrantup.com/downloads.html](https://www.vagrantup.com/downloads.html). 

Install and re-run using the following commands and it should install correctly.

```
$ sudo dpkg -i vagrant.deb 
$ vagrant up
```

## Step 4. Instructions for using the Virtual Machine

1. To start the VM, from a DOS prompt (Windows) or Terminal (Mac/Linux), issue the command "vagrant up".
2. To stop the VM, from a DOS prompt (Windows) or Terminal (Mac/Linux), issue the command "vagrant halt". Note: You should always stop the VM before you log off, turn off, or reboot your computer.
3. At the end of the course, to erase or delete the VM, from a DOS prompt (Windows) or terminal (Mac/Linux), issue the command "vagrant destroy". Warning: If you erase or delete the VM, you will lose any work you have done and data you have saved, and you will have download it again when you use the "vagrant up" command.
4. Once the VM is running, to access the notebook, open a web browser to "http://localhost:8001/" (on Windows and Mac) or "http://127.0.0.1:8001/" (on Linux).

NOTE: In step #4 above, try "http://localhost:8001/" first, if that doesn't work, try "http://127.0.0.1:8001/", the proper choice depends on the configuration of your computer.  We pre-configuted the virtual machine to by default start the iPython notebook on port 8001.  If you are having problems connecting to the notebook (neither of the two links works), you should check the output of the "vagrant up" command. It may be the case that there was a conflict on your computer with a program already using port 8001 and a higher port number was automatically used. If this occurs, you should use that port number instead of port 8001, and all the rest of the instructions will be the same.

## Step 5. Running Your First Notebook

Running your first notebook will test your software setup and environment.

1. If it is not already running, start the Virtual Machine by issuing issue the command "vagrant up" from a DOS prompt (Windows) or Terminal (Mac/Linux).
2. You should have already downloaded and unzipped the master.zip file in the module "Downloading and installing the virtual machine".  The zip file contains the file "lab0_student.ipynb" that you will need in step #4.  You can view a read-only online version of the Spark iPython notebook here.
3. Once the Virtual Machine is running, access the Jupyter web UI for running IPython notebooks by navigating your web browser to "http://localhost:8001" (or "http://127.0.0.1:8001/").
4. On the Jupyter web page, use the Upload button to upload the "lab0_student.ipynb" Spark iPython notebook file that was mentioned in step #2.
5. Select the file and run each cell - verify that you do not encounter any errors. 
6. At the end of the notebook, instructions are included on how to export the notebook as a Python (.py) file and to submit that file to the autograder.

The following videos walk you through the steps of running your first notebook.

WARNING:
If you encounter an error when running the second test, such as:
```
Py4JJavaError                             Traceback (most recent call last)
<ipython-input-2-5453bfa2d105> in <module>()
      6 
      7 rawData = sc.textFile(fileName)
----> 8 shakespeareCount = rawData.count()
      9 
     10 print shakespeareCount
```
This error is likely due to uploading the lab0 ipynb file into the data directory instead of the home (parent) directory. Try uploading the file into the home directory and running the notebook again.
