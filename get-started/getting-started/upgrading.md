---
description: This document covers upgrading the PowerShell Universal application.
---

# Upgrading

## General

The Universal application binaries can generally be upgraded without having to change the configuration or database manually. This document will cover how to upgrade the application and some caveats to be aware of in regards to configuration and data persistence.

### Data Persistence

Data is persisted in a LiteDB database with a default location of `%ProgramData%\UniversalAutomation\database.db`. The database will not be deleted during an upgrade of any kind. Any schema updates to the database will happen the first time you start up the new version of Universal. You may wish to backup your database before performing an upgrade.

### Configuration Persistence

Configuration files are stored by default in `%ProgramData%\UniversalAutomation`. Configuration files may be updated or transformed during an update. This will happen the first time that the new version of Universal server is started. You may wish to backup your configuration files before performing an upgrade.

If you are using git, changes to the Universal files will be synchronized after the server starts up.

#### appsettings.json

The `appsettings.json` file that is included in the application installation directory will be overwritten during upgrades. To avoid losing your settings in this file, consider installing it into the `%ProgramData%\PowerShellUniversal` folder. Universal will look at this folder first for [configuration settings. ](../../config/settings.md#programdata-appsettings-json)

#### web.config

The `web.config` file that is included in the application installation directory will be overwritten during upgrades. If you have moved your web.config file to an alternate location, it will not be overwritten. When creating an IIS website, you can simply include the `web.config` file in the web app's directory and have the [binaries stored in a different location](../../config/hosting/hosting-iis.md).

#### Dashboard Components and Frameworks

New versions of Universal may include new versions of Universal Dashboard Frameworks or Components. By default, these components and frameworks are deployed to `%ProgramData%\PowerShellUniversal` during startup of the Universal server. During an upgrade, these files are not deleted. This ensures that dashboards will continue to run on the previous dashboard framework and component versions.

You should have multiple versions of the dashboard frameworks and components available when you start the new version of Universal.

By default, new dashboards are set to always use the latest version of the dashboard framework. You can chose to set it to a specific version if you would like but will have to manually change the version during an upgrade.

**Repository**

Most of the settings for PowerShell Universal are stored within the repository folder. By default, this is in `%ProgramData%\UniversalAutomation\Repository`. While the upgrade should not affect these files, you may want to backup the files before upgrading.

## ZIP Upgrade

{% hint style="info" %}
Always ensure to run `Unblock-File` on Windows to unblock all the files extracted the ZIP. If you do not, PowerShell Universal will not function properly.
{% endhint %}

When upgrading an manual ZIP file installation, you will need to stop the application, delete the entire binary folder and replace it with the new binary folder. When you start the new version of Universal, new dashboard frameworks and components will be deployed and the existing database will be loaded.

## MSI Upgrade

To upgrade using the MSI, you can simply run the new version of the MSI. The MSI is setup to always perform a major upgrade. This means it will stop and remove the service, delete the entire installation directory, reinstall with the new files and then install and start the new service.

You will want to follow the guide on data and configuration persistence above to ensure all your settings are saved.

{% hint style="warning" %}
If you have configured a service account for your MSI installation, you will need to set the service account after upgrading.
{% endhint %}

## IIS Upgrade

When upgrading with IIS, you will need to first stop your application pool to ensure that the binaries used by IIS are no longer in use and then replace the binaries with the new ones. Ensure that you follow the configuration persistence recommendations above with regards to the `web.config` file.

## LiteDB v5 Upgrade

PowerShell Universal uses LiteDB to store jobs, app tokens, identities and git sync history. The original version of LiteDB included with PSU is version 4. We will be moving to version 5 in a future version. We have added version 5 support but are not yet upgrading users databases. You can choose to upgrade your database to version 5 by adjusting your connection string to perform an upgrade on the database. We suggest backing up your database file before doing so.

In `appsettings.json`, you will need to change the database type to `LiteDBv5` and add the upgrade parameter to the connection string.

```javascript
    "Data": {
    "RepositoryPath": "%ProgramData%\\UniversalAutomation\\Repository",
    "ConnectionString": "filename=%ProgramData%\\UniversalAutomation\\database.db;upgrade=true",
    "DatabaseType": "LiteDBv5",
```

