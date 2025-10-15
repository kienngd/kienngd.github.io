# WordPress Command Line Interface a quick guide


## Supercharge Your Local WordPress: A Quick Guide to WP-CLI 💻

WP-CLI (WordPress Command Line Interface) is a powerful tool that lets you manage your WordPress site directly from your terminal. It's much faster than clicking through the admin dashboard\! Here’s how to get it set up and start using it on your local machine.
<!--more-->
-----

## 1\. Get the WP-CLI File

First, you need the WP-CLI executable file. We'll use `curl` to download it.

```bash
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
```

This command downloads the file and saves it as `wp-cli.phar` in your current directory.

-----

## 2\. Set Permissions

The file you downloaded needs to be executable. Use the `chmod` command to give it the right permissions.

```bash
chmod +x wp-cli.phar
```

The `+x` option makes the file executable.

-----

## 3\. How to Run Commands

To use WP-CLI, you’ll typically run it by typing `./wp-cli.phar` followed by the command, like this:

```bash
./wp-cli.phar core download
```

### 💡 Pro Tip: Make it Easier\!

For a better experience, you can rename the file to just `wp` and move it to a folder in your system's PATH (like `/usr/local/bin`). This lets you run commands simply as `wp` instead of `./wp-cli.phar`.

1.  **Rename and Move:**
    ```bash
    sudo mv wp-cli.phar /usr/local/bin/wp
    ```
2.  **Test:** Now, you can run:
    ```bash
    wp --info
    ```
    If you see the WP-CLI version info, you're all set\!

-----

## 4\. Basic and Useful Commands

Once inside your local WordPress project's root folder, you can run these commands.

| Command | What it Does | Example |
| :--- | :--- | :--- |
| `core download` | Downloads the latest WordPress core files. | `wp core download` |
| `config create` | Creates the `wp-config.php` file. | `wp config create --dbname=local_db --dbuser=root` |
| `core install` | Runs the installation process (like going to `/wp-admin/install.php`). | `wp core install --url=local.test --title="My Site" --admin_user=admin --admin_password=secret --admin_email=a@b.com` |
| `plugin install` | Installs a plugin from the WordPress repository. | `wp plugin install contact-form-7 --activate` |
| `plugin update` | Updates all or specific plugins. | `wp plugin update --all` |
| `db export` | Exports your database to an SQL file. | `wp db export backup.sql` |
| `cache flush` | Clears WordPress and object caches. Essential after major changes. | `wp cache flush` |

use `wp --help` to see all available commands and `wp help <command>` to get more information on a specific command..

Start using WP-CLI today and see how much faster your local development becomes\! Happy coding\!
