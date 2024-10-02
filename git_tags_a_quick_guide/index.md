# Git Tags: A Quick Guide


![Git Tag a quick guide](git-tag-banner.webp "Git Tag a quick guide")
`Git` is a popular version control system. It helps developers `track changes` in their code. `Git tags` are like `bookmarks` for important points in your project's history.

## Here are some common Git tag commands:
1. List all tags:
   ```
   git tag # List all tags
   git tag -l "v1.8.5*" # List tags matching a pattern
   git tag -n # List all tags with commit message
   ```
   
<!--more-->

1. Create a new tag:
   ```
   git tag v1.0 # Create new tag from current commit
   git tag -f v1.0 # Force update tag if existed
   git tag -a v1.0 -m "Release version 1.0" # Create new tag with commit message
   git tag -a v1.0 9fceb02 -m "Release version 1.0" # Create new tag from commit-hash `9fceb02`
   ```



1. Delete a local tag:
   ```
   git tag -d v1.0
   ```

1. Delete a remote tag:
   ```
   git push origin --delete v1.0
   git push origin :refs/tags/v1.0
   ```

1. Push a tag to remote:
   ```
   git push origin v1.0
   git push origin --tags
   
   ```

## Other useful commands:
- Checkout a tag: 
  ```
  git checkout v1.0
  ```
- Compare two tags: 
  ```
  git diff v1.0 v1.1
  ```

`Git tags` are helpful for marking `release versions` or `important milestones`. They make it easy to `find specific points` in your project's `history`.
