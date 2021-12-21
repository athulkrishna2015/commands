error: GPGME error: No data
error: GPGME error: No data
error: GPGME error: No data
error: GPGME error: No data
error: failed to synchronize all databases (invalid or corrupted database (PGP signature))

```
sudo rm -R /var/lib/pacman/sync
sudo pacman -Syu
```
error: failed retrieving file 'core.db' from ftp.vectranet.pl : The requested URL returned error: 403
error: failed retrieving file 'extra.db' from ftp.vectranet.pl : The requested URL returned error: 403
error: failed retrieving file 'community.db' from ftp.vectranet.pl : The requested URL returned error: 403
warning: too many errors from ftp.vectranet.pl, skipping for the remainder of this transaction

```
sudo pacman-mirrors -f0 && sudo pacman -Syyu
```
