# GIT Commit message conventions


<!--more-->

## Commit message conventions
Ref-Url: https://www.conventionalcommits.org/en/v1.0.0/
```
<type>[optional scope]: <description>

[optional body]

[optional footer]
```

## Types list
- feat: add new feature
- fix: fix bug
- refactor: 
- docs: documents
- chore: small bugs not-relevant to code
- style
- perf: performance
- vendor: Update dependencies', packages' ... version
...

## Notes:
- BREAKING CHANGE in body.

## Examples
```
Example 1:
feat!: implement multi-languages

BREAKING CHANGE!: PHP Version change.

Example 2:
fix: homepage's bug 

Long long long description of bug 

Some other data.

Reviewed-by: Z
Ref: #123


Example 3:
fix(player): Video player can not initialize
```

