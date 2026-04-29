# Udon Essentials Plus — VPM Listing

This repo hosts the VCC listing for [Flare26/Udon-Essentials-Plus](https://github.com/Flare26/Udon-Essentials-Plus), a collection of modular UdonSharp packages for VRChat world creators.

The listing is published via GitHub Pages and can be added to VCC at:
```
https://flare26.github.io/Udon-Essentials-Plus-Listing/index.json
```

## Packages

| Package | ID |
|---|---|
| Udon Essentials Plus | `com.n8bits.udon-essentials-plus` |
| AudioLink Goodies | `com.n8bits.audiolink-goodies` |
| Cam Switcher | `com.n8bits.cam-switcher` |
| Light Volumes Integrations | `com.n8bits.light-volumes-integrations` *(coming soon)* |
| Summon Menu | `com.n8bits.summon-menu` *(coming soon)* |

All packages live in the [Udon-Essentials-Plus](https://github.com/Flare26/Udon-Essentials-Plus) repo under `Packages/`. Only packages that have a GitHub Release will appear in the listing.

## Releasing a Package

Releases are triggered manually per package from the [Udon-Essentials-Plus Actions tab](https://github.com/Flare26/Udon-Essentials-Plus/actions):

1. Bump the `version` field in the relevant `package.json`
2. Go to Actions → pick the workflow for that package (e.g. *Release - Udon Essentials Plus*)
3. Click **Run workflow**

The workflow reads the version from `package.json`, creates a tagged GitHub Release with a `.zip` and `.unitypackage`, and the next listing build picks it up automatically.

Tags are prefixed by package name (e.g. `udon-essentials-plus-1.0.0`) so releases from different packages don't collide.

## Rebuilding the Listing

The listing rebuilds automatically whenever `source.json` is pushed to `main`, or can be triggered manually via the [Build Repo Listing](../../actions/workflows/build-listing.yml) workflow.

The build action scans all releases in `Flare26/Udon-Essentials-Plus`, finds the package zips, reads their `package.json` to identify each package, and publishes the updated index to GitHub Pages.

To **add a new package** to the listing: run its release workflow in the package repo first, then push any change to `source.json` here to trigger a rebuild.

To **withhold a package** from the listing: simply don't run its release workflow. Packages without a release are invisible to VCC regardless of what's in the source repo.

## Customizing the Landing Page

The `Website/` directory contains the landing page. Most content is filled in automatically from [`source.json`](source.json) and the `package.json` of each released package (display name, description, keywords). 

To update what appears on the page for a package, edit its `description` or `keywords` fields in `Packages/com.n8bits.{name}/package.json` in the package repo, cut a new release, and the next listing build will reflect the changes.

## source.json Reference

| Field | Value |
|---|---|
| `url` | `https://flare26.github.io/Udon-Essentials-Plus-Listing/index.json` |
| `githubRepos` | `["Flare26/Udon-Essentials-Plus"]` |

The `githubRepos` field is all that's needed — the build action auto-discovers every released package in that repo.
