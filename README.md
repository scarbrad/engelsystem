# Engelsystem Docker Builder

This repository contains a GitHub Action to automatically build and package Docker images for the [official Engelsystem](https://github.com/engelsystem/engelsystem).

The workflow builds the image from the **official upstream repository** and pushes it to the GitHub Container Registry (GHCR).

## How it Works

The build process is triggered in three ways:

### 1. Weekly Automatic Build (Recommended)
*   **Schedule:** Runs every Monday at 03:00 UTC.
*   **Version:** Automatically detects the **latest stable release** of Engelsystem via the GitHub API.
*   **Result:** Pushes a fresh image (e.g., `engelsystem:v3.6.0-build.42`) containing the latest base image updates.

### 2. Manual Trigger
*   Go to **Actions** -> **Build and Push Engelsystem** -> **Run workflow**.
*   **Input:** You can specify a Release Tag (e.g., `v3.6.0`) or a Branch (e.g., `main`).
*   **Default:** Builds `main` if no version is specified.

### 3. Git Tag Mirroring
*   If you push a tag to this repository (e.g., `v3.6.0`), the workflow will checkout the **same tag** from the official repository and build it.
*   **Command:**
    ```bash
    git commit --allow-empty -m "Release v3.6.0"
    git tag v3.6.0
    git push origin main v3.6.0
    ```

## Docker Image Tags

Images are pushed to GitHub Container Registry with the following tags:

*   **Version Tag:** e.g., `ghcr.io/USER/engelsystem:v3.6.0` (Updated to point to the latest build of this version)
*   **Unique Build Tag:** e.g., `ghcr.io/USER/engelsystem:v3.6.0-build.123` (Permanent tag for this specific build run)

## Configuration

The workflow is defined in `.github/workflows/build.yml`. It uses the `engelsystem/engelsystem` repository as the source for the code and Dockerfile.