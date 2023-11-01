# git-inv - inventory of git repositories

## The Problem

I regularly use multiple computers and need to bring all my repositories with
me as I move between them. I was looking for a simple tool that can keep track
of all my repositories and allow me to save their remote origin URLs in
[`yadm`](https://github.com/TheLocehiliosan/yadm). I've tried using
[`gita`](https://github.com/nosarthur/gita) and other similar tools, but found
them to be either too complex or they didn't save URLs in their configuration.

## The Solution

Drop `git-inv` to the `$PATH` and...

```
$ cd ~
$ mkdir .git-inv
$ git inv save Desktop/neomutt/
Repository `Desktop/neomutt' saved.
$ git inv save Desktop/qutebrowser/
Repository `Desktop/qutebrowser' saved.
$ yadm add .git-inv/
$ git inv
Desktop/neomutt      main  2 days ago
Desktop/qutebrowser  main  8 days ago
$ git inv list
Desktop/neomutt
Desktop/qutebrowser
$ rm -rf Desktop/neomutt
$ git inv list
Desktop/qutebrowser
$ git inv lost
Desktop/neomutt
$ git inv lost | git inv clone
Desktop/neomutt
Cloning into 'Desktop/neomutt'...
remote: Enumerating objects: 130493, done.
remote: Counting objects: 100% (3241/3241), done.
remote: Compressing objects: 100% (1051/1051), done.
remote: Total 130493 (delta 2468), reused 2797 (delta 2189), pack-reused 127252
Receiving objects: 100% (130493/130493), 147.84 MiB | 13.80 MiB/s, done.
Resolving deltas: 100% (107259/107259), done.
$ git inv list
Desktop/neomutt
Desktop/qutebrowser
$ git inv status
Desktop/neomutt
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
Desktop/qutebrowser
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
$ git inv list | grep neomutt | git inv exec describe
Desktop/neomutt
20231023-38-g728800561
```
