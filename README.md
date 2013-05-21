# Introduction

**Usync** is a site-to-site synchronization program written in
[Scsh](http://www.scsh.net). It makes use of
[unison](http://www.cis.upenn.edu/~bcpierce/unison/), and
[rsync](https://rsync.samba.org/), for bi-directional, and
uni-directional synchronization, respectively.

# Usage

To perform two-way synchronization of the directory `/pub/yotninam/`,
between the current host, and to the hosts `tarupam`, and `taubetmo`:

```
usync /pub/yotninam tarupam,taubetmo
```

Take note, that there are no spaces between the hosts.

For more usage help, run:

```
usync --help
```
