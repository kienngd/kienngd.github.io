# 🚧 How to build a free blog


Hello. In this post we will learn how to build a free personal blog using Hugo + Github page. Have fun!

## Install hugo.

- Download hugo from: https://github.com/gohugoio/hugo/releases
- Install in your PC.
- Check hugo version: `hugo version`

<!--more-->

## Manage your site
**Step 2**: Create a new site.
- Command: 
    ```bash
        hugo new site myblog
    ```
- Then move to folder `myblog`
- Quick start document: https://gohugo.io/getting-started/

**Step 3**: Setup your hugo theme.

- Find a theme from: https://themes.gohugo.io/.
- Download theme and put into site's themes directory. Example we want to use theme Ananke:
    ```bash
        cd myblog
        git init
        git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
    ```
- Inside file `hugo.toml` (or `config.toml` if you use old version).
    ```text
        ...
        theme = "ananke"
        ...
    ```
- Hugo site configuration document: https://gohugo.io/getting-started/configuration/

## Manage your content
- Command to create new post: `hugo new <POST TYPE>/<POST_TITLE.md>`\
Then edit the new file.
- 🚧 Basic markdown document: https://...
- 🚧 Post header document: https://...
- 🚧 About resource folders struct: https://...

## Run local server to test and build 
- **Start hugo server**
    ```bash
        hugo server
    ```
    Default port is **1313** so you can access **http://localhost:1313**\
    `hugo help serve` to see all command options

- **Build site**
    ```bash
        hugo
    ```
    Result is saved in folder **public**.\
    `hugo help` to see all command options

<hr/>

🚧 **Next article**: Publish this blog using github page

**Step 6**: Register a new Git Hub Account.

**Step 7**: Create a new public repository.

**Step 8**: Inside repository setting, enable github pages.

**Step 9**: Upload folder **public** to repository

**Step 10**: Check your online site.

**Bonus:**
 1. Create cname record for your custom domain to github page domain.
 2. Update setting, use custom domain.
 3. Wait for a moment (sometimes to 24 hours) and check Enforce HTTPS

