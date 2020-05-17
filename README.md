# Visual Studio EditorConfig

## About

Most sources on the internet recommend checking an `.editorconfig` file into every repository, much like a `package.json` or `Nuget.config` file.  However, you will likely be using the same coding style preferences in most of the projects that you develop with Visual Studio (C# projects in particular).  Therefore, to avoid duplicating these preferences into every new repository (a nightmare to update if your style preferences ever change), it is much simpler to have a single `.editorconfig` file in its own repository, and then your other repos utilize that one.

This repository contains such an `.editorconfig`.  I developed it for my own projects, but I hope that my style preferences are general enough, to be of use to any Visual Studio project, in any repository.

## Usage

Suppose you have the following directory structure:
```
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
```
MKLINK "root-directory\.editorconfig" "root-directory\VsEditorConfig\.editorconfig"
```

On MacOS/Linux, run the following command:
```
ln -s "root-directory/VsEditorConfig/.editorconfig" "root-directory/.editorconfig"
```

Subsitute the above paths with those needed for your particular directory structure (absolute paths work best).  Once the link is created, you will be able to update the `.editorconfig` with `git pull` as normal, and the latest style preferences will then be available to all of your repositories (after restarting Visual Studio).

If you don't like any of our style/formatting preferences, then you can either fork our `.editorconfig` to use it as a starting point and modify it to fit your particular conventions, or add a separate `.editorconfig` with your overrides to the individual repos that need those overrides.
