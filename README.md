# VisualStudioEditorConfig

## About

Most sources on the internet recommend checking an .editorconfig file into every repository, much like a .gitconfig or packages.config file.  However, you will likely be using the same coding style preferences in almost every project that you develop with Visual Studio (C# projects in particular).  Therefore, to avoid duplicating these preferences into every new repository (a nightmare to update if your style preferences every change), it is much simpler to have a single .editorconfig file in its own repository, and then your other repos utilize that one.

This repository contains such an .editorconfig.  It was developed for Danware's projects, but we hope that our style preferences are general enough, and in keeping with good .NET coding practices, to be of use to any Visual Studio project, in any repository.

## Usage

Suppose you have the following directory structure:
```
C:\
    \git
        \VisualStudioEditorConfig
            .editorconfig
        \Repo1
        \Repo2
        \RepoGroup
            \Repo3
            \Repo4
        ...
```
If you want to use the same style preferences in all of your repos (Repo1, Repo2, Repo3, Repo4, etc.), then you should put the .editorconfig file in the root "C:\git" folder.  Unfortunately, the .editorconfig file was cloned into the subfolder "\VisualStudioEditorConfig".  You could copy the file to C:\git, but you would have to re-copy it anytime your style preferences change.  The solution is to create a symbolic link in the root folder to the versioned .editorconfig.

At an elevated command prompt, run the following command:
```
MKLINK C:\git\.editorconfig "C:\git\VisualStudioEditorConfig\.editorconfig"
```
subsituting the paths with those needed for your machine.  If you do not use an elevated command prompt (i.e., a command prompt opened with "Run as Administrator"), then you will get the error: `You do not have sufficient privilege to perform this operation.`  Once the link is created, you will be able to update the .editorconfig with `git pull` as normal, and the latest style preferences will then be available to all of your repositories.  Of course, your individual repos can still override these preferences with their own .editorconfig, e.g., if you don't like one of Danware's preferences.
