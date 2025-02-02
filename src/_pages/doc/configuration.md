---
title: Configuration
permalink: /doc/configuration/
sidebar: doc
---
{% include vars.html %}

## About

Each portable application can be configured through a simple [YAML](https://en.wikipedia.org/wiki/YAML){:target="_blank"} configuration file named `[appname]-portable.yml`.

This file is generated at first launch as a sample file named `[appname]-portable.sample.yml`. Rename this file `[appname]-portable.yml` and it would be used at runtime. It contains all the fields available to configure the application. Here is an example with [Firefox](/app/firefox-portable/) :

![](/img/faq/sample-configuration-file.png)

```yml
common:
  args: []
  env: {}
  app_path: ""
app:
  profile: default
  multiple_instances: false
  disable_telemetry: false
  disable_firefox_studies: false
```

Two main fields are to be taken into account :

### Common

This field is _common_ for all applications available in the Portapps catalogue.

* **args** : Pass additional arguments to the process.
* **env** : Add environment variables as a key/value list. Placeholders for values can be used and will be replaced with the relevant data :
  * **@ROOT_PATH@** : Root path of the portable app
  * **@APP_PATH@** : Application binaries path
  * **@DATA_PATH@** : Data path
  * **@DRIVE_LETTER@** : Current drive letter
* **app_path** : Application binaries path. If the application is on a network drive you have to set an UNC path like `\\?\MYSERVER\firefox-portable\app`.

{% include callout.html type="warning" title="About app_path" text="Be careful if you use `app_path` because the wrapper is closely linked to the version of the application used. Use ONLY if you know what you are doing." %}

Here is an example :

```yml
common:
  args:
    - --debug
    - --key=value
  env:
    ENV_VAR_KEY: env_var_value
    ANOTHER: true
    A_PLACEHOLDER: "@ROOT_PATH@\\subfolder"
  app_path: C:\portapps\firefox-portable\app
```

### App

This field is specific to each application and does not exist by default. It's up to the developer to set up the configuration.

```yml
app:
  ...
```