# home-assistant
My Home Assistant installation is modelled after this [very clear guide](https://iotechonline.com/home-assistant-install-with-docker-compose/) from Jere's website iotechonline.com.  
The beauty of setting up Home Assistant with `docker-compose` is that instead of remembering my configuration details, they are all just stored here in this repository as code (configuration as code)  

In this repository, I have layed out the barebones skeleton for a docker-compose setup of Home Assistant.  To get started, navigate to the directory where you want it and clone my repo with the command `git clone https://github.com/kklitzing/home-assistant`  
I've included sample [`.env`](.env.sample) (which holds your environmental variables for `docker-compose`) and [`secrets.yaml`](hass-config/secrets.yaml.sample) files.  
Edit or replace them, making sure to remove the suffix `.sample` and continue to follow [the steps](https://iotechonline.com/home-assistant-install-with-docker-compose/).  

I've added a `.gitignore` file to make sure no secrets are uploaded if you decide to backup/share your Home Assistant configuration to GitHub in the future.
When you back up your setup, make sure that you back up your secrets someplace safe as well!

## FAQ's
### What is the point of this repo?
The docker-compose setup scheme for Home Assistant assumes that you have this skeleton laid out on your system.  Rather than recreate it from scratch in the future, I instead created it within a GitHub repository, so that replicating my setup in the future will be that much easier.
### What are these `.keep` files?
[`git` tracks content, not directories.](https://markmail.org/message/4eqjxx73opiswfis)  To adapt to this, I have included empty files `.keep` to the leaf nodes of the (otherwise) empty directories.
