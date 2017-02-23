# Deploying apps

## Deployment overview

The `cf push` command is used both to create a new app and to push a new version of an existing one. The basic steps:

1. Put the code you want to deploy in a directory. This is usually accomplished by checking it out of version control.

1. Target the appropriate organisation and space.

    ```
    cf target -o SOMEORG -s SOMESPACE
    ```

1. Deploy the application by running:

    ```
    cf push APPNAME
    ```

    from the directory which contains the code and configuration files for your app.

The app should now be live at `https://APPNAME.cloudapps.digital`.

There are many options available when you ``push`` an app. You can optionally set them in a ``manifest.yml`` file in the directory from which you are running the ``push`` command. See the Cloud Foundry documentation on [Deploying with Application Manifests](http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html) [external link] for details.

For a production app, you should run at least two instances to ensure availability.

After deployment, you can increase the running instances to two using:

``cf scale APPNAME -i 2``

### Caveats
* Your app should not write to local storage. Cloud Foundry local storage is ephemeral and can be deleted at any time.
* You may need to set environment variables for your app to work. All configuration information should be stored in environment variables, not in the code. 
* Instances will be restarted if they [exceed memory limits](/#quotas).
* Your application should write all its log messages to `STDOUT`/`STDERR`, rather than a log file.
