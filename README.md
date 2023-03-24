## Intro

### What

A **'dev/localhost'** *proof-of-concept demo* of a **server-based 'mechanism'** for users to access files in **their own** directory/folder **only**. 

### How

For a URL in the form https://SOME_DOMAIN/`URL_BASE_PATH`/some-identifier ,

at the server end:

- the **username**, re: SSO (Single Sign-On), is obtained from a server/web variable (typically `REMOTE_USER`)

- the 'URL path' is *'rewritten'*, to display a list of files under a **private dir** (i.e. `PRIVATE_BASE_DIR`).

----

## Install

Tested on Linux (Ubuntu 22.04) and on Windows 10 (WSL) - with Caddy `v2.6.4` (2023-02-14).

### Prereqs

If `caddy` is not already installed, download it from here: https://github.com/caddyserver/caddy/releases

- For instance: `caddy_2.6.4_linux_amd64.tar.gz`.

- (`caddy` itself is one single binary, which does NOT need `sudo`.)

### Files

Grab the files in this repo - e.g. by using the 'standard' `git clone` procedure:

```sh
git clone --depth 1 https://github.com/png1ed/caddy-sso-file-server
cd caddy-sso-file-server
```

----

## Run

- Simplest invocation is:

```sh
caddy run
```

(The default 'config file' is named `Caddyfile`.)


- To specify a value for a 'config option', pass it to `caddy` - such as in these examples:


```sh
PORT=8080 caddy run

PORT=8080 REMOTE_USER=s1234567 caddy run
```

### URLs

In a web browser, open these URLs: (assuming the 'config options' are their default values)

- http://localhost:8027/the-base/course-ABC
- http://localhost:8027/the-base/course-DEF
- http://localhost:8027/the-base/course-XYZ/assessment-001

### Username

- For *test/preview* purposes, the username can be **changed**: (`REMOTE_USER`)

```sh
REMOTE_USER=s1234567 caddy run
```

----

## Config Options

- Referring to `Caddyfile`:

| Variable           | Default Value      | Remarks                        |
|--------------------|--------------------|--------------------------------|
| `PORT`             | 8027               | (Arbitrary number.)            |
| `REMOTE_USER`      | mock_user          | See the 'remarks' below.       |
| `URL_BASE_PATH`    | the-base           | (Can set it to: some-app-name) |
| `PRIVATE_BASE_DIR` | ./private_base_dir | See the 'remarks' below.       |

- Remarks about `REMOTE_USER`:

   - 'Best practice' is to **have** a default - as a *'safeguard'*.
   - (In the config file, can **modify** string `mock_user` to a *preferred* default, e.g. `v1dt____`.)
 
- Remarks about `PRIVATE_BASE_DIR`:

    - The dir **must NOT be 'web-accessible'** re: the web server - i.e. must NOT be under `/var/www/` or similar.
    - (Can be an absolute path.)

