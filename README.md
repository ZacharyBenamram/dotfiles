# Danny Hermes `dotfiles`

## Prerequisites

In order to do this you'll need `git` installed. It should come by default
on macOS and Linux. If not, get a new version of your OS.

## `bash-it` Framework

As of February 2019, I'm using [`bash-it`][14] for many shell features I
used to "handroll". I use the powerline theme, which has some font issues in
VS Code and required installing [Menlo for Powerline][15] (I followed a
[blog post][15] to resolve the issue).

## Symlinks

After cloning this, create symlinks to all configuration files:

```console
$ python create_symlinks.py
Adding symlinks:
----------------------------------------------------------------------
...
```

You may need to create `~/.ssh` as well. You may also want to enable
`git is-child` and `annoy` via:

```console
ln -s $(pwd)/is-git-child.sh /usr/local/bin/is-git-child
ln -s $(pwd)/annoy.py /usr/local/bin/annoy
```

(or some directory on your `${PATH}` other than `/usr/local/bin`).

## GNU Screen

In order to track open GNU Screen windows, the `dotfiles/screen_sessions.json`
file is used. Populate it with the "initial" content

```json
{"SENTINEL": null}
```

## System Paths / Defaults

There are some paths on the system that define default behavior.

- On Ubuntu, `/etc/ssh/sshd_config` [can be modified][2] to force `ssh`
  login to **only** accept a public key. In particular, the line
  `PasswordAuthentication no` should be added (or a variant of it should
  be uncommented). After modifying this, run `restart ssh` or just reboot.
- On macOS, `/private/etc/ssh/sshd_config` [can be modified][8] to force `ssh`
  login to **only** accept a public key. In particular, the line
  `PasswordAuthentication no` should be added (or a variant of it should
  be uncommented). Also `ChallengeResponseAuthentication no` should be set.
  "If you are using a stock install (i.e., you didn't build/install it yourself
  from source), launchd should take care of picking up the new config without
  having to restart the daemon."

## VS Code

In order to use VS Code [settings][9] and keybindings, create symlinks
into the VS Code install directory. (Before creating the symlinks you'll
likely need to delete the existing JSON files.)

On macOS:

```console
ln -s \
  $(pwd)/vscode/settings.macos.json \
  "${HOME}/Library/Application Support/Code/User/settings.json"
ln -s \
  $(pwd)/vscode/keybindings.macos.json \
  "${HOME}/Library/Application Support/Code/User/keybindings.json"
```

On Ubuntu:

```console
ln -s \
  $(pwd)/vscode/settings.ubuntu.json \
  "${HOME}/.config/Code/User/settings.json"
ln -s \
  $(pwd)/vscode/keybindings.ubuntu.json \
  "${HOME}/.config/Code/User/keybindings.json"
```

Also note that you may need to install Roboto on Ubuntu (see
`editor.fontFamily`).

My current (as of January 2019) list of extensions is

```console
$ code --list-extensions
DotJoshJohnson.xml
eamodio.gitlens
esbenp.prettier-vscode
kaiwood.center-editor-window  // CTRL+L recenters editor on current line
ms-python.python
ms-vscode.cpptools
ms-vscode.Go
```

These can be installed on a new machine via
`code --install-extension ${EXTENSION}`. The actual state of these is kept
in `${CONFIG_DIR}/Code/CachedExtensions/user` (a JSON file) but that file is
too specific to be stored in version control. (For example, it tracks the
current version of VS Code.)

> **NOTE**: `${CONFIG_DIR}` is `${HOME}/Library/Application Support` on macOS
> and `${HOME}/.config` on Linux

## Optional

- Install VS Code (`code`)
- It's not uncommon for me to install the [Google Cloud SDK][1].
- For working with `node`, install [`nvm`][4]
- For working with `python`, install [`pyenv`][5] and sometimes also
  [`pyenv-virtualenv`][10]
- For working with `go`, install [`goenv`][6]
- For working with `ruby`, install [`rbenv`][7]
- I occasionally like to use LaTeX for typesetting, so sometimes will
  install it on a new machine. I will also sometimes install `pdftk`.

### macOS

- Often the default version of `emacs` is too old, so it may be
  worth trying to update
- It's always important to start by running
  `xcode-select --install` to make sure Developer Tools are installed
- install [Homebrew][3]
- Set custom command to lock screen ([ref][11])
- Make function (`FN`) keys be function keys ([ref][12])

### Linux

- The [`libsecret` library][13] can be used in a similar fashion as the macOS
  keychain

  ```ini
  [credential]
         helper = /usr/share/doc/git/contrib/credential/libsecret/git-credential-libsecret
  ```

[1]: https://cloud.google.com/sdk/install
[2]: https://www.linux.org/threads/how-to-force-ssh-login-via-public-key-authentication.8726/
[3]: https://brew.sh
[4]: https://github.com/creationix/nvm
[5]: https://github.com/pyenv/pyenv
[6]: https://github.com/syndbg/goenv
[7]: https://github.com/rbenv/rbenv
[8]: http://serverfault.com/a/86007
[9]: https://code.visualstudio.com/docs/getstarted/settings
[10]: https://github.com/pyenv/pyenv-virtualenv
[11]: https://maclovin.org/blog-native/2017/high-sierra-set-a-global-shortcut-to-lock-screen
[12]: https://support.apple.com/en-us/HT204436
[13]: https://askubuntu.com/a/959662/439339
[14]: https://github.com/Bash-it/bash-it
[15]: https://dev.to/mattstratton/making-powerline-work-in-visual-studio-code-terminal-1m7
[16]: https://github.com/abertsch/Menlo-for-Powerline
