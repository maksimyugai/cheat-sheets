## GPG

To generate new GPG key just execute following command:
```shell
gpg --full-generate-key # all further choices can be default 
# To list keys 
gpg --list-secret-keys 
# To export particular public key 
gpg --armor --export <key-id>
```