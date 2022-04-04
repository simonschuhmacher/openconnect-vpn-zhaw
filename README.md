# Convenience script to connect to AnyConnect VPN server at ZHAW via OpenConnect

This script allows to connect to a AnyConnect VPN server using SSO for authentication via command line. Tested on macOS, probably working as well for Linux with some minor modifications.

The following tools need to be installed to use the script.


## Install OpenConnect

```shell
brew install openconnect
```


## Install OpenConnect-SSO

### Install pipx

Optional, but recommended, see [https://github.com/pypa/pipx](https://github.com/pypa/pipx).

```shell
pip3 install --user pipx
```


### OpenConnect-SSO

```shell
pipx install "openconnect-sso[full]"
```

once finished installation, run

```shell
pipx ensurepath
```


## Connect manually to server

To save the password to keychain, run the `openconnect-sso` command once manually (**yourname needs to be changed to your name / abbreviation**):

```shell
sudo openconnect-sso --server "ras.zhaw.ch" --user="yourname@students.zhaw.ch"
```

Log in in the web view showing up. Password will then automatically be saved to keychain.


## Modify script

Modify the script found in this repo called `vpnzhaw` with your information, namely your email address, by setting the correct value for the variable `VPN_USER` correctly (replace `yourname`):

```shell
VPN_USER="yourname@students.zhaw.ch"
```


Make the script executable:

```shell
chmod +x vpnzhaw
```


Place the modified script at `usr/local/bin/`


## Allow to run the script without sudo (optional)

The script needs root permission to work properly.
To allow executing it with sudo without entering a password, add the file `/private/etc/sudoers.d/vpnzhaw`, for example using nano:

```shell
sudo nano "/private/etc/sudoers.d/vpnzhaw"
```

and paste the following to the file

```shell
yourmacusername ALL=(ALL) NOPASSWD: /usr/local/bin/vpnzhaw
```

replace *yourmacusername* with your actual username. To get this, run `whoami` in terminal.

(If using nano, save with `CTRL+o` and exit with `CTRL+x`)


## Using the script

Installation should now be finished. Use the script with the following commands:

- `vpnzhaw start` to start a new connection to the VPN server. If not yet connected, just executing `vpnzhaw` will start a new connection as well.
- `vpnzhaw status` to show whether OpenConnect is currently running. If OpenConnect is currently running, just executing `vpnzhaw` will show the status as well.
- `vpnzhaw stop` to close the existing connection.


Enjoy 😚




