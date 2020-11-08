Flatpak manifest for GitHub Destkop app
=======================================

This repository contains the files to create a Flatpak version of the [GitHub Desktop](https://desktop.github.com/) Git client.

It is based on [this fork](https://github.com/shiftkey/desktop) which contains extra work for better Linux integration, that is, for now, not official.

Installation
------------

To build and install this Flatpak, you have to [install Flatpak, Flatpak builder and the Flathub repo](https://flatpak.org/setup/). Don't forget to initialize this repo submodules. Then run:

```sh
flatpak-builder build com.github.Desktop.yaml --repo=repo --install --force-clean --install-deps-from=flathub
```

Once installed, launch GitHub Desktop by running:

```sh
flatpak run com.github.Desktop
```

Updating `desktop` repo and dependencies
----------------------------------------

Flatpak builder doesn't allow the build scripts to access the internet, so you have to download all the required dependencies before hand. These dependencies are listed in the `generated-sources.json`. That's the reason we have a fixed commit for building `desktop` repo, since can guarantee that `generated-sources.json` dependencies match.

To update `desktop` repo to its latest commit and update the dependencies, you have to:

1. Clone [https://github.com/shiftkey/desktop](https://github.com/shiftkey/desktop) inside this repo.
2. Change `com.github.Desktop.yaml` commit to the desired one here:

    ```yaml
    ...
          - type: git
            url: https://github.com/shiftkey/    desktop.git
            commit: <put the commit here>
    ...
    ```

3. Run `generated-sources` script to update `generated-sources.json`.

4. Make sure the patches in the `patches` directory still apply.
