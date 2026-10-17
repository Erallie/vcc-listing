# Erallie's VCC Packages

Central VCC repository listing for VRChat world packages by Erallie.
This is a static listing website, not a Unity project. Package source code
and release ZIPs stay in their respective project repositories.

## Publish this repository

1. Move this entire folder, including its hidden `.git` directory, to:
   `G:\Projects\VRChat\Unity_Projects\vcc-listing`.
2. Create a public, empty GitHub repository named `vcc-listing` under Erallie.
   Do not initialize another README or license on GitHub.
3. Commit the customized files locally, add the new remote, and push:

```powershell
git add .
git commit -m "Configure Erallie's central VCC listing"
git remote add origin https://github.com/Erallie/vcc-listing.git
git push -u origin main
```

4. In the GitHub repository, open **Settings > Pages** and set the build
   source to **GitHub Actions**.
5. Open **Actions > Build Repo Listing > Run workflow** and select `main`.
   If an initial push run happened before Pages setup and failed, run it again.

The existing clone retains the official template's history and an `upstream`
remote. It has no `origin` remote until you connect your own repository.
Nothing has been pushed or published by this local setup.

## Public addresses after deployment

- Website: https://erallie.github.io/vcc-listing/
- VCC listing JSON: https://erallie.github.io/vcc-listing/index.json
- Add to VCC:
  `vcc://vpm/addRepo?url=https%3A%2F%2Ferallie.github.io%2Fvcc-listing%2Findex.json`

The listing ID is `com.erallie.vcc-listing`. It is separate from package IDs
and from the existing Stage Amplifier project's listing. Existing subscribers
must add this new listing separately; this setup does not migrate them.

## Included packages

The current `source.json` scans release ZIPs from:

- `Erallie/stage-amplifier-and-whitelist`

That repository currently publishes both `com.erallie.stage-amplifier` and
`com.erallie.minimal-amplifier`, so both can appear without copying their source
into this repository.

When Minimal Amplifier has its own GitHub repository with published package
release ZIPs, add that repository to `githubRepos` too. Do not add a repository
that does not exist or has no package releases yet.

Each release ZIP must contain its package's `package.json` at the ZIP root.
VCC package identity comes from the manifest's `name`, not the GitHub repo name.

## Refresh the listing

After publishing a package release in another repository, run this repository's
**Build Repo Listing** workflow. Release events in another repository do not
trigger this workflow automatically. No scheduled polling is configured.

Pushes to `source.json`, `Website/`, or the listing workflow on `main` rebuild
the site automatically. A `repository_dispatch` event named `packages-updated`
is also supported for future integration; sending it from another repository
requires separately configured authorization and is not set up here.

## Customize

- `source.json`: listing name, ID, canonical URL, author, and package sources.
- `Website/index.html`: layout and social metadata.
- `Website/styles.css`: appearance.
- `Website/app.js`: Add to VCC and other page interactions.

The page uses the official VRChat listing template. The template's placeholder
banner and favicon files are retained. No banner is enabled in `source.json`:
a central listing should not reuse one individual project's banner by default.
To enable a banner, replace `Website/banner.png` and add a top-level
`"bannerUrl": "banner.png"` property to `source.json`.

## Template credit

Based on the official VRChat Community
[VPM Package Listing Template](https://github.com/vrchat-community/template-package-listing),
using [package-list-action](https://github.com/vrchat-community/package-list-action).
Individual packages retain their own licenses. This listing does not relicense
third-party template files or any listed package.
