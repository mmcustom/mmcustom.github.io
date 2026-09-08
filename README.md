# mmcustom.github.io

This is the root GitHub Pages site for the `mmcustom` account. Its only current
job is to host the **Digital Asset Links** file that the Bakery Rush Android
app needs at:

```
https://mmcustom.github.io/.well-known/assetlinks.json
```

That file has to live at the bare domain root — GitHub Pages project repos
(like `Bakery-Rush`) only serve under `/Bakery-Rush/`, and Android always
looks for `.well-known/assetlinks.json` at the root of the domain, no matter
what path the app actually points at. A repo literally named
`mmcustom.github.io` is the one GitHub auto-serves at the bare root, so this
repo exists to carry that one file.

**Important — GitHub Pages runs Jekyll by default, which ignores any file or
folder starting with a dot (like `.well-known`).** The empty `.nojekyll` file
in this repo turns that off so `/.well-known/assetlinks.json` actually gets
served. Don't delete it.

## Setup steps

1. Create a new **public** GitHub repo named exactly `mmcustom.github.io`
   (this exact name is what makes GitHub serve it at the domain root instead
   of under a `/reponame/` sub-path).
2. Push the contents of this folder to its `main` branch.
3. In the repo's Settings → Pages, set the source to deploy from `main` /
   root (usually auto-detected for a repo with this name).
4. Confirm it's live: `https://mmcustom.github.io/.well-known/assetlinks.json`
   should return the JSON below, not a 404.
5. Once the Android package is built and uploaded to Google Play Console once,
   go to **Play Console → your app → Setup → App integrity** and copy the
   **SHA-256 certificate fingerprint** shown there. Replace
   `REPLACE_ME_WITH_SHA256_FINGERPRINT` in `.well-known/assetlinks.json` with
   that value, commit, and push. That's what removes the browser address bar
   from the Android app and makes it look like a real native app.

Until step 5 is done with the real fingerprint, the Android app will still
work, it'll just show a thin browser address bar at the top instead of
looking fully native.
