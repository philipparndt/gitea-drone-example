# Gitea with Drone.io example

This is a working example of gitea with drone on a Synology NAS.

### Tested versions:

- gitea/gitea version: 1.9.5 
- drone/drone version: 1.6.0
- drone/agent version: 1.6.0 

### Folders on NAS:

- `/volume1/docker/gitea`
- `/volume1/docker/drone`

### http or https

you can find two examples for both in the subfolders `http` and `https`

### Installation process

- create folders
- update TODO configuration variables in the `docker-compose.yml` file
  you can disable `DRONE_GITEA_CLIENT_ID` and `DRONE_GITEA_CLIENT_SECRET` for the moment
- `docker-compose up`
- launch gitea page `http://<TODO IP-OF-THE-NAS>:3000`
- install using SQlite (make sure to update/insert the correct server locations)
- create a initial gitea user, this will be the admin
- create a new oauth application this will give you the missing config parameters
  for `DRONE_GITEA_CLIENT_ID` and `DRONE_GITEA_CLIENT_SECRET`
- stop the docker containers
- update the `docker-compose.yml` file
- `docker-compose up -d`
- browse to drone `http://<TODO IP-OF-THE-NAS>:3001`

### Bonus

Example for a `.drone.yml` that executes a remote shell script:

```yml
kind: pipeline
name: default
steps:
- name: ssh
  image: appleboy/drone-ssh
  settings:
    host: 192.168.1.1
    username: username
    password: 
      from_secret: ssh_password
    port: 22
    script:
      - /path/to/some/script.sh
      - echo hello
```

Do not forget to register the secret `ssh_password` on the drone server for the project.
