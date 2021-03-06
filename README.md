github-clonetools
=======================
Python command line tool to clone all public repos and gists from a single github account,
and populate empty new repos with a set of templated common default files.
    
# Installation:
Developed for Python 2.7x work, though it may work for other distributions.

To install, run `python setup.py build install`

# Usage:

The `setup.py` file installs three command line scripts into your python scripts directory.

- `clonerepos [username] [directory]` clones all public github repos from github user 
`username` into directory `directory`.
If a directory is given but doesn't exist, it will be created.
If no directory is given, the repos are cloned into the current working directory.
If a subdirectory already exists that matches the name of a repo, that repo is skipped. 

- `clonegists [username] [directory]` clones all public github gists from github user 
`username` into directory `directory`. 
If a directory is given but doesn't exist, it will be created.
An empty Wing IDE project file will be created at the root of this directory.
The directories are named according to the first file in a gist. If no directory is given, 
the repos are cloned into the current working directory.
If a subdirectory already exists that matches the name of a gist, that gist is skipped. 

- `cloneall [username] [repo directory] [gists directory]` clones all public github 
repos and gists from github user `username` into directories `repo directory` 
and `gists directory`, respectively.
If these directories are given but don't exist, they will be created.
If no directories are given, all repos and gists are cloned into the current working directory.
If a subdirectory already exists that matches the name of a repo or gist, that repo or gist is skipped. 

# Files generated for empty repos: 
When an empty repo is cloned using either the `clonerepos` or `cloneall` script,
the directory is automatically populated with a set of templated default files. These include:

- `.gitignore`
- `README.md`
- `LICENSE.txt`

Additionally, for empty projects with the word "python" in the description:

- A templated `setup.py` file, pointing to a created `src/` directory
- An empty `src/__init__.py` file

These files can be templated with repo-specifc information (or however else you'd like) using the methods in
`github_clonetools/default_files.py`.
Individual default files can be added/removed to the script behavior by editing
the method `write_default_files` in `github_clonetools/clonetools.py`.

This behavior can be tested using any empty repo. I use https://github.com/thearn/test-empty-repo for this purpose.

# Examples:

To clone all of github user thearn's public gists and repos into the current directory:
```bash
$ cloneall thearn
```

To clone all github user thearn's public gists and repos into the separate `thearn_repos` and `thearn_gists` directories:
```bash
$ cloneall thearn thearn_repos thearn_gists
```

To clone all of github user thearn's public repos into a directory named `thearn_repos`:
```bash
$ clonerepos thearn thearn_repos
```

To clone all of github user thearn's public gists into a directory named `thearn_gists`:
```bash
$ clonegists thearn thearn_gists
```
