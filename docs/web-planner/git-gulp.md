<!-- Space: ~213834277 -->
<!-- Parent: Web Documentation -->
<!-- Parent: Web Planner -->
<!-- Title: Git-Gulp -->
<!-- Layout: (plain) -->

# ![gulp](https://upload.wikimedia.org/wikipedia/commons/thumb/7/72/Gulp.js_Logo.svg/60px-Gulp.js_Logo.svg.png) Git-Gulp

Ensure that you install the following versions
- npm: **6.9.0**
- node: **10**
- git: **2.18.0**
- gulp-cli: **2.0.1**


1. Node is the main engine for this package to function, please download the **LTS** version of node from [here](https://nodejs.org/en/download/).
2. Next you need to install gulp globally, simply run `npm install --global gulp-cli` within your command line.
3. You now need to download the gulp files from **git**, navigate to the folder you wish to store your files within and run the following command:

```
git pull https://git.clickdealer.tech/clickdealer/webteam/websites.git
```
If successful you will see the following message:
```
? git clone https://git.clickdealer.tech/clickdealer/webteam/websites.git
Cloning into 'websites'...
remote: Enumerating objects: 239, done.
remote: Counting objects: 100% (239/239), done.
remote: Compressing objects: 100% (93/93), done.
remote: Total 239 (delta 150), reused 219 (delta 139)
Receiving objects: 100% (239/239), 118.16 KiB | 7.88 MiB/s, done.
Resolving deltas: 100% (150/150), done.
```
4. Install all the packages by opening *websites* folder within your command line, and then running `npm install`.
5. Now you need to set up your config, to do this copy the `config.json.example` file from within the `websites` which you just created. Rename this copied file to `config.json` and update the `username` to yours, this is usually the initials from your work email.
6. You will need to generate your SSH key for file upload authorization. Run `ssh-keygen -m PEM -t rsa -b 2048 -C "<your_email_address>"` within a terminal window. Obviously replace `your_email_address` with your work email. When prompted for the following simply press enter and leave them blank: `Enter file in which to save the key`, `Enter passphrase` x2.
7. Finally, we need to send your public SSH key to Shane/Martyn, this needs adding to the server before you have authorization to upload files, to copy this run the command below, the SSH Public Key will then be in your clipboard so paste within an email or chat to Martyn/Shane.

Mac: `pbcopy < ~/.ssh/id_rsa.pub`

Windows: `type %HOMEDRIVE%%HOMEPATH%\.ssh\id_rsa | clip`

**Your ready to go, below we have listed the commands you may use, any questions please contact Shane/Martyn**

# Basic Usage

If the **--theme** over-ride is displayed in the command below then it is **REQUIRED** for that command.

Below are the commands you can use, run `gulp` to see a list of these commands within the command line.

### `gulp get --theme _themev2-name-1234`:

This command will fetch a dealers theme from git and initialize it on your machine, once downloaded all you need to do then is to `cd` into this folder, and run the command below.

When the folder is downloaded the demo files will be removed and re-uploaded to keep demo in sync with what has been committed within git.

### `gulp watch`:

Start to watch for any file changes and handle accordingly. Gulp will watch all Less, Images and JavaScript and compile/compress, gulp will also watch for any file changes and upload when detected to the demo server.

### `gulp publish`:

This command will add, commit and push all changes to git, this is how you can your files onto the staging server ready to launch, run this when you are finished.

### `gulp reset`:

Made a mistake or need to clear all changes made? Simply run this command and any changes you have made will be deleted, and the theme will be restored what is currently on git, which should be identical to the staging server.

### `gulp new --theme _themev2-name-1234`:

Creating a new website? This is the command for you! This command will create your skelton theme folder, add, commit and push to git ready. Once completed just `cd` into the folder and run `gulp watch` to start working.


# Updating packages

To update simply run `npm install` for now, this will update all of your packages.

# Updating Gulp

To update your gulp please ensure to `cd` into the **websites** directory, then run `git pull`.

# Note
Do not modify files **not** within the `themes` directory.

Modifying any files not within the `themes` directory may result in undesired results, this could include global data loss.

Any detected un-authorised modifications will be reported.

The only file's you can modify outside of the `themes` directory are the following:
- config.json
- .gulp.json
