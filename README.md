# LineageOS Mirror Manifest

## Using the mirror to sync

Usage: `repo init -u https://github.com/LineageOS/mirror --mirror`

Once the mirror is synced, you can then run `repo init -u /path/to/mirror/LineageOS/android.git -b $BRANCHNAME` and sync normally.

If you want to sync the source quickly but want it to be up-to-date without syncing the mirror every time, then run `repo init -u http://www.github.com/LineageOS/android -b $BRANCHNAME --git-lfs --reference=/path/to/mirror/`. This will init the new repo and fetch all the (available) data from the mirror, but will fallback to GitHub if something is missing in the mirror.

## Updating the mirror manifest

The [default-manifest workflow](./.github/workflows/regenerate-default-manifest.yml)
regenerates `default.xml` daily at 00:00 UTC and commits any changes directly to
`main`. It can also be run manually from the repository's Actions tab.

The workflow uses its built-in `GITHUB_TOKEN` to list public repositories and
push the generated manifest. If either organization contains private
repositories that must be included, configure a `MIRROR_REGEN_TOKEN` repository
secret with a fine-grained personal access token that has read access to both
organizations. The workflow still uses `GITHUB_TOKEN` to push to this
repository.

The workflow fails if GitHub cannot list the organizations' repositories, so it
will not commit a partial manifest because of an API or network error.
