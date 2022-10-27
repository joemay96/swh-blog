# Sketching with Hardware Blog
This is the sketching with hardware blog.

## How to costumize the theme
For changes in your preferred theme.

1. You need to fork the repository of the theme you want so change, so that the changes can be applied.
2. With the command 
``` bash
git submodule add link-to-your-fork themes/how-you-want-your-themes-name
```
you can add a submodule to your repo. After adding the submodule you have to change in your config.toml the name of your theme to the name you gave it with your last command. [Adding a theme](https://gohugo.io/getting-started/quick-start/)
4. Now you can change the the theme files and push them to your fork and the changes can be applied. You have now control over your(!) theme.

### Changes in the theme
If you change something in the theme and want to push your changes your need to go into your theme folder. [Submodules cloning](https://www.w3docs.com/snippets/git/how-to-pull-the-latest-git-submodule.html)
```
cd themes/my-theme
```
In here we have a seperate git and thereform need to add the changes in here.
```
git add .
git commit -m "theme changes"
git push origin main
```

### The theme as submodule was not loaded
After adding the submodule it can be possible that the files in the folder you specified is empty. This can also happen after cloning your repo. ThisYou than need to first look at your **.gitmodules** file in your folder and check if the URL to your theme repo is correct, if not change the URL.
In the next steps you are going to pull all code from your submodules:
```
git submodule init //to initialize your submodules
git submodule update
```
now all submodules you added should pull from their origins.