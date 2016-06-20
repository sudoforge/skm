# Simple Key Manager

Simple Key Manager (**SKM**) is a small shell script designed to simplify common
interactions with SSH keys.

## Assumptions

By default, SKM makes a few assumptions about how your keys are stored. I'll
list these below:

### Key locations

1.  Both public and private keys are stored in `~/.ssh/keys`

### Key naming scheme

SKM was designed with the idea of "grouped" keys. Often times, I find myself
booting up one of my machines to ssh into a single server, or to work on a
single particular project -- before shutting down again.

Because of this, SKM supports adding single keys, groups of keys, or all keys at
once. Follow the naming scheme below to set up your groups correctly.

_Support for custom groups is planned for the future._

| Usage      | Example usage           | Example private name | Example public name |
| ---------- | ----------------------- | -------------------- | ------------------- |
| VCS        | Github, Bitbucket, etc. | vcs.github           | vcs.github.pub      |
| Operations | SSHing into a server    | ops.myserver         | ops.myserver.pub    |

## Installation

```bash
git clone https://github.com/bddenhartog/simple-key-manager

cd simple-key-manager

chmod u+x skm

ln -sf $(pwd)/skm /usr/bin/skm
```

_You can replace /usr/bin in the last command with any directory in your PATH._

## Usage

Now on to the easy bit. Review the table below and you're good to go!

| Command          | Description                                          |
| ---------------- | ---------------------------------------------------- |
| all              | Uses `ssh-add` to add all keys                       |
| vcs              | Uses `ssh-add` to add all keys prefixed with `vcs.`  |
| ops              | Uses `ssh-add` to add all keys prefixed with `ops.`  |
| ls               | Lists all currently active keys                      |
| status           | Like `skm ls`, but shows the status of all keys      |
| clear            | Deletes all identities from the authentication agent |
| disable {key(s)} | Disables any number of keys                          |
| enable {key(s)}  | Enables any number of keys                           |
| export {key(s)}  | Shows the public key for any number of keys          |

## Contributing

Please [create an issue][1] for any bugs, feature requests, or other comments.

Thank you for checking out my project! I hope it's helpful!

[1]: https://github.com/bddenhartog/simple-key-manager/issues
