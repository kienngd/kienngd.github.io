# How to Update Your Docker Image Without Starting From Scratch


Hi, it's me here again! 👋

Ever been in this situation? You have a `Docker image` that you've been using for a while, and suddenly you `need to add some new softwares`. Building everything from scratch again? Ain't nobody got time for that! 😅

Let me share a neat trick I use to save time.

<!--more-->

![Docker](banner-docker.jpg "Docker")

## The Situation

Let's say I have an image called `my-image` (based on Ubuntu). After using it for a while, I realize I need to install some extra packages. Sure, I could modify the original Dockerfile and rebuild everything, but that would take forever! 🐌

## The Quick Solution

Here's a faster way to do it:

1. Create a new Dockerfile (let's call it `Dockerfile.update`):
    ```dockerfile
    FROM my-image
    USER root
    RUN apt update && apt install -y your-new-package
    # Add more commands as needed
    ```

2. Build a new image:
    ```bash
    docker build -t my-image-new -f Dockerfile.update .
    ```

3. Play the name-swapping game:
    ```bash
    # Backup old image
    docker tag my-image my-image-backup

    # Make new image the main one
    docker tag my-image-new my-image
    ```

4. Test it out:
    ```bash
    docker run my-image some-command
    ```

5. If everything works, clean up:
    ```bash
    docker rmi my-image-backup my-image-new
    ```

And that's it! Your image is updated, and your disk space is clean. 🎉

## Why This is Cool

- Much `faster` than rebuilding from scratch
- `Safe` (you have a backup if something goes wrong)
- Saves disk space after cleanup

**Remember**: Always **test** your updated image **before removing** the backup! Better safe than sorry! 😉

Happy Dockering! 🐳

