# Server Configuration

The configuration of the software is done in the client and [campaign settings](/docs/dm/settings/).
While you actually could modify the configuration stored in the save file (see below), it is not recommended and, thus, not documented, here.
In contrast, this section focuses on the configuration that should be done within the central configuration file, which is `./server/server_config.cfg`.

The configuration file is divided up into two sections: Webserver, and General.
These sections are indicated by these designations, within square brackets (e.g. `[Webserver]`).
Within each section, there are certain variables defined via a name and their value, using the scheme `name = value`, followed by a line-break.
A leading `#` denotes a comment; every line with a leading `#` will be ignored.

Only change the configuration if something does not work accordingly and you know what you're doing.

## Webserver

This section contains several variables concerning the webserver that distributes the client to the players.

### host
`host` (default: `0.0.0.0`, accepting strings resolveable by *DNS*) tells the server on what (IP-) address it is reachable.
The default is set to `0.0.0.0` which, in this context, means: 'Any IP on this machine'.

Most likeley, you won't need to change this setting, unless you're sharing the machine with others (e.g. on a shared (v)server) or run several servers on the machine with different addresses.

### port
`port` (default: `8000`, accepting numbers from 1 to 2^16 -1) tells the server on which port to listen.
PlanarAlly uses port `8000` by default.
You can freely adjust this setting according to your server's setup and will need to, if another application already listens on `8000`).

Be sure that the port you use is not used by any other application.
Also, make sure the port you use is also accessible from outside of the machine.
Especially when running from within a private network (e.g. at home) you might need to enable *port forwarding* in your router's configuration.

This configuration key will not be used, when `socket` is used, i.e. the `#` before `socket` is removed.

### socket
`socket` (default: `/tmp/planarally.sock`, accepting filepath) tells the server where to look for an internal endpoint for communications with the network/internet.
This is an alternative to communicating via port.
Most likely, you will need this in the context of reverse proxies.

`socket` is inactive (i.e. commented off) by default.
If you activate the configuration-key by removing the leading `#`, sockets, regardless of `socket`'s value, will be used instead of `port`.

### Secure Sockets Layer (SSL)
PlanarAlly supports to encrypt communication in between the server and the players via [Secure Sockets Layer (SSL)](https://en.wikipedia.org/wiki/Transport_Layer_Security).
Despite the name, this is independent from the *socket* configuration, above.
The SSL-configuration needs three variables to be configured: `ssl`, `ssl_fullchain`, and `ssl_privkey`.

`ssl` (default: `false`, accepting true/false) tells the server whether SSL should be used.
If set to `false` (default), the other two settings will simply be ignored as they are not needed by the server.
**Despite it is set to false by default, it is highly recommended to use transport encryption.**

`ssl_fullchain` (default: `cert/fullchain.pem`, accepting filepath) tells the server where to look for the `*.pem`-file containing the certificate containing the 'full chain' of certificates to your certificate authority (CA).
Please note that neither the folder `cert`, nor the file `fullchain.pem` are shipped with PlanarAlly, but have to be generated/referred to for each individual installation by yourself.

`ssl_privkey`(default: `cert/privkey.pem`, accepting filepath) tells the server where to look for the `*.pem`-file containing your private certification key.
Please note that neither the folder `cert`, nor the file `privkey.pem` are shipped with PlanarAlly, but have to be generated/referred to for each individual installation by yourself.
**Please also take the 'private' in 'private key' *very* seriously!**

### Cross Origin Resource Sharing (CORS)
PlanarAlly supports Cross Origin Resource Sharing.
This functionality is deactivated by default and only accepts resources from the same origin.

`cors_allowed_origins` (inactive by default, default: `['*']`, accepting `['*']`, `['example.org', 'example.com']`, and `[]`) tells the server which hosts are eligible for CORS.
If it is not specified (default), only requests to the host running the server are allowed.
See [python-socketio on readthedocs.io](https://python-socketio.readthedocs.io/en/latest/api.html#asyncserver-class) for more information on the meaning of the allowed values.

## General

This section contains general settings for PlanarAlly.

### save\_file

`save_file` (active by default, default: `planar.sqlite`) tells the server where to look for the central save file wherein all users, settings, locations, assets and so on are saved.

:::info Savefile format
Note that, at this moment, PlanarAlly only supports storing the saves in *.sqlite* format.
:::

### public\_name

`public_name` (inactive default, accepting valid ip or hostname) is used to set an ip or hostname address that is inserted into the invitation url via the [DM's campaign settings](/docs/dm/settings/#invitation-url).
If inactive or empty, the server falls back to normal operation and uses the ip/hostname address it is accessed with.

## APIserver

The API server is an administration server on which some API calls can be made.
This contains the same options as the settings of the [configuration of the webserver](#Webserver), but applying them to the API server.

Thus, only major differences are listed here:
* **Always** use a different port or socket than for the webserver.
* `host` is defaulted to `localhost` instead of `0.0.0.0` to limit access.
* `port` is defaulted to `8001` (using the port next to the webserver's default).
