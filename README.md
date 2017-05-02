# Simple Key Manager

Simple Key Manager (**SKM**) is a small shell script designed to simplify common
interactions with SSH keys.

## This project is no longer maintained.

Maintaining multiple keys is a lot of work for very little benefit: if the main
workstation is compromised, _all_ of the keys on that workstation are compromised,
so using multiple keys for a single identity (person, machine, workstation, etc) 
doesn't really provide any additional security benefits. The author recommends
using a single key, and automating as much as possible to reduce or remove the
need to ever connect directly to a remote host.

The following content represents the README prior to deprecation.

## Assumptions

By default, SKM makes a few assumptions about how your keys are stored. I'll
list these below:

### Key locations

1.  Both public and private keys are stored in `~/.ssh/keys`

### Key naming scheme

SKM was designed with the idea of "grouped" keys. Often times, I find myself
booting up one of my machines to ssh into few servers, or to work on a few
specific projects -- before shutting down again.

Because of this, SKM supports adding keys to the agent one at a time, in groups,
or all at once. "Groups" are created by naming your keyfiles with a common
prefix. Look to the table below for an example.

| Group Tag  | Example private name | Example public name |
| ---------- | -------------------- | ------------------- |
| vcs        | vcs.github           | vcs.github.pub      |
| mytag      | mytag.somekey        | mytag.somekey.pub   |

Note that you do not need to follow this naming scheme if you do not want to
take advantage of the grouping feature. You are free to name your keys whatever
you wish, and `skm add` will handle it properly.

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

| Command | Example Parameters                    | Description                     |
| ------- | ------------------------------------- | ------------------------------- |
| add     | all &#124; {group tags} &#124; {keys} | Adds keys to the agent          |
| disable | key1 key2 key3 ...                    | Disables keys                   |
| enable  | key1 key2 key3 ...                    | Enables keys                    |
| export  | key1 key2 key3 ...                    | Shows public key info           |
| ls      | none                                  | Lists active keys               |
| status  | none                                  | Shows the status of all keys    |
| clear   | none                                  | Clears the authentication agent |

## Example actions

| Command                                      | Explanation                                           |
| -------------------------------------------- | ----------------------------------------------------- |
| `$ skm add all`                              | Adds all keys in `~/.ssh/keys` to the agent           |
| `$ skm add tagA tagB.keyname`                | Adds all tags prefixed with `tagA` and `tagB.keyname` |
| `$ skm disable tagA.key1 tagA.key2`          | Disables `tagA.key1` and `tagA.key2`                  |
| `$ skm enable tagA.key2`                     | Enables `tagA.key2`                                   |
| `$ skm export tagB.key3 tagA.key2 tagC.key4` | Outputs the public key info for the specified keys    |

## Contributing

Please [create an issue][1] for any bugs, feature requests, or other comments.

Thank you for checking out my project! I hope it's helpful!

[1]: https://github.com/bddenhartog/simple-key-manager/issues
