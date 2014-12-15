Chef Solo Repository for Chunlea
================================

This repository was what I used in my daily life to bootstrap server for what I need. 

1. Prerequisites
----------------
At first, you need to clone this repository to your machine.
Then, run `bundle install` to install gems used in the repository.
And then, just use `berks install` to install the cookbooks in `Berksfile`.

Add SSH authorized_keys to server if necessary. Thank you Github. :kissing_heart:
> Don't forget to change it to your public keys url instead of mine.  :smile:
```
mkdir .ssh
curl https://github.com/chunlea.keys >> ~/.ssh/authorized_keys;chmod 600 .ssh/authorized_keys
```

2. The Cookbooks I Used
-----------------------

|Cookbook       | Description          
|:-------------:|:--------------
|nginx          | [Nginx Cookbook](https://github.com/opscode-cookbooks/nginx) 

3. How to Use Chef-solo
-----------------------
Do the things we mentioned in [**Prerequisites**](#) first.

### 3.1 Create the node file first
Create the node description in `nodes/porject.domain.name.or.host.name.json`. Use project's domain as the node's file name, and with those content.
```json
{
    "run_list": []
}
```


### 3.1 Prepare a new server with chef
Just run `knife solo prepare username@__ip_addr__ -i _ssh_private_key -p port -N domain.name.or.host.name` to prepare your server. It will install chef-solo on your server.
Or you can use `knife solo bootstrap username@__ip_addr__ -i _ssh_private_key -p port -N domain.name.or.host.name` to bootstrap your server which can **prepare** your server first and then **cook** with the cookbooks in the nodes json file.
We offten use **bootstrap** with a nodes json file to save our time.

### 3.2 Cook your cookbooks on your server
First of all, after **prepare** your server, you need to edit the nodes json file of your server.
Add recipes to the **run_list** and so on.
Then just run `knife solo cook username@__ip_addr__ -i _ssh_private_key -p port -N domain.name.or.host.name`, it will automatically run your cookbooks on your server.

4. How to Add New Cookbook
--------------------------
You can just add cookbooks in `Berksfile` and once you run `knife solo prepare` or `knife solo bootstrap`, the knife-solo will automatically install cookbooks form http://api.berkshelf.com/ or Github via Berkshelf.

**Don't put your own cookbook in *`cookbooks`* folder, Put it in *`site-cookbooks`* instead or add it's own git repo in `Berksfile`.**

5. Links
--------
http://chef.leopard.in.ua