<!--cspell:ignore sarg  -->
# Go Dev Container

[![OpenSSF Scorecard](https://api.scorecard.dev/projects/github.com/sarg3nt/go-dev-container/badge)](https://scorecard.dev/viewer/?uri=github.com/sarg3nt/go-dev-container)
[![Scorecard supply-chain security](https://github.com/sarg3nt/go-dev-container/actions/workflows/scorecard.yml/badge.svg)](https://github.com/sarg3nt/go-dev-container/actions/workflows/scorecard.yml)
[![trivy](https://github.com/sarg3nt/go-dev-container/actions/workflows/trivy.yml/badge.svg)](https://github.com/sarg3nt/go-dev-container/actions/workflows/trivy.yml)
[![Dependabot Updates](https://github.com/sarg3nt/go-dev-container/actions/workflows/dependabot/dependabot-updates/badge.svg)](https://github.com/sarg3nt/go-dev-container/actions/workflows/dependabot/dependabot-updates)
[![Dependency Review](https://github.com/sarg3nt/go-dev-container/actions/workflows/dependency-review.yml/badge.svg)](https://github.com/sarg3nt/go-dev-container/actions/workflows/dependency-review.yml)
[![Release](https://github.com/sarg3nt/go-dev-container/actions/workflows/release.yml/badge.svg)](https://github.com/sarg3nt/go-dev-container/actions/workflows/release.yml)

A Go Dev Container using `mise` to install Go and other conventinet tools.  `mise` can then be used to install various other go versions as needed.

- [Tools Included](#tools-included)
  - [Go Tooling](#go-tooling)
  - [Utilities](#utilities)
- [Using `mise` to Manage Go Versions](#using-mise-to-manage-go-versions)
- [Included `.devcontainer` Config](#included-devcontainer-config)
- [Initial Worksation Setup](#initial-worksation-setup)
  - [WSL](#wsl)
  - [Windows Font Install](#windows-font-install)
    - [Windows Terminal Font Setup](#windows-terminal-font-setup)
    - [Visual Studio Code Font Setup](#visual-studio-code-font-setup)
- [Initial Dev Container and Project Setup](#initial-dev-container-and-project-setup)
  - [`dev.sh`](#devsh)
  - [Dev Container Setup](#dev-container-setup)
- [Contributions](#contributions)
- [Author](#author)


## Tools Included

See the root `mise` config file at `home/vscode/.config/mise/config.toml` for all tools and versions.

### Go Tooling
- golang
- golangci-lint
- goreleaser

### Utilities
- bat
- fzf
- gitui
- helm
- k9s
- kubectl
- kubectx
- lsd
- starship
- yq

## Using `mise` to Manage Go Versions

1. Copy the `.mise.toml` file from the root of this repo to your projects repo root and modify it as needed.
1. The provided `.devcontainer` will automatclly call `mise install` to install the custom versions of the applications.
1. After the container is started and you shell into it you may need to call `mise use golang@<version>` to switch to the new version.  The included `help` explains how to do this in more detail and other `mise` commands you can use.

## Included `.devcontainer` Config

This project not only builds the dev container into the provided Docker container it also includes an example implemantion in the `.devontainer` directory.  
Do the following to use this implmention.

1. Cone down the rpository.
1. Copy the `.devcontainer` directory to your project.  Note:  you should not already have a `.devctonaer` directory or things could get weird.
1. Copy the following files to the root of your projects.  All of these are optional but encouraged.
  - `.mise.toml`
  - `cspell.json`  Edit this with your specific words that you need to `cspell` to ignroe globally.
  - `dev.sh` This file helps launch and exec into the dev container.
1. Starship has a custom Power Line command prompt we include, for it to function properly you need one of the Nerd Fonts installed.  See the [Initial Worksation Setup](#initial-worksation-setup) documentiaon for instrucitons on downloading and installing the fonts.


## Initial Worksation Setup

Instructions to set up your worksation.
For more information on Dev Containers check out the [official docs](https://code.visualstudio.com/docs/devcontainers/containers).

### WSL

1. If you will be building Docker containers in Windows, then install Docker Desktop for Windows following [Docker's instructions](https://docs.docker.com/desktop/install/windows-install/).  If you do not need Docker for Windows support then you can [directly install Docker inside of Ubuntu](https://docs.docker.com/engine/install/ubuntu/) **AFTER** you install WSL and Ubuntu in the following steps. 
1. Install VS Code from the [Visual Studio Code website](https://code.visualstudio.com/download) or from the Microsoft Store.
1. Open VS Code and click on the "Extensions" button to the left.  
   1. Search for "Dev Containers" and install it.
   1. Search for "WSL" and install it.
1. WSL is the Windows Subsystem for Linux and facilitates the use of a Linux distruction on Windows.  
Follow the [Microsoft insructions](https://learn.microsoft.com/en-us/windows/wsl/install) to install WSL and a Linux distribution.  Ubuntu is probably the most commong Linux OS used in WSL, but feel free to choose what you want.  Note that the dev container itself uses Rocky Linux but this shouldn't matter to you during use.

### Windows Font Install

To get the full functionality of font ligatures and icons for the Starship prompt you will need to install a [Nerd Font](https://www.nerdfonts.com/) from [Nerd Fonts Downloads](https://www.nerdfonts.com/font-downloads).  If you skip this step the Dev Container terminal command line will look weird and not have icons thus making it harder to read.

Many of us use [FiraCode Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.0.2/FiraCode.zip) or [FiraMono Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.0.2/FiraMono.zip) but you can [preview](https://www.programmingfonts.org/#firacode) any of the fonts and choose which one is best for you.

Download your chosen font and [install it in Windows](https://support.microsoft.com/en-us/office/add-a-font-b7c5f17c-4426-4b53-967f-455339c564c1) then proceed to the next step.

#### Windows Terminal Font Setup

1. Open Windows Terminal, select the menu chevron to the right of the last tab and select settings.
1. On the left select `Profiles` --> `Defaults`
1. Under `Additional Settings` select `Appearance`
1. Under `Font Face` select the name of the font you downloaded, for example if you chose the "Firacode Nerd Font" then you'd choose `Firacode NF`  You may need to check `Show all items` or restart Windows Terminal to see the new fonts.

#### Visual Studio Code Font Setup

1. Select `File` --> `Preferences` --> `Settings`
1. Expand `Text Editor` --> select `Font`
1. In the `Font Family` text box paste the following:  

> **NOTE:** This assumes you chose "FiraCode NF", if not, replace the first font name with the name of the font you installed in Windows.

   ```
   'FiraCode NF', 'CaskaydiaCove NF', Consolas, 'Courier New', monospace
   ```

## Initial Dev Container and Project Setup

The following contains initial project setup.

### `dev.sh`

This script is used to more easily start Visual Studio code and hop into the Dev Container from the terminal that it is ran from.

- Open the `dev.sh` file and set a `docker_exec_command` if desired, this is optional but if this repo is used a lot, it is a nice to have.  This will create a command in the users `.bashrc` and `.zshrc` to quickly exec into this running dev container.
- Change `project_name` to match the name of the repository.  Exaple: If your root project repository is called `my-go-project` then set `project_name` to `my-go-project`

To use the `./dev.sh` script, simply run it, then when VS Code opens, there should be a prompt at the bottom right of the editor saying "Folder contains a Dev Container . . .".  Click the "Reopen in Container" button and VS Code will open the dev container and attach to it.
![Reopen in Container](.devcontainer/reopen_in_container.png)
> **NOTE:** If you have not opened the dev container before or if it has been updated it will download the container from Github, which can take a while.

### Dev Container Setup

Edit the `devcontainer.json` file to make the following changes.

- Change the `name`, by replacing "Template" to the name of your project.
- Replace all instances of `template-` with your projects name and a dash.  Example: `my-project-`

The rest of this doc is typically kept in all projects that use the dev container.

## Contributions

If you would like to contribute to this projects, please, open a PR via GitHub. Thanks.

## Author

David Sargent
- dave [at] sarg3.net
- GitHub at [sarg3nt](https://github.com/sarg3nt)
