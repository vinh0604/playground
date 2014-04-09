## Getting Started

Alright, let's get started. This workshop assumes that you're familiar with some basic Linux commands. In order to provide a consistent environment for each participant, we're using Vagrant and VirtualBox. In case you haven't installed these, we can do this now.

### Install VirtualBox

VirtualBox is available for Linux, Mac OSX and Windows. You can download it [here](https://www.virtualbox.org/wiki/Downloads) or ask the organizer for a copy.

Please follow the installation instructions according to your operating system.

### Install Vagrant

Vagrant is available for Linux, Mac OSX and Windows. You can download it [here](http://www.vagrantup.com/downloads.html) or ask the organizer for a copy.

Please follow the installation instructions according to your operating system.

### Setup a Vagrant instance with Docker

Get your copy of the Vagrant box named ```saucy-docker``` from the organizer. Change the path in your ```Vagrantfile``` accordingly.

Your Vagrantfile should similar to this:

```ruby
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # ...

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url = "/tmp/saucy-docker.box"

  # ...
end
```

This box contains the most recent version of ```Docker``` and is pre-configured. To start a new VM with this box, just type ```vagrant up``` in your shell.

It'll ask for your password at some point, as it has to configure a shared folder with your host system. Once this command has finished, a simple ```vagrant ssh``` will get you access to your brand new VM.

### Welcome aboard!

You made it! Let's give it a try. Assuming that you're on the VM, let's check the version of Docker.

```bash
docker version
Client version: 0.9.1
Go version (client): go1.2.1
Git commit (client): 3600720
Server version: 0.9.1
Git commit (server): 3600720
Go version (server): go1.2.1
```

Cool, let's do some actual Docker things :)
