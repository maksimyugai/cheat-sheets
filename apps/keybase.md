# Importing pgp keys from keybase into gpg
This can be useful for a number of things including singing git commits which uses gpg.

If you don't have gpg already installed, you can install it with most package managers on unix systems, on macos you can brew install gpg.

Assuming you have published your public and private keys, simply install gpg, and then you can import them directly.

### Import the public key
```shell
$ keybase pgp export | gpg --import
```

### Import the private key
```shell
$ keybase pgp export -s | gpg --allow-secret-key-import --import
```
During the second command, you may be asked by keybase to authenticate and create a passphrase for the key. Read these carefully and make sure to store your passwords using a password manager.

Note: The above example shows you how to import a private key from the keybase servers, this is definetely something you need to think about before doing it. Do not upload your private key to the keybase servers unless you have a really good reason and have thought through the risks. Your private key is meant to be kept private from EVERYONE.

### Exporting gpg keys
Now you've imported your pgp keys into gpg, you can now export them in the gpg format for use in things like git. This is the main reason people try to use keybase and gpg together.

You'll probably want to export your gpg public key and upload it to something like github or gitlab. You may also wish to distribute this to people so they can verify the tags of your git repository.

### Export the gpg key from gpg
```shell
$ gpg --armor --export youremail@email.com
```
Simply replace youremail@email.com with the email address attached to your key. If you can't remember what email address is attached to your public key, you can list all your gpg keys with gpg --list-keys.

You can now attach this to your github, gitlab, or preferred git remote host which will automatically verify either commits or tags. You can also distribute this as desired to others for verification purposes.

### Pushing key updates from gpg to keybase
If you've made some changes to your keys, perhaps added an email address, or changed the expiration date, you'll want to take your keys from gpg and push them back up to keybase. This can be done really easily.

### Tell keybase to fetch your key from GPG and update it on keybase
```shell
$ keybase pgp update
```
Pulling key updates from keybase into gpg
Alternatively, you may wish to pull updates from keybase into gpg. For this purpose, you can do the same step as we used to import the key.

```shell
$ keybase pgp export | gpg --import
```
Troubleshooting
If you're getting the following error, you might not have told GPG what TTY to use to ask for a passphrase.

```shell
error: gpg failed to sign the data
error: unable to sign the tag
```
This can be fixed in a few ways, first you can tell GPG to use the current TTY via:

```shell
$ export GPG_TTY=$(tty)
```
Or, a more popular option is to install pinentry via brew install pinentry.

#### Source: https://www.elliotblackburn.com/importing-pgp-keys-from-keybase-into-gpg/