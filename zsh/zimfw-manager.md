# Using zim:fw for zsh settings management

I've been using [zim:fw](https://zimfw.sh/) for the past year or so to manage
my zsh shell configuration. I was finding that `oh-my-zsh` and `zprezto` were
causing me performance issues on initial shell load.

I did some troubleshooting of the startup time using `zprof` to profile what
was taking time to load. After doing that analysis I looked for something that
was more lightweight. Check out the performance comparison to other
frameworks in the [repo's](https://github.com/zimfw/zimfw) home page.

## zim:fw

After installing, the basics include the `.zimrc` config file and
the `zimfw` command line utility.

Themes and modules are set in the `.zimrc` file by using
the `zmodule` command.

### Common commands
- `zimfw install`
- `zimfw uninstall`
- `zimfw list`
- `zimfw update` to update modules
- `zimfw upgrade` to upgrade the zimfw plugin manager

## Summary

Overall, `zimfw` has met my needs well. It's straightforward to use
and extensible enough to take advantage of `oh-my-zsh` config as well.
