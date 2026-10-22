# Shota Kato's Portfolio

This is the personal portfolio site of Shota Kato, mainly showcasing research and publications. It is based on the [aafu theme](https://github.com/darshanbaral/aafu) by Darshan Baral.

Visit the live site [here](https://s-kat0.github.io/).

## Local development

Run Hugo through the npm scripts:

```sh
npm ci
npm run dev    # local preview server
npm run build  # production build into ./public
```

The scripts run Hugo from the physical path of the repository (`pwd -P`). Hugo grants Node read access only to the project directory, and Node resolves symbolic links before checking that permission. When the repository is opened through a symbolic link (e.g., `~/Dropbox` → `~/Library/CloudStorage/Dropbox`), running `hugo` directly therefore fails in PostCSS with `ERR_ACCESS_DENIED`.
