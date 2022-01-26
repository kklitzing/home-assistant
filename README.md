# home-assistant

My Home Assistant installation is modelled after this [very clear guide](https://iotechonline.com/home-assistant-install-with-docker-compose/) from Jere's website iotechonline.com.  
The beauty of setting up Home Assistant with `docker-compose` is that instead of remembering my configuration details, they are all just stored here in this repository as code (configuration as code)  

## How to use it
In this repository, I have layed out the barebones 'skeleton' for a docker-compose setup of Home Assistant.  To get started, navigate to the directory where you want to locate your Home Assistant folder and clone this repo with the command 
>`git clone https://github.com/kklitzing/home-assistant`  

Next, we have to necessarily customize the setup to you and your installation specifics (things like <hostip>, `uid` and `gid`, passwords, etc.).
These include mainly [`configuration.yaml`](hass-config/configuration.yaml) and the [`docker-compose.yaml`](docker-compose.yaml) file.  

  I've included sample files for the [`.env`](.env.sample) and [`secrets.yaml`](hass-config/secrets.yaml.sample) files as well.  
You will have to edit or replace them as you follow [the guide](https://iotechonline.com/home-assistant-install-with-docker-compose/), making sure to remove the suffix `.sample` from these filenames.

I've added a `.gitignore` file to make sure no secrets are uploaded if you decide to backup/share your Home Assistant configuration to GitHub in the future.
When you back up your setup, make sure that you back up your secrets someplace safe as well!

## FAQ's
### What is the point of this repo?
The docker-compose setup scheme for Home Assistant assumes that you have this skeleton laid out on your system.  Rather than recreate it from scratch in the future, I instead created it within a GitHub repository, so that replicating my setup in the future will be that much easier.
### What are these `.keep` files?
[`git` tracks content, not directories.](https://markmail.org/message/4eqjxx73opiswfis)  To adapt to this, I have included empty files `.keep` to the leaf nodes of the (otherwise) empty directories.
