<!-- Space: WE -->
<!-- Parent: Web Documentation -->
<!-- Parent: Tech -->
<!-- Title: xdebug -->
<!-- Layout: (plain) -->

# xdebug

The steps below apply to any IDE, perform these first.

- Pull down repo with updates to Dockerfile etc...
- Update your `docker-compose.override` with the new values within the example.

If your running docker ensure to run `docker-compose up -d` again to apply these new settings.

<a name="phpstorm-specific"></a>
## PHPStorm Specific
1. Configure your Debug Configurations, simply click the dropdown highlighted below and click `Edit Configurations`.
2. Add a new `PHP Remote Debug` Configuration, name it anything, I named mine `xdebug`. Keep all the settings as the default and hit Apply.
3. Next we need to set up the CLI Interpreter. Open up your settings (File > Settings).
4. Now go to (Languages & Frameworks > PHP). [1]
    1. Click the 3 dots next to the CLI Interpreter dropdown. [2]
    2. Click the `+` button to add a new Interpreter. [1]
    3. Choose `From Docker...` from the dropdown list.
    4. Select the `Docker` radio button in this new window adn click `Ok`, leave all settings as default.
    5. Click `OK` within the CLI Interpreter dialog as these settings can remain default.
5. You will not be back to the main setting's dialog within your PHP section. Click the folder icon to the right of `Path Mappings`. [3]
    1. Click `+` [1] and select your **Project Route**, in my case it's `E:/code/click-web` [2], then for **Remote Path** enter `/var/www` [3], click `Ok`.
6. Click Apply and click the settings.
7. Last step is to configure a server, go to (Settings > Languages & Frameworks > PHP > Servers).
    1. Click the `+` to add a new server. [1]
    2. Name the server anything, I named it `xdebug`. [2]
    3. Enter the hostname you use to run locally on your current project. [3]
    4. Check the `Use path mappings` checkbox [4], then you will see your project route [5], to the right of that enter `/var/www`. [6]

<a name="visual-studio"></a>
## Visual Studio

<a name="browser-settings"></a>
## Browser Settings
If you are using chrome you can simply install [this helper](https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc?hl=en). But in essence this just adds a cookie: `XDEBUG_SESSION: XDEBUG_ECLIPSE`.

Ensure this cookie is set before you refresh the page.


![](/img/documentation/xdebug/1.png)
![](/img/documentation/xdebug/2.png)
![](/img/documentation/xdebug/3.png)
![](/img/documentation/xdebug/4.png)
![](/img/documentation/xdebug/6.png)
