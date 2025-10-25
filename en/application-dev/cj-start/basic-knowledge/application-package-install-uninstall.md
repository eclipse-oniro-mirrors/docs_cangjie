# Application Installation, Uninstallation, and Update Development Guide

This chapter introduces the installation and uninstallation process of application packages and two update methods.

## Application Package Installation and Uninstallation

Developers can install and uninstall applications using debugging commands. For installation commands, refer to [install](../../tools/cj-bm-tool.md#installation-command-install) in the bm tool. For uninstallation commands, refer to [uninstall](../../tools/cj-bm-tool.md#uninstallation-command-uninstall) in the bm tool. For details, see the [Compilation, Release, and Deployment Flowchart](./application-package-structure-stage.md#release-package-structure).

## Application Package Updates

For developers, updating an application package first requires modifying the `versionCode` field in the [app.json5 configuration file](./app-configuration-file.md#appjson5-configuration-file). After packaging with DevEco Studio, the update is released on the app market, following the same process as the initial release. For end users, after a new version is released, the application package can be updated through the following methods:

- Update via the app market: The app market notifies users of the new version, and users can upgrade the application through the app market (client) based on the notification.