#vagrant-chef-lamp

Sets up a LAMP dev box running `ubuntu/trusty64` in provider lxc or virtualbox.

- LAMP packages installed:
	- apache2
	- mysql-server
	- php5
	- php5-cli
	- php5-dev
	- php5-mysql
	- php-pear
  - xdebug
- Other miscellaneous packages installed:
	- vim
- Default Apache site enabled
- Apache modules enabled
	- mod_rewrite
	- mod_alias
- MySQL can be accessed from the host machine
	- **host:** localhost
	- **user:** root
	- **password:** root
- Xdebug installed and setup to allow remote debugging

##Usage

Clone git repository and update modules:

```
git clone https://github.com/noobli/vagrant-chef-lamp
git submodule init
git submodule update
```

Setup and provision the box:

```
vagrant up
```

##Crédits

- Jhony Alceu Pereira

Based in project: https://github.com/mike182uk/lamp-vagrant-chef-solo