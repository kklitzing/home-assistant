# home-assistant
My Home Assistant installation is modelled after this [very clear guide](https://iotechonline.com/home-assistant-install-with-docker-compose/) from Jere's website iotechonline.com.
The beauty of setting up Home Assistant with `docker compose` is that instead of remembering my configuration details, they are all just stored here in this repository as code (configuration as code)
I layed out the barebones skeleton in this repo: you can (I have) clone the repo within the directory where you want it with the command `git clone https://github.com/kklitzing/home-assistant` 
then edit (or replace)  `.env` and the `secrets` files and just [follow the steps](https://iotechonline.com/home-assistant-install-with-docker-compose/).  
I've added a `.gitignore` file to make sure no secrets are uploaded if you decide to backup/share your Home Assistant configuration to GitHub in the future.

## FAQ's
### What is the point of this repo?
The docker-compose setup scheme for Home Assistant assumes that you have this skeleton laid out on your system.  Rather than recreate it from scratch in the future, I created it here instead, so replicating my setup should be that much easier.
### What are these `.keep` files?
[`git` tracks content, not directories.](https://markmail.org/message/4eqjxx73opiswfis)  To adapt to this, I have included empty files `.keep` to the leaf nodes of the (otherwise) empty directories.
