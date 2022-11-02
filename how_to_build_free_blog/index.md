# How to build a free blog

Hello, in this post will learn how to build a free personal blog using Hugo + Github page. Have fun!

**Step 1**: Install hugo.

- Download hugo from: https://github.com/gohugoio/hugo/releases
- Install in your PC.

**Step 2**: Create a new site.

- Quick start document: https://gohugo.io/getting-started/
- Command: 
```bash
hugo new site myblog
```

**Step 3**: Setup your hugo theme.

- Find a theme from: https://themes.gohugo.io/.
- Download theme and put into site's themes directory.
Example we want to use Ananke theme:
```bash
cd myblog
git init
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
```
- Inside file config.toml.
```text
theme = "ananke"
```
<!--more-->
**Step 4**: Create new post.
```bash
hugo new <POST TYPE>/<POST_TITLE.md>
```
Then edit the new file.

**Step 5**: Test your site in your PC and build site.

**Start hugo server**
```bash
hugo server
```
Default port is **1313** so you can access **http://localhost:1313** or **http://[YOUR IP]:1313**

**Build site**
```bash
hugo
```
Result is saved in folder **public**.

**Step 6**: Register a new Git Hub Account.

**Step 7**: Create a new public repository.

**Step 8**: Inside repository setting, enable github pages.

**Step 9**: Upload folder **public** to repository

**Step 10**: Check your online site.

**Bonus:**
 1. Create cname record for your custom domain to github page domain.
 2. Update setting, use custom domain.
 3. Wait for a moment (sometimes to 24 hours) and check Enforce HTTPS
