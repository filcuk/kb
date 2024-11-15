---
title: Administration
description: 
published: true
date: 2024-11-15T17:12:31.736Z
tags: 
editor: markdown
dateCreated: 2024-10-31T21:57:35.341Z
---

# Resources

# Troubleshooting
## Interface
### Github page link doesn't work on default langulage with locales
See [github.com](https://github.com/requarks/wiki/discussions/7297).
Locales have been disabled as a 'temporary' workaround.

## Permissions
### EACCES: permission denied
Ensure that the container has access to write to target
```
chown -R 1000:1000 ./<target_dir>
```
> Default container uses node 1000:1000 user & group. Lscr.io container may use custom ones.
{.is-info}

If the problem persists, ensure the 'Target Folder Path' is correct:
```
./data/export	> /app/wiki/data/export
/data/export	> /data/export
```
Which assumes the volumes are mounted in Docker Compose:
```
    volumes:
      - $DOCKERDIR/appdata/wiki/app/config:/config:rw
      - $DOCKERDIR/appdata/wiki/app/data:/data:rw
```

### WARNING: UNPROTECTED PRIVATE KEY FILE!
Ensure that your key has `0600 -rw-------` access:
```
chmod 0600 ./data/secure/git-ssh.pem
```
> You can check current ownership and permissions using `ls -l`
{.is-success}
