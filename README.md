# usb-ssh-key

Making USB drives useful again.

## What?

Instructions for putting your encrypted SSH key on an encrypted USB drive.
Plus a script for conveniently loading the key.

## Why?

**For the purist pair programmer**  
You use pairing machines. You rotate pairs often. You use [git-duet].
But you use a shared key that's stored on the machine... oh the horror!
Be proud of your code, stick your real identity on it.
Use your own key from your slick USB drive.
Plug, load, unplug, pair, rotate, repeat.

**For the security conscious**  
Multi-factor authentication. Identification is provided with a combination of
different components; something the user knows and something the user possesses.
Only the correct combination of a USB drive and multiple passphrases (to decrypt
the drive and to decrypt the key) allows the key to be used.

Disclaimer: Use at your own risk. Host machine may not be safe.

## How?

### Format and encrypt the drive

### Add SSH key to drive

### Backups

## Credits

This repository is a fork of Tammer Saleh's popular blog post.
It's where I learned how to do this.

[git-duet]: https://github.com/git-duet/git-duet
[tsaleh]: http://tammersaleh.com/posts/building-an-encrypted-usb-drive-for-your-ssh-keys-in-os-x/
