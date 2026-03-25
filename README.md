# Zest × Tauri

This repository is a basic template for packaging your Pulp games into a Windows/Mac/Linux application. It's using [Zest](https://tkers.dev/zest) to create a web bundle, and [Tauri](https://tauri.app) to wrap the game in a native app.

## Getting started

1. [Copy this template repository](#1-copy-this-template-repository)
2. [Configure Tauri and Zest](#2-configure-tauri-and-zest)
3. [Upload your game data and icon](#3-upload-your-game-data-and-icon)
4. [Run the build workflow](#4-run-the-build-workflow)
5. [Download the artifacts](#5-download-the-artifacts)

### 1. Copy this template repository

Click the green **Use this template** button and pick **Create a new repository**. Give your project a suitable name, select whether you want it to be **Public** or **Private**, and click **Create repository** to continue.

### 2. Configure Tauri and Zest

First you'll want to update 2 config files. Typically you'll only have to do this step once, when setting up a new project:

Select `zest.conf.json` from the list of files in your repository's **Code** tab, and click the pencil icon to **Edit this file**. Update your game's `title`, an optional `color` (or remove this line if your game uses PulpScript to change the palette), and add or remove any `plugins` you might want.

> To build Tauri apps, it's recommended to leave `autoplay` enabled and keep the `tauri.js` plugin.

Make sure to click **Commit changes...** when you're done to save your Zest configuration to the repo.

Next is the `tauri.conf.json` file, located in the `src-tauri/` folder. Navigate to it and click **Edit this file** again. In this JSON file you'll want to update a few keys:

- `productName` should reflect your game's title
- `mainBinaryName` should reflect the internal binary name, typically this can be (a short version of) your game's title, but without spaces or special characters
- `version` is sometimes shown in the application metadata (this has to be a **valid semver** format, e.g. `1.0.0`)
- `identifier` can be set to your game's bundle ID
- `title` (located under `app.windows[]`) is used in the main window's title bar
- `copyright` (located under `bundle`) should be the author name, and is usually shown somewhere alongside the version number

There are a few other keys you can edit, like the `width` and `height` keys (the initial window size), or the `resizable` and `fullscreen` booleans of the window object.

> Make sure to leave other properties like `withGlobalTauri: true` and `build.frontendDist: "../web"` intact, as the plugin and workflow relies on this.

As before, make sure to **Commit changes...** when you're done!

### 3. Upload your game data and icon

Navigate to the `src/` folder, which is where you'll update your game when a new version becomes available. In there, click the **Add file** button and choose **Upload files**. Upload an `icon.png` and your Pulp project `data.json` file here. Make sure the filename matches exactly, so GitHub will know to overwrite the existing files in this folder.

Optionally write a commit message and describe the changes you made (might be useful if you want to check the log later), and click **Commit changes**.

### 4. Run the build workflow

Finally we get to the good bits! Open up the **Actions** tab and pick the **Compile Tauri apps** workflow. Here you can click the **Run workflow** button (and confirm running it against the `main` branch) to start packaging your game. This process takes around 10 minutes, so grab yourself a cup of coffee while you wait to be amazed.

### 5. Download the artifacts

Once the workflow has completed (indicated by a green checkmark), your artifacs should appear at the bottom of the **Summary** page. Hit the download button for the platform(s) you want, and enjoy the result of your hard work.

Congrats! You're ready to share your creation with the world ✨

## GitHub Actions usage

All free GitHub account include 2000 build minutes per month. Keep in mind that when building for Mac/Windows/Linux simultaneously, you are using approximately 30 minutes (3 platforms times ~10) per build. If you want to disable some platforms, edit the `tauri.yml` file located in the `.github/workflows/` folder. Here you can remove (or comment out, by prefixing the lines with `#`) the platforms you're not interested in. Look for the `strategy.matrix.include` key near the top of the file.

You can check your current usage by navigating to the [Billing and licensing](https://github.com/settings/billing) settings of your account, and selecting the **Actions** tab under the **Metered usage** section.
