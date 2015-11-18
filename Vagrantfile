# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "fgrehm/trusty64-lxc"

  # problem solution for debian-box derived distribution
  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"

  # port forwarding for apache2, mysql and xdebug
  config.vm.network "forwarded_port", guest: 80, host: 80
  config.vm.network "forwarded_port", guest: 3306, host: 3306
  config.vm.network "forwarded_port", guest: 9990, host: 9990

  # Synced folders
  config.vm.synced_folder "./", "/var/www", type: "nfs"

  # change orders to change default provider
  config.vm.provider "lxc" do |lxc|
    lxc.customize 'cgroup.memory.limit_in_bytes', '1024M'
  end

  config.vm.provider "virtualbox" do |vb, override|
    vb.memory = "1024"
    vb.cpus   = 2
    override.vm.box = "ubuntu/trusty64"
  end

  # Provision via chef solo
  config.vm.provision "chef_solo" do |chef|
    chef.add_recipe "apt"
    chef.add_recipe "vim"
    chef.add_recipe "apache2"
    chef.add_recipe "apache2::mod_rewrite"
    chef.add_recipe "apache2::mod_alias"
    chef.add_recipe "apache2::mod_php5"
    chef.add_recipe "base::mysql"
    chef.add_recipe "php"
    chef.add_recipe "php::module_apc"
    chef.add_recipe "php::module_curl"
    chef.add_recipe "php::module_gd"
    chef.add_recipe "php::module_mcrypt"
    chef.add_recipe "php::module_mysql"
    chef.add_recipe "php::apache2"
    chef.add_recipe "base::xdebug"

    chef.json = {
      "apache" => {
        "default_site_enabled" => true
      },
      "php" => {
        "ext_conf_dir" => "/etc/php5/mods-available",
        "ini_settings" => {
          "date.timezone" => "Europe/London"
        }
      },
      "xdebug" => {
        "config_file" => "/etc/php5/mods-available/xdebug.ini",
        "directives" => {
          "remote_autostart" => 1,
          "remote_connect_back" => 1,
          "remote_enable" => 1,
          "remote_log" => "/tmp/xdebug-remote.log"
        }
      }
    }
  end
end