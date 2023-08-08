# Snip tips


<!--more-->
# Some snip tips

## PostgreSQL
- Get all running query
  ```sql
    SELECT pid, state, query, age(clock_timestamp(), query_start) AS query_age, psa.*
    FROM pg_stat_activity psa
  ```
- Miscellaneous
  ```bash
    pg_lsclusters
    sudo pg_dropcluster 14 main --stop
    sudo pg_upgradecluster 12 main    
  ```

## Sqlite3
- Install sqlite3-console ubuntu: `sudo apt install sqlite3`
- Connect to db file: `sqlite3 path/to/db/file`

## Laravel
- Encrypt / Decrypt message with Laravel 10
  ```php
  use Illuminate\Support\Facades\Crypt;
  $encrypted = Crypt::encrypt('My secret message');
  $decrypted = Crypt::decrypt($encrypted);
  // -- OR --
  $encrypted = Crypt::encrypt('My secret message', 'secret_key');
  $decrypted = Crypt::decrypt($encrypted, 'secret_key');
  ```
  - config('app.cipher') is encrypt / decrypt algorithm
  - config('app.key') is default secret_key

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
  `
    --endpoint-url
    --no-verify-ssl
    --no-paginate
    --output : json / text / table
    --profile : 
    --color : on / off / auto
    --cli-read-timeout
    --cli-connect-timeout

  `

## Ubuntu
- Show OS version-information
  ```bash
    lsb_release -a
  ```

## Openbox
- Openbox configuration-file: `~/.config/openbox/rc.xml`
- Reload configuration-file (after edit): `openbox --reconfigure`

