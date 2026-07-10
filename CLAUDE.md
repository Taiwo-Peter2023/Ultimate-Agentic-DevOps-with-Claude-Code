# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static HTML/CSS portfolio website deployed to AWS using S3 and CloudFront, provisioned with Terraform, and automated via GitHub Actions.

## Structure

Pure HTML5 and CSS3. No JavaScript. No build step. No framework.

- `index.html` — main portfolio page; contains inline `<script>` for the mobile menu and section scrolling
- `privacy.html`, `terms.html` — standalone legal pages
- `style.css` — the single stylesheet for all pages
- `images/` — logo, hero banner, profile photo, and course thumbnails

## Development

There is no build, lint, or test tooling. To preview locally, open `index.html` directly in a browser or serve the directory with any static file server (e.g. `python -m http.server`).

## Deployment

The site is served by Nginx from `/var/www/html` on an Ubuntu VM using the default Nginx config — no config changes required. Verify with `curl -I http://localhost` (expect 200) and by loading `http://<public-ip>` in a browser.

## DMI Ownership Rule

Before deployment, a "Deployed by:" line with the student's details MUST be added to the footer in `index.html` (see README.md for the exact format). This proof must be visible in the browser screenshot submission. Do not remove this line once added.


# Command 
terraform init, terraform plan, terraform apply

# Conventions
All infrastructure changes go through Terraform — never modify AWS resources manually
No JavaScript in this project
CSS uses mobile-first approach with breakpoints at 900px, 768px, and 600px

# Safety
Never put secrets in this file. No API keys, passwords, or AWS credentials.