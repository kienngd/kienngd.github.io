# Git log quickly and easily


These are some `git log commands` I use everyday and I think they are helpful for you.
<!--more-->

## Log all
```bash
    git log
```

## Filter the commits
```bash
    # Get last n commits
    git log -n 5

    ## Filter by dates
    # show commits from the past two weeks
    git log --since="2 weeks ago"
    # or by using --after
    git log --after="2 weeks ago"

    # show commits until January 1, 2024
    git log --until="2024-01-01"
    # or by using --before
    git log --before="2024-01-01"

    # get commits from a specific author
    git log --author="Author Name"

    # show commits with "fix" in the message
    git log --grep="fix"
```

## Formatting output
You can also format the log messages by using the `--pretty` option.
### Predefing format
- `oneline`: Displays each commit on a single line.
- `short`: Includes commit hash, author, date, and subject.
- `medium`: Adds commit message and file changes.
- `full`: Includes full commit information.
- `format`: Allows custom formatting using placeholders (e.g., %H for commit hash, %an for author name, %s for subject).

```bash
    # show concise logs
    git log --pretty=oneline
    # custom format
    git log --pretty=format:"%h - %s"
    git log --pretty=format:"Commit: %H\nAuthor: %an\nDate: %ad\nSubject: %s\n\n%b"
```
### Specifiers
- `%H` Commit hash
- `%h` Abbreviated commit hash
- `%T` Tree hash
- `%t` Abbreviated tree hash
- `%P` Parent hashes
- `%p` Abbreviated parent hashes
- `%an` Author name
- `%ae` Author email
- `%ad` Author date (format respects the --date=option)
- `%ar` Author date, relative
- `%cn` Committer name
- `%ce` Committer email
- `%cd` Committer date
- `%cr` Committer date, relative
- `%s` Subject

## Other options
- `--graph`: Display a commit graph.
- `--reverse`: Show commits in chronological order (oldest first).
- `--no-merges`: Exclude merge commits.
\
\
**And the last thing**: You can combine multiple options
