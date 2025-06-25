<div align="center">
  <img src="logo.svg" alt="Kubsidian Sync" width="150"/>
  <h1>Kubsidian Sync</h1>
  <p><strong>Synchronizes data from the Kubsidian Federation Server into your vault.</strong></p>
</div>

![Made for Obsidian](https://img.shields.io/badge/Made%20for-Obsidian-blueviolet?style=for-the-badge)

This plugin for Obsidian connects to a **Kubsidian** Federation Server to sync and update your vault with the latest Kubernetes resource documentation. It provides a seamless way to keep your technical documentation automatically in sync with the state of your infrastructure.

## Features

-   **Automatic Background Check**: Periodically checks the server for new updates based on a configurable interval.
-   **Dynamic Status Bar Icon**: A clear and intuitive icon in the status bar provides at-a-glance information about the sync status:
    -   **Orange Border**: A new update is available and ready to be downloaded.
    -   **Red Border**: An error occurred during the last check or the plugin is not configured.
    -   **Rotating Icon**: A sync or check is currently in progress.
-   **One-Click Update**: When an update is available, simply click the status bar icon to download and unpack the latest data into your vault.
-   **Reliable Checksum Verification**: Uses the `overall_checksum` from the `.metadata.json` file inside the archive, ensuring data integrity and avoiding unnecessary downloads based on unreliable HTTP headers.
-   **Secure**: Uses Basic Authentication to connect to your server. Credentials are stored locally within your Obsidian vault's plugin data.

## How It Works

The plugin follows a robust and efficient workflow:

1.  **Check**: Periodically (or when manually triggered), the plugin downloads the `.zip` archive from the configured Federation Server URL.
2.  **Verify**: It unzips the archive in memory, finds the `.metadata.json` file, and extracts the `overall_checksum`. This remote checksum is compared against the last known checksum stored locally.
3.  **Notify**:
    -   If the checksums are different, the status bar icon gets an orange border, indicating an update is ready. The pre-downloaded data is cached, waiting for your confirmation.
    -   If the checksums match, the icon gets a green border, and no further action is needed.
4.  **Sync**: When you click the orange-bordered icon, the plugin uses the pre-downloaded data to:
    -   Delete the old documentation folder.
    -   Unpack the new data into the root of your vault.
    -   Update the local checksum and turn the icon's border green.

## Installation

1.  Ensure you have Obsidian installed.
2.  Install BRAT (Beta Reviewers Auto-update Tester) from the Community Plugins section in Obsidian.
3.  Open the command palette (Ctrl/Cmd+P) and run "BRAT: Add a beta plugin".
4.  Paste the URL of this repository `https://github.com/Air-Mark/kubsidian-sync` into the dialog.
5.  Enable "Kubsidian Sync" in the "Community Plugins" tab in Obsidian's settings.

*(Alternatively, for manual installation:)*
1.  Download the `main.js`, `manifest.json`, and (if any) `styles.css` from the latest release.
2.  Create a new folder named `kubsidian-sync` inside your Obsidian vault's `.obsidian/plugins/` folder.
3.  Copy the downloaded files into the `kubsidian-sync` folder.
4.  Go to Settings -> Community Plugins in Obsidian and enable "Kubsidian Sync".

## Configuration

After installing and enabling the plugin, you need to configure it:

1.  Open Obsidian's `Settings`.
2.  Navigate to the `Kubsidian Sync` tab under "Community Plugins".
3.  Fill in the following fields:
    -   **Federation Server URL**: The full URL to your Kubsidian server's `/federation/export` endpoint. (e.g., `https://kubsidian.com/federation/export`)
    -   **Username**: The username for Basic Authentication on your server.
    -   **Password**: The password for Basic Authentication.
    -   **Check interval (minutes)**: How often the plugin should check for updates in the background. Set to `0` to disable automatic checking (you can still check manually by clicking the icon).

Once configured, the plugin will perform its first check.
