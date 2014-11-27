git-post-receive-irc-bot
========================

Reports to #channels about pushes, deletes, force-pushes, new branches etc. Like GitHub's IRC bot.

![screenshot](http://i.imgur.com/lD2z49h.png)
![screenshot](http://i.imgur.com/SeOlIWH.png)
![screenshot](http://i.imgur.com/ZW6q2BJ.png)
![screenshot](http://i.imgur.com/tZsVqIz.png)

Setup
-----------

1. Clone the repo or download the zip.
1. Clone/download [suckless/ii](http://tools.suckless.org/ii/) pipe-based IRC client and extract to `ii-src/`.
1. Edit `PREFIX` in `ii-src/config.mk` to point to `ii/` and `$ make clean install`.
1. Copy `connect.example` to `connect` and modify to suit your needs; most probably you'll want to change:
   1. `channels_onconnect='#us #test'`
   1. `ii`'s start-up command (server, port, nick, username, password) → see `$ man ./ii/share/man/man1/ii.1`.
1. Run `./connect`. It will start both `ii` and its reconnector in the background and exit immediately. No feedback is correct here.
1. The bot will have connected to the IRC server by now.

Now, on the same server from which you're running the bot, create `$YOUR_REPO'S_GIT_DIR/hooks/post-receive` with the following content:

```sh
#!/bin/sh
/your_directory_to_extracted/git-bot/post-receive 'irc.somewhere.net' '#channel'
```

`irc.somewhere.net` must match the `-s <servername>` parameter of `ii` in `connect` script.
