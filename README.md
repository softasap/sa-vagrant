sa-vagrant
==========

[![Build Status](https://travis-ci.org/softasap/sa-vagrant.svg?branch=master)](https://travis-ci.org/softasap/sa-vagrant)


Installs basic vagrant setup with necessary plugins



Example of use:

<pre>

     - {
         role: "sa-vagrant",
         vagrant_version: 1.8.1,

         vagrant_plugins:
           - vagrant-vbguest
           - vagrant-hostsupdater
           - vagrant-auto_network
       }

</pre>


There are tons of vagrant plugins. Some of them are quite handy.
Usually I am using three plugins with vagrant:

- vagrant-vbguest: Synhronizes guest additions versions inside image  with the master Oracle VirtualBox version. This helps to prevent random issues with shared folders.
- vagrant-hostsupdater: Automatically updates host files with side dev aliases used. Important: this plugin will ask you for privileged access to write into /etc/hosts.  
- vagrant-auto_network: This plugin registers an internal address range and assigns unique IP addresses for each successive request so that network configuration is entirely hands off. It's much lighter than running a DNS server and masks the underlying work of manually assigning addresses.

With plugins above, my Vagrantfile usually contains: aliases for dev websites to be added to /etc/hosts + I prefer all Vagrant boxes to have the same IP address subnetwork.
<pre>
config.vm.hostname = "www.local.dev"
config.hostsupdater.aliases = ["alias.local.dev", "alias2.local.dev"]
config.vm.network :private_network, :auto_network => true

# My favorite:  to stick to 33.* subnetwork
AutoNetwork.default_pool = '192.168.33.0/24'
</pre>

Vagrant in action:

https://github.com/Voronenko/lamp-box/
