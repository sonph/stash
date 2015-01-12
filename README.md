# What
`stash` is a simple Python script used to quickly save and access values in the shell across different sessions.

# Why
A lot of times I need to use some values over and over again such as a server's IP address or a path.

For example:

    scp -R somepath 69.59.69.59:~/
    ssh 69.59.69.59

Saving these into environment variables is a viable solution but they do not persist across different shell session.

Storing them into dotfiles is simple, just `echo VAR=value >> ~/.zshenv`, but what if you want to change them or "refresh" in existing sessions (or maybe in different `tmux` tabs)? `source ~/.zshenv` everytime is surely too much of a hassle.

# How
* `stash <key> <value>` to save a value
* or `<cmd> | stash <key> --stdin` to save a value
* `` `stash <key>` `` or `$(stash <key>)` to acess a value

Or better yet, if you are using `zsh` (this can't be done in `bash` AFAIK), alias `$` to `stash` with `echo "alias \$='<path-to-stash>'" >> ~/.zshrc` so you can do

* `$ <key> <value>` to save
* `` `$ <key>` `` to access a value

With this, now you can do:

    $ AWS 69.59.69.59
    scp -R somepath `$ AWS`:~/
    # and in another shell
    ssh `$ AWS`



# Install
In `zsh`:
`wget -O $HOME/.stash https://raw.githubusercontent.com/sonph/stash/master/stash && chmod u+x $HOME/.stash && echo "alias \$='$HOME/.stash'" >> $HOME/.zshrc`

In `bash`:
`wget -O $HOME/.stash https://raw.githubusercontent.com/sonph/stash/master/stash && chmod u+x $HOME/.stash && echo "alias stash='$HOME/.stash'" >> $HOME/.bashrc`
