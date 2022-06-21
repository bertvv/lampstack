# Demo/playground server with a LAMP stack

This is a demo/playground machine set up with Vagrant and Ansible. It contains a CentOS VM with a LAMP stack, and Wordpress.

It is useful for showing how Ansible works, or as a test-environment for developing in PHP.

## Dependencies

The setup is OS independent, as long as you have the following tools installed:

* [Git](https://git-scm.com/downloads) (on Windows, also install Git Bash)
* [VirtualBox, including the "Extension pack"](https://www.virtualbox.org/wiki/Downloads/)
* [Vagrant](https://www.vagrantup.com/downloads.html)
* Optionally, [Ansible](http://docs.ansible.com/intro_installation.html) (on [supported platforms](http://docs.ansible.com/intro_installation.html#control-machine-requirements))

## Getting started

Open a Bash shell (Git Bash on Windows), go to a suitable directory to store this project and issue the following commands:

```console
git clone --config core.autocrlf=input https://github.com/bertvv/lampstack
cd lampstack
ansible-galaxy install -r ansible/requirements.yml
```

**Warning** On Windows, it is essential that you include the setting `core.autocrlf=input` when cloning. If you forget, all files will get DOS line endings, and the setup will fail.

Also, on Windows, where you don't have the `ansible-galaxy` command, run this script instead to install the necessary roles:

```console
./scripts/role-deps.sh
```

And finally, start the VM with:

```console
vagrant up
```

The VM will be attached to VirtualBox's [default Host-only network adapter](https://askubuntu.com/questions/198452/no-host-only-adapter-selected) and has a static IP address, 192.168.56.77.

To shut down the VM, execute `vagrant halt`. Start it again with `vagrant up`. If you made a mistake and the VM is broken, do

```ShellSession
vagrant destroy -f
vagrant up
```

## Accessing the virtual machine

* To start using the Wordpress site, surf to <http://192.168.56.84/wordpress/>
* PHP code dropped in the `www/` directory is immediately visible on the website at <http://192.168.56.84/>
* To get shell access via ssh, do
    * `vagrant ssh` (no password)
    * or `ssh vagrant@192.168.56.84` (password `vagrant`)
    * prepend all commands that need root privileges with `sudo` (no password required)
* To access the Cockpit monitoring dashboard, surf to <https://192.168.56.84:9090/> and log in with user name vagrant and password vagrant.