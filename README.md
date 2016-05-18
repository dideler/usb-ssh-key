# usb-ssh-key

Making USB drives useful again.

## What?

Instructions for putting your encrypted SSH key on an encrypted USB drive.  
Plus a script for conveniently loading the key.

## How?

[Put your SSH key on a USB drive](#create-your-own-usb-ssh-key), then

1. Insert USB and load SSH key

  ```shell
  /Volumes/keys/load  # Loads the key for 10 hours then force ejects
  ```
1. Unplug USB drive

Repeat steps 1-2 when key expires.

## Why?

### Pair programming

Pairs can benefit from using SSH keys on USB drives in their workflow.

Pairing machines should not store any personal state on them.  
Loading a key from USB lets you treat pairing machines as shared temporary devices.  
[*Treat your pairing machines as cattle, not pets*][cattle]

If you rotate pairs often, it's not recommended you load your own key whenever you drive.
Load one of your keys at the start of the pairing session and use [git-duet].
It allows a commit to have a different author and committer.

### Security

#### Multi-factor authentication

Identification is provided with a combination of different components;
something the user knows and something the user possesses.
Only the correct combination of a USB drive and passphrases allows the key to be used.

#### Encryption

Both the USB drive and SSH key are encrypted.

This means you'll have to decrypt the drive with a passphrase, and then decrypt the key with a passphrase.

#### SSH Agent

The script interacts with your key via an SSH Agent*.
This means you don't need to repeat the tedious step of typing a passphrase whenever you use the key.
Instead you type it once per login session.

The most secure place to store the unencrypted key is in program memory.
The key is stored in the memory associated with the ssh-agent process, which runs the duration of a local
login session. The ssh-agent handles communication for any signing operations.

When you decrypt the private key The key is stored in memory

When a key is added to an agent, it's kept in memory and the agent issue signing operations to the programs in need

The main advantage of an ssh-agent over the standard public key authentication is that all the magic happens in the ssh-agent process.
The ssh process never has access to the key material, which makes it less vulnerable to memory content leaks.

The OpenSSH ssh-agent also has protection against tampering, making it hard for a hacker (without root access)
to extract private keys from the cache, as most debugging interfaces will not be available.

(extract)
A normal SSH client process cannot
be used to store the unencrypted key because SSH client processes only last the
duration of a remote login session. Therefore, users run a program called
ssh-agent that runs the duration of a local login session, stores unencrypted
keys in memory, and communicates with SSH clients using a Unix domain socket.

<sup>* An SSH Agent will need to be pre-installed on the machine.</sup>


#### Timeouts

allows for a timeout to be set on the validity of keys. After a certain amount of time, you’ll need to type your passphrase again to unlock it.


Disclaimer: Use at your own risk. Host machine may not be safe.

## Create your own USB SSH key

### Mac OS X

#### 1. Format and encrypt the drive

Find a suitable USB drive. I'm fond of the sleek
[Kingston DataTraveler drives][kingston] with metal casing,
like the SE9, GE9, Micro 3.1, or SE9 G2 3.0. These are stylish, capless, and
thin, with a large ring so they will attach easily to your keychain.

You can use your existing key, but it's recommended you create a new key.
If you're feeling extra adventurous, you can have a different key per service.

TODO: add passphrase if missing (or create new key)
```bash
ssh-keygen -p -f ~/.ssh/id_rsa
```

#### 2. Add SSH key to drive

There is no way to recover a lost passphrase. If the passphrase is lost or
forgotten, a new key must be generated and the corresponding public key copied
to other machines.

### Ubuntu Linux

TODO

### Extras (optional)

It's good to have a backup. The easiest way is to repeat the above steps for
another USB drive, using the same key instead of creating a new one.
Store it in a safe place, like a safe or fireproof box.

For even more SSH tips, read https://blog.0xbadc0de.be/archives/300

## Credits

This repository is a fork of [Tammer Saleh's blog post][tsaleh].

[cattle]: http://webcache.googleusercontent.com/search?q=cache:VwaEoCsPugAJ:blog.doismellburning.co.uk/treat-your-servers-like-cattle-not-like-pets&num=1&hl=en&gl=uk&strip=1&vwsrc=0
[git-duet]: https://github.com/git-duet/git-duet
[kingston]: http://www.kingston.com/en/usb/personal_business
[tsaleh]: http://tammersaleh.com/posts/building-an-encrypted-usb-drive-for-your-ssh-keys-in-os-x/
