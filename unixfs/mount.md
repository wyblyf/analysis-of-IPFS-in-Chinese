```
wayne@wayne:~/ipfs/unixfs$ ipfs mount --help
USAGE
  ipfs mount - Mounts IPFS to the filesystem (read-only).

SYNOPSIS
  ipfs mount [--ipfs-path=<ipfs-path> | -f] [--ipns-path=<ipns-path> | -n]

OPTIONS

  -f, --ipfs-path string - The path where IPFS should be mounted.
  -n, --ipns-path string - The path where IPNS should be mounted.

DESCRIPTION

  Mount IPFS at a read-only mountpoint on the OS. The default, /ipfs and /ipns,
  are set in the configuration file, but can be overriden by the options.
  All IPFS objects will be accessible under this directory. Note that the
  root will not be listable, as it is virtual. Access known paths directly.

  You may have to create /ipfs and /ipns before using 'ipfs mount':

  > sudo mkdir /ipfs /ipns
  > sudo chown $(whoami) /ipfs /ipns
  > ipfs daemon &
  > ipfs mount

  Example:

  # setup
  > mkdir foo
  > echo "baz" > foo/bar
  > ipfs add -r foo
  added QmWLdkp93sNxGRjnFHPaYg8tCQ35NBY3XPn6KiETd3Z4WR foo/bar
  added QmSh5e7S6fdcu75LAbXNZAFY2nGyZUJXyLCJDvn2zRkWyC foo
  > ipfs ls QmSh5e7S6fdcu75LAbXNZAFY2nGyZUJXyLCJDvn2zRkWyC
  QmWLdkp93sNxGRjnFHPaYg8tCQ35NBY3XPn6KiETd3Z4WR 12 bar
  > ipfs cat QmWLdkp93sNxGRjnFHPaYg8tCQ35NBY3XPn6KiETd3Z4WR
  baz

  # mount
  > ipfs daemon &
  > ipfs mount
  IPFS mounted at: /ipfs
  IPNS mounted at: /ipns
  > cd /ipfs/QmSh5e7S6fdcu75LAbXNZAFY2nGyZUJXyLCJDvn2zRkWyC
  > ls
  bar
  > cat bar
  baz
  > cat /ipfs/QmSh5e7S6fdcu75LAbXNZAFY2nGyZUJXyLCJDvn2zRkWyC/bar
  baz
  > cat /ipfs/QmWLdkp93sNxGRjnFHPaYg8tCQ35NBY3XPn6KiETd3Z4WR
  baz
  ```