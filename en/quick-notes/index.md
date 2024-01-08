# Quick-notes


<!--more-->
# Some Quick-notes

## Sqlite3
- Install sqlite3-console ubuntu: `sudo apt install sqlite3`
- Connect to db file: `sqlite3 path/to/db/file`

## Install awscli
  ```bash
    sudo apt update
    sudo apt install awscli
    aws --version
    aws configure
    aws configure [--profile profile-name]
    aws configure set region us-west-2 --profile profile1
    aws configure list
    aws help
    aws s3 help
    aws s3 rm help
    aws --endpoint-url=https://s3south.storage.com.vn --profile citigo1 s3 ls
    aws --endpoint-url=https://s3south.storage.com.vn --profile citigo1 s3 rm --recursive s3://kiotviet-export
    aws --endpoint-url=https://s3south.storage.com.vn --profile citigo2 s3 rm --recursive s3://kiotvietimages
  ```
  **aws params**
  ```
    --endpoint-url
    --no-verify-ssl
    --no-paginate
    --output : json / text / table
    --profile : 
    --color : on / off / auto
    --cli-read-timeout
    --cli-connect-timeout

  ```

## Ubuntu
- Show OS version-information
  ```bash
    lsb_release -a
  ```
- Add self-signed CA
  - copy file rootCA.crt to `/usr/local/share/ca-certificates`
  - Update: `sudo update-ca-certificates`  
  - Convert pem to crt in **der-format** `openssl x509 -outform der -in yourfile.pem -out yourfile.crt`
  - Convert perm to crt in **ASCII-PEM-format** just rename.
- ....

## Openbox
- Openbox configuration-file: `~/.config/openbox/rc.xml`
- Reload configuration-file (after edit): `openbox --reconfigure`

## Linux commands
- List folder, short desc by size: du -sh database/backup/* | sort -hr

## GIT commands
- Update branches-list (and other information): `git fetch --prune origin`
- Delete remote branches: `git push origin --delete branch_1 branch_2` or `git push origin :branch_1 :branch_2`
- List all remote branches: `git branch -r`

## docker-compose
### Install docker-compose version 2 (and still using docker-compose version 1 too)
- Document link: https://github.com/docker/compose
- Download file from release page: https://github.com/docker/compose/releases 
- Copy file to `~/.docker/cli-plugins/`, rename to `docker-compose`, set excute permission `chmod u+x docker-compose`
- Run `~/.docker/cli-plugins/docker-compose version` to check if it is new version

## Tilix - shortcut keys
- How to install tilix?
- Shortcut-Keys
  - CTRL + ALT + T: New session
  - CTRL + PageDown / PageUp: Move to next / previous session
  - CTRL + ALT + R / D / A: New window right / down / auto
  - Super + ALT + Arrow: Change window size
  - CTRL + TAB: change window
- ...
