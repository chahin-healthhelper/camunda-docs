---
id: flags
title: Flags
description: "Flags allow you to control the availability of certain features within Desktop Modeler."
---

import Tabs from "@theme/Tabs";
import TabItem from "@theme/TabItem";

Flags allow you to control the availability of certain features within Desktop Modeler.

## Configuring Flags

You may configure flags in a `flags.json` file or pass them via CLI.

### Configure in `flags.json`

Place a `flags.json` file inside the `resources` folder of your local [`{USER_DATA}`](../search-paths#user-data-directory) or [`{APP_DATA_DIRECTORY}`](../search-paths#app-data-directory) directory to persist them.

### Configure via CLI

Pass flags via the command line when starting the application.

<Tabs groupId="os" defaultValue="windows" queryString values={
[
{label: 'Windows', value: 'windows' },
{label: 'macOS', value: 'macos' },
{label: 'Linux', value: 'linux' }
]
}>

<TabItem value='windows'>

```plain
"Camunda Modeler.exe" --disable-plugins
```

</TabItem>

<TabItem value='macos'>

```plain
camunda-modeler --disable-plugins
```

</TabItem>

<TabItem value='linux'>

```plain
camunda-modeler --disable-plugins
```

</TabItem>
</Tabs>

Flags passed as command line arguments take precedence over those configured via a configuration file.

## Available Flags

| flag                                               | default value                       |
| -------------------------------------------------- | ----------------------------------- |
| ["disable-plugins"](#disable-plug-ins)             | false                               |
| "disable-adjust-origin"                            | false                               |
| "disable-cmmn"                                     | true                                |
| "disable-dmn"                                      | false                               |
| "disable-form"                                     | false                               |
| "disable-platform"                                 | false                               |
| "disable-zeebe"                                    | false                               |
| "disable-remote-interaction"                       | false                               |
| "single-instance"                                  | false                               |
| "user-data-dir"                                    | [Electron default](../search-paths) |
| ["display-version"](#custom-display-version-label) | `undefined`                         |
| ["zeebe-ssl-certificate"](#zeebe-ssl-certificate)  | `undefined`                         |

## Examples

### Disable Plug-ins

Start the modeler without activating installed plug-ins. This is useful to debug modeler errors.

### BPMN-only Mode

To disable the DMN and Form editing capabilities of the App, configure your `flags.json` like this:

```js
{
    "disable-dmn": true,
    "disable-form": true
}
```

As a result, the app will only allow users to model BPMN diagrams.

![BPMN only mode](./img/bpmn-only.png)

### Custom `display-version` label

To display a custom version information in the status bar of the app, configure your `flags.json` like this:

```js
{
    "display-version": "1.2.3"
}
```

![Custom version info](./img/display-version.png)

### Zeebe SSL certificate

> :information_source: The Modeler will read trusted certificates from your operating system's trust store.

Provide additional certificates to validate secured connections to a Camunda 8 installation.

Configure your `flags.json` like this:

```js
{
    "zeebe-ssl-certificate": "C:\\path\\to\\certs\\trusted-custom-roots.pem"
}
```

Additional information adapted from the [upstream documentation](https://nodejs.org/docs/latest/api/tls.html#tlscreatesecurecontextoptions):

> The peer (Camunda 8) certificate must be chainable to a CA trusted by the app for the connection to be authenticated. When using certificates that are not chainable to a well-known CA, the certificate's CA must be explicitly specified as trusted or the connection will fail to authenticate. If the peer uses a certificate that doesn't match or chain to one of the default CAs, provide a CA certificate that the peer's certificate can match or chain to. For self-signed certificates, the certificate is its own CA, and must be provided.
