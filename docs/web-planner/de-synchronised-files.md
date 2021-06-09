<!-- Space: WE -->
<!-- Parent: Web Documentation -->
<!-- Parent: Web Planner -->
<!-- Title: De-Synchronised Files -->
<!-- Layout: (plain) -->

# De-Synchronised Files

If you have got de-synchronized files this means that there are files on the live server which are not within git.

We should aim to get the git repo the master version of the website, giving us better chance for recovery.

You must either download these files and add them to Git, or mark them for deletion which will be done by tech periodically.

The de-synchronised files will display as follows:<br>
![De-Synchronized File](https://i.imgur.com/oGNWKRQ.png)

# Mark for Deletion
If you know for certain that the files on the live server are not needed anymore, mark these for deletion. To mark for deletion simple click on the checkbox to the right of the file. This will mark this file for deletion.

If you are unsure which files are needed, you should follow the next step for downloading the files and add them all into the git repo.

# Downloading

To download the files click the download link, this will take you to a download page on the website. (this is locked down to the office IP, so if working from home ensure your connected to the VPN)

With the downloaded files you can add these to the required folder locally and then run __gulp publish__ to get them into git.

When going to launch these new files you will see that the de-synchronized files will still show, this is because this gets processed on launch, so launching the website again will remove the ones that have been added.

*Note: if the files are marked for deletion these wont be downloaded*
