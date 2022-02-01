# home-assistant
In this repository, I have layed out the barebones 'skeleton' for a docker-compose setup of Home Assistant. My Home Assistant installation is modelled after this [very clear guide](https://iotechonline.com/home-assistant-install-with-docker-compose/) from Jere's website iotechonline.com.  
This guide will get you all the way to the Home Assistant onboarding script.  

The beauty of setting up Home Assistant with `docker-compose` is that it simplifies the installing, troubleshooting, and sharing of your setup because the bulk of the details are already baked in to `docker-compose.yaml` which builds the server environment.  Rather than having to remember or document a slew of `apt-get` commands and multiple manual file changes, by using `docker-compose`, you store much of the installation procedures and configuration as code.

The reddit user luna87 [put it well](https://www.reddit.com/r/homeassistant/comments/c3p3ek/comment/ersd9kv/?utm_source=share&utm_medium=web2x&context=3):
>I would also recommend using docker-compose and git for version control... ...you can easily define your entire container stack as a single service and bring everything up / down / restart together with docker compose.
>
>You can then use Git to version control all of it. If I ever needed to move my home assistant install, all I would need to do is install docker, docker compose and git. Git clone my Git repository and docker-compose start. <br/>  
# &nbsp; &nbsp; :ok_hand:
# Pre-requisites
[Excellent, concise guide for Raspberry Pi `docker` and `docker-compose`](https://jfrog.com/connect/post/install-docker-compose-on-raspberry-pi/)
* [install docker](https://docs.docker.com/engine/install/)
  `curl -fsSL https://get.docker.com -o get-docker.sh`
  `sudo sh get-docker.sh`: execute the install script with root priviledges
  `sudo usermod -aG docker ${USER}`: add your user to the group Docker
  `groups ${USER}`: Check that your user was successfully added
* [Install `docker-compose`](https://docs.docker.com/compose/install/):
  `sudo apt install docker-compose`
  


## How to use it <br/>  Three steps
- [ ] Copy project folder
- [ ] modify `.env.sample` and `secrets.yaml.sample`
- [ ] execute docker-compose  

### Copy project  
To get started, navigate to where you want to locate your Home Assistant folder.  
`cd ~` (I prefer it to be in my user's home directory)  

Then, bring this repo folder and it's contents to your computer:  
`git clone https://github.com/kklitzing/home-assistant`  
If you don't have git installed, fret not.  On this page, simply click on the green box that says Code and select `Download ZIP`.  Extract the ZIP archive into the desired directory.

- [x] Copy project folder
- [ ] modify `.env.sample` and `secrets.yaml.sample`
- [ ] execute docker-compose  



### Modify environmental variables  
If this is your first time with HA, you have to edit (or replace) just two files: [`.env`](.env.sample) and [`secrets.yaml`](hass-config/secrets.yaml.sample)  
If you are restoring your existing HA setup, then additionally make sure to combine the lines from this repo's [`configuration.yaml`](hass-config/configuration.yaml) and `secrets.yaml` when restoring your own.  

- The `.env` file holds variables that the `docker-compose` command will refer to when it builds the containers.  
  First open the `.env` file within the base directory with your choice of text editor
  `cd home-assistant`
  `nano .env.sample`
  The default PUID and PGID should suitable, but change the passwords to something unique:
  ```
  MYSQL_ROOT_PASSWORD=mariadbrootpassword
  HA_MYSQL_PASSWORD=ha_dbdatabasepassword
  ```
  Change the root (mariadbrootpassword) and HA_sql passwordssword"mariadbrootpassword"
  ```
  PUID=1000
  PGID=1000
  ```
   
  After editing the pertinent fields, using **Ctrl-O** will give you the option to save with a different filename.  Save and exit without the suffix `.sample`
  
  >If you happened to save and close the files without renaming, you can rename them with the command `mv`, i.e.:  
  `mv .env.sample .env` and `mv ~/ha-config/secrets.yaml.sample ~/ha-config/secrets.yaml.sample`  
  
- The [`secrets.yaml`](/hass-config/secrets.yaml.sample) file is used by Home Assistant looks in the `secrets.yaml` whenever it sees a `!secret` reference in the configuration.yaml file that you don't want to hold in `configuration.yaml`.
  by Home Assistant to store secrets needed for setup/interaction with the other software containers.
  These values could just be kept within the configuration.yaml file, because you can then safely share your config file with others while troubleshooting.
  `nano hass-config/secrets.yaml`  

  ```
  hostip: "<hostip>" # substitute your pi's LAN IP address  e.g., hostip: 192.168.0.31 
  configurator_url: "http://<hostip>:3218/" 
  nodered_url: "http://<hostip>:1880/"
  
  ha_db_url: "mysql://homeassistant:<ha_dbdatabasepassword>@<hostip>/ha_db?charset=utf8"
  ```
  `<hostip>`: Is your hosts IP address on the network.
    
  *You will have to make sure to otherwise remove the suffix `.sample` from these filenames*
- [x] Copy project folder
- [x] modify `.env.sample` and `secrets.yaml.sample`
- [ ] execute docker-compose  
  
### `docker-compose`
[The guide I followed for the installation of Docker](https://phoenixnap.com/kb/docker-on-raspberry-pi) suggests adding Your user to the Docker group so that containers can be run without requiring root priveleges, which is generally considered [best practice](https://en.wikipedia.org/wiki/Principle_of_least_privilege).
  
If your regular user does not yet already have permissions for docker, then go ahead and enter the command:  
`sudo usermod -aG docker [user_name]` (In Raspberry Pi OS, the default user is 'pi' so `sudo usermod -aG docker pi`)  
  
  *\*You must restart the user session (i.e., log out and back in) for this change to take effect.*

 When you're ready to build your containers, navigate to the installation directory: `cd ~/home-assistant`
  then:  
`docker-compose up -d`

> Depending on your Linux distribution, [some of these applications may already be installed on the host system](https://iotechonline.com/home-assistant-install-with-docker-compose/?cn-reloaded=1#comment-346). To avoid conflicts, you will have to uninstall them first (e.g., `sudo apt-get remove mosquitto`)
- [x] Copy project folder
- [x] modify `.env.sample` and `secrets.yaml.sample`
- [x] execute docker-compose  
## All done! :tada:
If you open a web browser on the pi (or other computer on the LAN) you should now (or shortly) be able to navigate into the Home Assistant webserver at 'http://<hostip>:8123’
to start onboarding.
  
  
  
## FAQ's

### What is git? GitHub?
  Git is a command-line tool, used by programmers to share/submit their code changes to a version controlled repository, so that when a bug crops up, or a software team decides to tackle a problem via a different route, the 5 W's (who, what, when, where, and why) that surround the code base are readily observable, because each change has been documented.  Github, as the name evokes, sprung up around that, and besides providing a easy, web-accessible UI, it aids collaborative development build by serving as ahas many tools and integrations useful for testing and building software.  With all these various tools, it turns out that GitHub can be useful for than just code, it's a platform used for [curated lists](https://github.com/folkswhocode/awesome-diversity), demos of [code snippets](https://gist.github.com/jbsulli/03df3cdce94ee97937ebda0ffef28287), sharing Animal Crossing: New Horizonds infographics, and even [hosting websites](www.kyleklitzing.com).
### What's the point of this repo? <br/> Why don't I just follow [the guide at iotechonline.com](https://iotechonline.com/home-assistant-install-with-docker-compose/)?
  You can! I created this repo for a few reasons:
  * to make it easier for others to setup a Home Assistant, Nodered, MQTT, SQL server!
  * so that replicating my setup in the future will be that much easier.  The docker-compose setup scheme for Home Assistant from Jere's guide assumes that you have this skeleton created on your system.  Rather than recreate it from scratch in the future, I instead created it within a GitHub repository.
  * to learn (the best way for one to learn is to teach)
### Isn't it dangerous to publicly share your configuration?
  Particularly with a public repository, you must make sure that no secrets are uploaded when the backing up the Home Assistant configuration to GitHub.  This would tantamount to posting one's passwords in a public forum.  To prevent this, I've added a `.gitignore` file to ensure that the sensitive files used in production (`.env` and `secrets.yaml`) **are _not_** uploaded to a git repository.  This means that you still need to find a safe place to backup your secrets file, even if in the future, like me, you decide to backup/share your Home Assistant configuration to GitHub.  
*  **When you back up your setup, make sure to securely back up your secrets and passwords as well!**
  
### I've already dabbled with HA in Docker, do I need to do anything?  
  You will need to first [stop and remove all docker containers and images](blog.baudson.de/blog/stop-and-remove-all-docker-containers-and-images)

  To stop all containers, you can execute the command:  
`docker stop $(docker ps -aq)`  
  Before removing the containers in the next step, I would advise you to **backup** the folder containing your existing Home Assistant config, if you intend to use it again.  After you've backed up any save stores and you're ready for a clean slate, simply type  
`docker rm $(docker ps -aq)`  
>If your previous efforts with Docker are still plaguing you, there is a nuclear option: `docker system prune --all --volumes`  
>Make sure your `/hass-config/` folder is backed up first, **everything** will be wiped from the docker volumes/directories.


### What are these `.keep` files?
Because [`git` tracks content, not directories.](https://markmail.org/message/4eqjxx73opiswfis), I have included empty files named `.keep` to the leaf nodes of the (otherwise) empty directories, so that the structure is preserved within the git repository.  Contrary to the name, they don't have to be kept, and can safely be either ignored or deleted.

### How does one ensure they have write permissions?
  Within a directory, type `ls –l [file_name]` (without the brackets)



### What's a good way of doing backups?
I've modelled my backup script after that which user mwav3 [posted to the Home Assistant community forum](https://community.home-assistant.io/t/what-backup-strategy-when-running-home-assistant-in-docker/262539/10):  

Many of these important files start with `.` and are often hidden by default in Windows, macOS, and Linux.  When you backup the folders, make sure that you are viewing all files before selection and copying.

I make use of rsync, I first make sure the directories exist
`mkdir ~/backups/hassrsync -p`  
and make sure that my user:defaultgroup has full permissions to the hass-config folder
(rsync had issues with hidden folders like `.store`, sync seemed to have permission issues without first recursively changing ownership of the directory and files within)  
    `sudo chown -R pi: home/pi/<directory-being-backed-up>`  

  The actual backup routine looks much like below:
  ```
  sudo chown -R pi: ~/home-assistant
  rsync -ab --backup-dir=old_`date +%F` --delete --exclude=old_* /home/pi/home-assistant /media/pi/thumbdrive-backup/hassrsync
  ```
