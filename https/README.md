# https

This is an example of a gitea + drone installation using self signed https certificates.

You need to place a `ca-certificates.crt` file that contains the self signed root ca and 
all other relevant CA's within this folder. You can pick a default `ca-certificates.crt`
and add your certificate at the top or bottom of this file.

I use dnsmasq and nginx on a separate Raspberry Pi to handle the subdomains.


### Using self signed certificates during build
```yml
kind: pipeline
name: default

clone:
  disable: true

steps:
- name: custom_clone
  image: plugins/git
  settings:
    depth: 10
    skip_verify: true

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