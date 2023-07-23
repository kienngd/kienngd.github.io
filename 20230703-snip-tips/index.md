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

## Ubuntu
- Show OS version-information
  ```bash
    lsb_release -a
  ```

## Openbox
- Openbox configuration-file: `~/.config/openbox/rc.xml`
- Reload configuration-file (after edit): `openbox --reconfigure`

