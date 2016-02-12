# usb-ssh-key

Making USB drives useful again.

## What?

Instructions for putting your encrypted SSH key on an encrypted USB drive.
Plus a script for conveniently loading the key.

## Why?

### For the purist pair programmer

You pair program. You use pairing machines. You rotate pairs often. You ping pong. You use [git-duet].

But you use a shared key that's stored on the machine... oh the horror!

Be proud of your code and brand it with your real identity.  
Just carry your slick USB drive with you.

Plug, load, unplug, pair, rotate, repeat, ???, profit.

### For the security conscious
<dl>
  <dt><strong>Multi-factor authentication</strong></dt>
  <dd>
    Identification is provided with a combination of different components;
    something the user knows and something the user possesses.
    Only the correct combination of a USB drive and multiple passphrases allows
    the key to be used.
  </dd>

  <dt><strong>SSH Agent</strong></dt>
  <dd>TODO</dd>

  <dt><strong>Encryption</strong></dt>
  <dd>Both the USB drive and SSH key are encrypted.</dd>

  <dt><strong>Timeouts</strong></dt>
  <dd>allows for a timeout to be set on the validity of keys. After a certain amount of time, you’ll need to type your passphrase again to unlock it.</dd>
</dl>



(extract)
For added security (for instance, against an attacker that can read any file on
the local filesystem), it is common to store the private key in an encrypted
form, where the encryption key is computed from a passphrase that the user has
memorized. Because typing the passphrase can be tedious, many users would prefer
to enter it just once per local login session. The most secure place to store
the unencrypted key is in program memory, and in Unix-like operating systems,
memory is normally associated with a process. A normal SSH client process cannot
be used to store the unencrypted key because SSH client processes only last the
duration of a remote login session. Therefore, users run a program called
ssh-agent that runs the duration of a local login session, stores unencrypted
keys in memory, and communicates with SSH clients using a Unix domain socket.

(clean)
In addition to multi-factor authentication, the script also uses an SSH Agent.
When a key is added to an agent, it's kept in memory and the agent issue signing operations to the programs in need

(extract)
The main advantage of the ssh-agent over the standard public key authentication is that all the magic happens in the ssh-agent process. The ssh process never has access to the key material, which makes it less vulnerable to memory content leaks (does that ring a bell ?). If you were using the SSH agent till today (with a passphrase), the OpenSSH client roaming bug did not impact your private keys.

(maybe)
The OpenSSH ssh-agent also has protection against tampering, making it hard for a hacker (without root access) to extract private keys from the cache, as most debugging interfaces will not be available.



Disclaimer: Use at your own risk. Host machine may not be safe.

## How?

### Format and encrypt the drive

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

### Add SSH key to drive

There is no way to recover a lost passphrase. If the passphrase is lost or
forgotten, a new key must be generated and the corresponding public key copied
to other machines.

### Optional extras

It's good to have a backup. The easiest way is to repeat the above steps for
another USB drive, but using the same key instead of creating a new one.
Store it in a safe place, like a safe or fireproof box.

For even more SSH tips, read https://blog.0xbadc0de.be/archives/300

## Credits

This repository is a fork of [Tammer Saleh's blog post][tsaleh].
It's where I learned how to do this.

[git-duet]: https://github.com/git-duet/git-duet
[kingston]: http://www.kingston.com/en/usb/personal_business
[tsaleh]: http://tammersaleh.com/posts/building-an-encrypted-usb-drive-for-your-ssh-keys-in-os-x/
