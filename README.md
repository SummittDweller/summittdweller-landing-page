# summittdweller-landing-page

This project defines the [Hugo](https://gohugo.io/)-generated landing page for [summittdweller.com](https://summittdweller.com/).

# Deploying This Site

This site is deployed via [DigitalOcean App Platform](https://docs.digitalocean.com/products/app-platform/), which is connected directly to this GitHub repository. There is no manual deployment step:

1. Commit and push changes to the `main` branch of this repo.
2. App Platform detects the push, clones the repo (including the `themes/bootstrap-bp-hugo-startpage` git submodule), builds the site with its Hugo buildpack, and serves the static output at [summittdweller.com](https://summittdweller.com/).

Note that the `baseURL` is intentionally commented out in `config.toml` so that App Platform can serve the site from whatever URL it assigns.

# Updating This Site

The process of adding a site, or making any addition/change, to this page is now very simple:

```
cd ~/GitHub/summittdweller-landing-page
# ...edit content, config.toml, etc...
git add -A
git commit -m "Describe your change"
git push
```

App Platform *automagically* takes care of the rest!

# Legacy Docker Deployment (Retired)

This site was previously deployed as a Docker image (`summittdweller/summittdweller-landing`, later `mcfatem/summittdweller-landing`) pushed to Docker Hub and run on a DigitalOcean Docker droplet behind Traefik, with Watchtower auto-pulling new `:latest` images. That workflow is retired; its artifacts (`Dockerfile`, `push-update.sh`, etc.) have been preserved in the `.out-of-the-way/` directory for reference.
