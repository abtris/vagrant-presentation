theme: Merriweather, 8

# Vagrant

## [www.vagrantup.com](https://www.vagrantup.com/)

---

## Install Virtualbox + Vagrant

- [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)
  - [guest additions](https://docs.oracle.com/cd/E36500_01/E36502/html/qs-guest-additions.html)

- [https://www.vagrantup.com/downloads.html](https://www.vagrantup.com/downloads.html)

---

# Mac

```
brew install Caskroom/cask/virtualbox
brew install Caskroom/cask/virtualbox-extension-pack
brew install Caskroom/cask/vagrant
```

---

## Default image from Vagrant docs

```
$ vagrant init hashicorp/precise64
$ vagrant up
```

---

```
$ vagrant ssh
Welcome to Ubuntu 12.04 LTS (GNU/Linux 3.2.0-23-generic x86_64)

 * Documentation:  https://help.ubuntu.com/
New release '14.04.5 LTS' available.
Run 'do-release-upgrade' to upgrade to it.

Welcome to your Vagrant-built virtual machine.
```

---

# Atlas - discovery boxes

## [https://atlas.hashicorp.com/boxes/search](https://atlas.hashicorp.com/boxes/search)

---

## Remove old Vagrant instance and file

```
$ vagrant destroy
$ rm Vagrantfile
```

---

## Use ubuntu office image for 16.04 LTS

```
$ vagrant init ubuntu/xenial64
$ vagrant up
```

---

```
$ vagrant ssh
Welcome to Ubuntu 16.04.1 LTS (GNU/Linux 4.4.0-62-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.
```

---

```
$ vagrant status
Current machine states:

default                   running (virtualbox)

The VM is running. To stop this VM, you can run `vagrant halt` to
shut it down forcefully, or you can run `vagrant suspend` to simply
suspend the virtual machine. In either case, to restart it again,
simply run `vagrant up`.
```

---

```
$ vagrant help
Usage: vagrant [options] <command> [<args>]

    -v, --version                    Print the version and exit.
    -h, --help                       Print this help.

Common commands:
     box             manages boxes: installation, removal, etc.
     destroy         stops and deletes all traces of the vagrant machine
     global-status   outputs status Vagrant environments for this user
     halt            stops the vagrant machine
     help            shows the help for a subcommand
     init            initializes a new Vagrant environment by creating a Vagrantfile
     login           log in to HashiCorp's Atlas
     package         packages a running vagrant environment into a box
     plugin          manages plugins: install, uninstall, update, etc.
     port            displays information about guest port mappings
     powershell      connects to machine via powershell remoting
     provision       provisions the vagrant machine
     push            deploys code in this environment to a configured destination
     rdp             connects to machine via RDP
     reload          restarts vagrant machine, loads new Vagrantfile configuration
     resume          resume a suspended vagrant machine
     snapshot        manages snapshots: saving, restoring, etc.
     ssh             connects to machine via SSH
     ssh-config      outputs OpenSSH valid configuration to connect to the machine
     status          outputs status of the vagrant machine
     suspend         suspends the machine
     up              starts and provisions the vagrant environment
     version         prints current and latest Vagrant version

For help on any individual command run `vagrant COMMAND -h`

Additional subcommands are available, but are either more advanced
or not commonly used. To see all subcommands, run the command
`vagrant list-commands`.
```

---

# Synced folders

```
$ vagrant up
...
$ vagrant ssh
...
ubuntu@ubuntu-xenial:~$ ls /vagrant
README.md  ubuntu-xenial-16.04-cloudimg-console.log  Vagrantfile
```

---

```
ubuntu@ubuntu-xenial:~$ touch /vagrant/foo
ubuntu@ubuntu-xenial:~$ exit
$ ls
README.md  Vagrantfile foo ubuntu-xenial-16.04-cloudimg-console.log
```

---

# Provisioning

---

## Vagrantfile

```
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y mc
  SHELL
end
```

---

```
$ vagrant provision
```

or

```
$ vagrant destroy
$ vagrant up
```

---

# Vagrant providers

- VirtualBox
- VMware
- Docker
- Hyper-V


---

# Vagrant provision

- File
- Shell
- Ansible
- CFEngine
- Chef
- Puppet
- Docker
- Salt

---

# Vagrant Networking

- Forwarded Ports
- Private Networks
- Public Networks

---

# Vagrant Multi-machine

```
Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: "echo Hello"

  config.vm.define "web" do |web|
    web.vm.box = "apache"
  end

  config.vm.define "db" do |db|
    db.vm.box = "mysql"
  end
end
```

---

# Vagrant plugins

- [Core](https://github.com/mitchellh/vagrant/tree/master/plugins)
- [Wiki](https://github.com/mitchellh/vagrant/wiki/Available-Vagrant-Plugins)
	- [vagrant-cachier](http://fgrehm.viewdocs.io/vagrant-cachier/) - currently unmaintained

---

# Packer

## [www.packer.io](https://www.packer.io/)

- Packer is a tool for creating machine and container images for multiple platforms from a single source configuration.

---

# Veewee

## [github.com/jedi4ever/veewee](https://github.com/jedi4ever/veewee)

- Easing the building of vagrant boxes
