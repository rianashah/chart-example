# Homework 6: Chart Example

In your home directory, make a folder called `Development`, if it doesn't exist. This is where we will keep all of the code for the class. Next, make sure that you are inside that folder, by checking the output of the following command:

```shell
pwd
```

If `pwd` shows that you are in a different directory, run `cd ~/Development` and check with `pwd` again.

## How to clone this repo

Next, clone this repository by clicking the green button in the upper right corner, selecting `SSH` and copying the string that looks like `git@github.com:code4policy/<REPO-NAME>.git` (`<REPO-NAME>` will be the name of your repository). Then, in the terminal run the following:

```
git clone git@github.com:code4policy/<REPO-NAME>.git
```

Note that by default, git will clone the repository into a folder with name `<REPO-NAME>`. After the repo is cloned, open that directory (use `cd`).

## Run a local server

D3.js charts won't work unless you're running a web server. This can be done locally with:

```
python3 -m http.server
```

Once you run this, you can open up the website by typing `http://localhost:8000/` into the browser. You'll need to open up a new tab in the terminal to continue your work. Make sure to `cd` back into this project folder and then open up the project in sublime text with `subl .`

# Task

1. Split up the HTML, CSS and JavaScript
2. 
