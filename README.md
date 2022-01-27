# home-assistant

My Home Assistant installation is modelled after this [very clear guide](https://iotechonline.com/home-assistant-install-with-docker-compose/) from Jere's website iotechonline.com.  
The beauty of setting up Home Assistant with `docker-compose` is that it simplifies the installing, troubleshooting, and sharing of your setup because the bulk of the details are already baked in to `docker-compose.yaml` which builds the server environment.  Rather than having to remember or document a slew of `apt-get` and multiple manual file changes, by using `docker-compose`, you store much of the installation procedures and configuration as code.

## How to use it
In this repository, I have layed out the barebones 'skeleton' for a docker-compose setup of Home Assistant.  
To get started, navigate to the directory where you want to locate your Home Assistant folder and clone this repo with the command:  
`git clone https://github.com/kklitzing/home-assistant`  
As long as there isn't already a folder with this name, this will create the project in a folder called `/home-assistant/`
Next, we have to necessarily customize the setup to you and your installation specifics (things like <hostip>, uid and gid, passwords, etc.).
This consists of having to edit (or replace) just two files: [`.env`](.env.sample) and [`secrets.yaml`](hass-config/secrets.yaml.sample)  

You will have to make sure to remove the suffix `.sample` from these filenames as you follow [the guide](https://iotechonline.com/home-assistant-install-with-docker-compose/)

  
## FAQ's
### What's the point of this repo? <br/> Why don't I just follow [the guide at iotechonline.com](https://iotechonline.com/home-assistant-install-with-docker-compose/)?
  You can! I created this repo for two reasons:
  * to make it easier for others to setup a Home Assistant, Nodered, MQTT, SQL server!
  * to learn (the best way for one to learn is to teach)
The docker-compose setup scheme for Home Assistant from Jere's guide assumes that you have this skeleton created on your system.  Rather than recreate it from scratch in the future, I instead created it within a GitHub repository, so that replicating my setup in the future will be that much easier.
### Isn't it dangerous to publicly share your configuration?
  Particularly with a public repository, you must make sure that no secrets are uploaded when the backing up the Home Assistant configuration to GitHub.  This would tantamount to posting one's passwords in a public forum.  To prevent this, I've added a `.gitignore` file to ensure that the sensitive production files (`.env` and `secrets.yaml`) **are _not_** uploaded to a git repository.  This means that you still need to find a safe place to backup your secrets file, even if in the future, like me, you decide to backup/share your Home Assistant configuration to GitHub.  
*  **When you back up your setup, make sure to securely back up your secrets and passwords as well!**
### What are these `.keep` files?
[`git` tracks content, not directories.](https://markmail.org/message/4eqjxx73opiswfis)  To adapt to this, I have included empty files `.keep` to the leaf nodes of the (otherwise) empty directories.  They can safely be ignored/deleted.
