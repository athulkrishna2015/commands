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
To fix the error I ran the same steps as before:

```sudo rm -R /var/lib/pacman/sync
sudo pacman -Syy
```
and deleted the temporary files of pamac via

`
sudo rm -rf /tmp/pamac
`

Looks like your local signatures are expired and/or invalid and are preventing you from installing the keyring and gnupg packages.

It’s kind-of a catch-22: the local signatures need to be updated to function, but the signatures on the packages containing the required updates don’t match any valid local ones, and thus are prevented from installing.

The fix is simple, but a bit of a security risk. The signatures are there to protect you against MITM (man in the middle) attacks. However, in order to install the new signatures in your system’s current state, you’ll need to temporarily disable those checks.

(@Wollie , let us know if there’s a better way to do this, as I’d be interested in an alternative)

The 5 lines of code below should resolve the issue. They essentially do the following:

backup current pacman.conf
turn off all signature checks
download/install gnupg and keyring packages (ignore manjaro-system updates for now)
restore original pacman.conf settings (which turns signature checks back on)
update system
(If any of the below commands fail, please post the output here and do not continue.)
```
sudo cp -f "/etc/pacman.conf" "/etc/pacman.conf.orig"
sudo sed -i 's/SigLevel.*/SigLevel = Never/' /etc/pacman.conf
sudo pacman -Syy gnupg archlinux-keyring manjaro-keyring --ignore manjaro-system
sudo mv -f "/etc/pacman.conf.orig" "/etc/pacman.conf"
sudo pacman -Syu
```

(l)[https://forum.manjaro.org/t/root-tip-mitigate-and-prevent-gpgme-error-when-syncing-your-system/84700]

Open the file `/etc/pacman.conf` in a terminl editor (nano, micro, vi) and locate the following section

# By default, pacman accepts packages signed by keys that its local keyring
# trusts (see pacman-key and its man page), as well as unsigned packages.
SigLevel    = Required DatabaseOptional
LocalFileSigLevel = Optional
#RemoteFileSigLevel = Required
Change the SigLevel to

....
`SigLevel    = Required DatabaseNever`
....
Remove the files in /var/lib/pacman/sync - they will be fetched as necessary
```
sudo rm -f /var/lib/pacman/sync/*
```
Change mirror
```
sudo pacman-mirrors --continent
```
