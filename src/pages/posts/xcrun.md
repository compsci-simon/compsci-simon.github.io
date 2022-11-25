---
layout: "../../layouts/MarkdownLayout.astro"
title: "M1 Mac: xcrun: error: invalid active developer path"
subtitle: "Error with git after mac update."
url: "xcrun"
pubDate: "25 Nov 2022"
---

I just recently updated my mac to macOS Ventura v13.0.1 and tried to commit some new changes to my repo when I got the error:

```bash
$ xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun
```

This is due to macOS uninstalling commandline tools with the recent update. To fix the issue simply run `xcode-select --install`.

If that did not work then you may need to reset xcode installation.

1. Check if Xcode is installed

```bash
xcode-select -print-path

# If the output of the above command is not similar to the following line, Xcode is not installed. Skip to Step 3.
# /Library/Developer/CommandLineTools
```

2. Remove bad installation

```bash
# Remove the Developer directory
sudo rm -rf $(xcode-select -print-path)

# Remove the CommandLineTools directory
sudo rm -rf /Library/Developer/CommandLineTools
```

3. Install Xcode

```bash
sudo xcode-select --install
```
