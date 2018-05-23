Usync
=====


Overview
--------

Usync is a simple site-to-site synchronization program written in [Scsh](http://www.scsh.net). It makes
use of [unison](http://www.cis.upenn.edu/~bcpierce/unison/), and [rsync](https://rsync.samba.org/),
for bi- and uni-directional synchronizations, respectively.


Prerequisites
-------------

- scsh ≥ 0.7
- rsync ≥ 3.1
- unison ≥ 2.48


Installation
------------

If you’re using Nix, run:

    $ nix-env -i usync

or

    $ nix-env -iA $(nix-channel --list | awk '{print $1}').usync

If that doesn’t work, or if you’re not using Nix, do the following.

To install it to the current user:

    $ mkdir -p ~/bin
    $ curl -SLo ~/bin/usync https://raw.githubusercontent.com/ebzzry/usync/master/usync
    $ chmod +x ~/bin/usync

To install it globally:

    # curl -SLo /usr/local/bin/usync https://raw.githubusercontent.com/ebzzry/usync/master/usync
    # chmod +x /usr/local/bin/usync


Usage
-----

To perform two-way synchronization of the directory `/pub/yot/ninam`, between the current host, to
the hosts `tarupam`, and `taubetmo`, while preserving the directory structure remotely (take note,
that there must be no spaces between the hosts specification, due to the IFS environment variable,
found in most shells):

    $ usync /pub/yot/ninam/ tarupam,taubetmo

The command above will perform two-way synchronization of the diretory `ninam/` found under
`/pub/yot/`, to `tarupam:/pub/yot/`, and `taubetmo:/pub/yot/`.

Using our example above, the two-way synchronization system basically tells that if the tree
`tarupam:/pub/yot/ninam/` contains new and/or updated items, compared with
`localhost:/pub/yot/ninam/`, and `localhost:/pub/yot/ninam/` also happens to have new and/or updated
items, then, they will trade updates.

Ideally, the result is that `localhost:/pub/yot/ninam/`, `tarupam:/pub/yot/ninam/`, and
`taubetmo:/pub/yot/ninam/`, are all equal.


It is also possible to perform synchronization of multiple files, and directories, to remote
hosts. To do so, run:

    $ usync /pub/yot/ninam/ ~/file.text ~reyn/*.blend tarupam,taubetmo

The command above will perform two-way synchronization of the paths
`/pub/yot/ninam/`, `~/file.text`, and `~reyn/*.blend` to the
remote hosts `tarupam`, and `taubetmo`, using the same directory
structuring system described above.

If you want to perform one-way synchronization, of the above, like
`rsync`, run:

    $ usync --one-way --prefer-local /pub/yot/ninam/ ~/file.text ~reyn/draft.blend tarupam,taubetmo

For more usage information, run:

    $ usync --help


Credits
-------

Thanks to [Riastradh](http://community.schemewiki.org/?Riastradh) for helping me with Scheme48’s
module system.
