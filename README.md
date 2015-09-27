Scotch Bedrock
==============
We use this as a boilerplate to get new development projects up and running in seconds.

This is a Vagrant setup with:
* [ScotchBox](http://box.scotch.io)
* [Roots Bedrock](https://roots.io/bedrock/)
* Some simple provision script setup in the Vagrantfile

The reason for this repo is to get a lighter setup than with [Trellis](https://roots.io/trellis/).

### Step 1
Download, fork or clone this repo to your local machine, eg 
```
git clone https://github.com/ekandreas/scotch-bedrock thenewproject 
```
### Step 2
Change settings in the two lines of Vagrantfile. eg, 
```
    hostname = "thenewproject"
    ip = "192.168.33.111"
```
### Step 3
Run Vagrant! 
```
vagrant up
```
### Step 4
Ignore the red lines of install messages and missing sendmail!

### Step 5
Browse to your hostname.dev, eg 
```
http://thenewproject.dev
```
### Step 6
Log in to WordPress with username *admin* and password *admin* at /wp/wp-admin, eg 
```
http://thenewproject.dev/wp/wp-admin
admin / admin
```
