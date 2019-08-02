# pcs-org-au-dmoj
Deployment configuration and encyrpted secrets for deploying DMOJ to pcs.org.au

Secrets are stored in the `secrets` folder and configured to be committed using the `git-crypt` utility. You will need the GPG key to unlock the secrets.

## Prerequisites
- Running Traefik instance to proxy the site
- Make sure `git-crypt` is installed: `apt install git-crypt`

## Deployment
- `git clone --recurse-submodules` this repository and `cd` into it
  - If you cloned without submodules, you can clone them now with `git submodule update --init --recursive`
- `git-crypt unlock /path/to/keyfile` to decrypt secrets (never commit the keyfile to this repository)
- Check you are happy with `.env`
- Make folders as necessary:
  - `source .env` to load environment variables
  - `mkdir -p $PROBLEMS_PERSISTENT_ROOT/problems`
  - `mkdir -p $MYSQL_PERSISTENT_ROOT`
- `docker-compose build` to rebuild the images for good measure
  - This may take a few minutes depending on cache
- `docker-compose up -d`
