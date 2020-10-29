### lets be jenky

and follow this guide on [youtube](https://www.youtube.com/watch?v=pMO26j2OUME) to set up jenkins in docker

* https://hub.docker.com/r/jenkins/jenkins is the offically maintained repository
* to just start on instance write `docker run -p 8080:8080 -p 50000:50000 -d jenkins/jenkins:lts` in your prefered CLI
  * `-p 8080:8080` -> docker will run on this port
  * `-p 50000:50000` -> Master/Slave Communication via this port

    * *Jenkins initial setup is required. An admin user has been created and a password generated.*
    * Please use the following password to proceed to installation:
    * 422b59acdc5f4c7a9087cb6a26a80731
    *  This may also be found at: /var/jenkins_home/secrets/initialAdminPassword

* `docker ps` -> shows all running docker processes
* `docker stop $(docker ps -aq)` -> stops all running processes
* `-d` -> detached mode
* `-v jenkins_home:/var/jenkins_home` -> bind a named volume right side is name / left side is folder inside the particular image 
  * when binding an already exising volume to docker, consider the jenkins user needs like `chmod -755` so write acess
* we need this to be able to persist a lot of jenkins peripherie, like user, plugin, config, etc

  > so this is the new string with all settings:  `docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts`

* `docker logs <containerId>` and grab your password: ours is above, but just in case
* now use the browser to open the exposed port, for us `localhost:8080`
* use the inital password
* we will install the suggested plugins
  * funny enough `docker log <containerId>` will show us all the download in the background
* we will set admin credentials now

  Key | value
  ----|-------
  User|admin
  pass|admin
  fullname|janpaul
  email|janpauldahlke@gmail.com

#### Types of Jenkins Projects
* we can now select `new Element` || `Element anlegen`, there we will see a lot of the installed plugins, that allow us to chose from a project types


  FreeStyle | Pipeline | Multibranch-Pipeline
  ----------|----------|---------------------
  simple taske, `npm run tests` | the whole delivery cycle, `test`, `build`, for a single branch | like pipeline, for multiple pipelines of the same repo

---

  My Questions:
  * how to ssh into an exisiting and running docker -> https://phoenixnap.com/kb/how-to-ssh-into-docker-container
  * how to delete an image via CLI `docker image rm <containerId> `, it might need `--force`