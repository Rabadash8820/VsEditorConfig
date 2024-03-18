# Visual Studio EditorConfig

## About

Most sources on the internet recommend checking an `.editorconfig` file into every repository, much like a `package.json` or `Nuget.config` file. This is definitely valid for team or open-source projects, where multiple devs collaborate with different personal coding styles. However, you will likely be using the same quality/style preferences for all of your own personal/private projects/repos. Therefore, to avoid duplicating these preferences into every new repository (a nightmare to update if your quality/style preferences ever change), you can create a single `.editorconfig` file in its own repository, and have your various repos utilize that one. Essentially, that `.editorconfig` becomes one of the many ["dotfiles"](https://dotfiles.github.io/) that define your own personal coding environment.

This repository contains such an `.editorconfig`. I developed it for my own projects, but I hope that my style preferences are general enough to be of use to any Visual Studio project, in any repository. If not, maybe this repo will serve as a point of reference for you to make your own `.editorconfig`!

## Usage

Suppose you have the following directory structure:

```txt
root-directory\
    VisualStudioEditorConfig\
        .editorconfig
    Repo1\
    Repo2\
    RepoGroup\
        Repo3\
        Repo4\
    ...
```

If you want to use the same style preferences in all of your repos (Repo1, Repo2, Repo3, Repo4, etc.), then you should put the .editorconfig file in the "root-directory\" folder.  Unfortunately, the .editorconfig file was cloned into the subfolder "VsEditorConfig\".  You could copy the file to root-directory, but you would have to re-copy it everytime your style preferences change.  The solution is to create a symbolic link in root-directory to the versioned .editorconfig.

On Windows, run the following command at an elevated command prompt.  If you do not use an elevated command prompt (i.e., a command prompt opened with "Run as Administrator"), then you will get the error: `You do not have sufficient privilege to perform this operation.`

```bat
MKLINK "root-directory\.editorconfig" "root-directory\VsEditorConfig\.editorconfig"
```

On MacOS/Linux, run the following command:

```sh
ln -s "root-directory/VsEditorConfig/.editorconfig" "root-directory/.editorconfig"
```

Subsitute the above paths with those needed for your particular directory structure (absolute paths work best).  Once the link is created, you will be able to update the `.editorconfig` with `git pull` as normal, and the latest style preferences will then be available to all of your repositories (after restarting Visual Studio).

If you don't like any of my style/formatting preferences, then you can either fork my `.editorconfig` to use it as a starting point and modify it to fit your particular conventions, or add a separate `.editorconfig` with your overrides to the individual repos that need those overrides.
