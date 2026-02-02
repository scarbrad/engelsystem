# Engelsystem Docker Builder

This repository contains a GitHub Action to build Docker images for [Engelsystem](https://github.com/engelsystem/engelsystem) automatically.

## How to Trigger a New Build

To build a new version of Engelsystem (e.g., matching the official version `v1.2.3`), you need to create an empty commit and tag it. This triggers the GitHub Action.

### Steps

1.  **Check for the latest version** in the official [Engelsystem repository](https://github.com/engelsystem/engelsystem/tags).
2.  **Run the following commands** in your terminal (replace `v1.2.3` with the desired version):

```bash
# 1. Create an empty commit to mark the release in history
git commit --allow-empty -m "Release v1.2.3"

# 2. Tag the commit with the version number
git tag v1.2.3

# 3. Push the commit and the tag to GitHub to start the build
git push origin main v1.2.3
```

The GitHub Action will now:
1.  Checkout the official Engelsystem repository at the tag you specified (e.g., `v1.2.3`).
2.  Build the Docker image.
3.  Push the image to the GitHub Container Registry.