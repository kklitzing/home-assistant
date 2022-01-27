# home-assistant
In this repository, I have layed out the barebones 'skeleton' for a docker-compose setup of Home Assistant. My Home Assistant installation is modelled after this [very clear guide](https://iotechonline.com/home-assistant-install-with-docker-compose/) from Jere's website iotechonline.com.  

The beauty of setting up Home Assistant with `docker-compose` is that it simplifies the installing, troubleshooting, and sharing of your setup because the bulk of the details are already baked in to `docker-compose.yaml` which builds the server environment.  Rather than having to remember or document a slew of `apt-get` commands and multiple manual file changes, by using `docker-compose`, you store much of the installation procedures and configuration as code.

The reddit user luna87 [put it well](https://www.reddit.com/r/homeassistant/comments/c3p3ek/comment/ersd9kv/?utm_source=share&utm_medium=web2x&context=3):
>I would also recommend using docker-compose and git for version control... ...you can easily define your entire container stack as a single service and bring everything up / down / restart together with docker compose.
>
>You can then use Git to version control all of it. If I ever needed to move my home assistant install, all I would need to do is install docker, docker compose and git. Git clone my Git repository and docker-compose start. <br/>  
# &nbsp; &nbsp; :ok_hand:
## How to use it <br/>  Three steps
- [ ] Copy project folder
- [ ] modify `.env.sample` and `secrets.yaml.sample`
- [ ] execute docker-compose  

### Copy project  
To get started, navigate to where you want to locate your Home Assistant folder.  
`cd ~` (I prefer it to be in my user's home directory)  

Then, bring this repo folder and it's contents to your computer:  
`git clone https://github.com/kklitzing/home-assistant`  
As long as there isn't already a folder with this name, you will now see the root folder for the project `/home-assistant/` within the working directory.  

- [x] Copy project folder
- [ ] modify `.env.sample` and `secrets.yaml.sample`
- [ ] execute docker-compose  
### Modify environmental variables  
Next, we have to necessarily customize the setup to you and your installation specifics (things like <hostip>, uid and gid, passwords, etc.).
This consists of having to edit (or replace) just two files: [`.env`](.env.sample) and [`secrets.yaml`](hass-config/secrets.yaml.sample)  

  I opened the two files using the text editor `nano`:  
`nano .env.sample` and `nano hass-config/secrets.yaml`  
After editing the pertinent fields, using **Ctrl-O** will give you the option to save with a different filename.  Save without the suffix `.sample`
>If you happened to save and close the files without renaming, you can rename it with the commands  
`mv .env.sample .env` and `mv ~/ha-config/secrets.yaml.sample ~/ha-config/secrets.yaml.sample` 
    
*You will have to make sure to otherwise remove the suffix `.sample` from these filenames*
- [x] Copy project folder
- [x] modify `.env.sample` and `secrets.yaml.sample`
- [ ] execute docker-compose  
### `docker-compose`
  When you're ready to build the stack change to the `cd ~/home-assistant`  
`docker-compose up -d` (as root user?), if your regular user does not have permissions for docker then execute  
`sudo usermod -aG docker [user_name]` (In Raspberry Pi OS, the default user is 'pi' so `sudo usermod -aG docker pi`)

> Depending on the distro, [some of these applications may already be installed](https://iotechonline.com/home-assistant-install-with-docker-compose/?cn-reloaded=1#comment-346). To avoid conflicts, you will have to uninstall them first (e.g., `sudo apt-get remove mosquitto`)
- [x] Copy project folder
- [x] modify `.env.sample` and `secrets.yaml.sample`
- [x] execute docker-compose  
## All done!
If you open a web browser on the pi (or other computer on the LAN) you should now (or shortly) be able to navigate into the Home Assistant webserver at 'http://<hostip>:8123’
to finish setup.
  
  ## FAQ's
### What's the point of this repo? <br/> Why don't I just follow [the guide at iotechonline.com](https://iotechonline.com/home-assistant-install-with-docker-compose/)?
  You can! I created this repo for a few reasons:
  * to make it easier for others to setup a Home Assistant, Nodered, MQTT, SQL server!
  * so that replicating my setup in the future will be that much easier.  The docker-compose setup scheme for Home Assistant from Jere's guide assumes that you have this skeleton created on your system.  Rather than recreate it from scratch in the future, I instead created it within a GitHub repository.
  * to learn (the best way for one to learn is to teach)
### Isn't it dangerous to publicly share your configuration?
  Particularly with a public repository, you must make sure that no secrets are uploaded when the backing up the Home Assistant configuration to GitHub.  This would tantamount to posting one's passwords in a public forum.  To prevent this, I've added a `.gitignore` file to ensure that the sensitive production files (`.env` and `secrets.yaml`) **are _not_** uploaded to a git repository.  This means that you still need to find a safe place to backup your secrets file, even if in the future, like me, you decide to backup/share your Home Assistant configuration to GitHub.  
*  **When you back up your setup, make sure to securely back up your secrets and passwords as well!**
### What are these `.keep` files?
[`git` tracks content, not directories.](https://markmail.org/message/4eqjxx73opiswfis)  To adapt to this, I have included empty files `.keep` to the leaf nodes of the (otherwise) empty directories.  They can safely be ignored/deleted.
