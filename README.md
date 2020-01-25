# dmenu_move

Move files fast with Nautilus and dmenu.

![demo](/demo.gif)


## Introduction

_dmenu\_move_ is a Nautilus script, i.e. a custom scripted action for [Nautilus](https://wiki.gnome.org/action/show/Apps/Files?action=show&redirect=Apps%2FNautilus), GNOME file manager.

It allows user to move all selected files to a destination from a user-defined list.

The destination selection is achieved through [dmenu](https://tools.suckless.org/dmenu/) from [suckless.org](https://suckless.org/).

An accompanying script, _dmenu\_go_, allows to open a new Nautilus window to one of destination in the same list.

For more context, read the [accompanying blog post](https://www.eigenbahn.com/2020/01/25/gnome-shortcut-move-files).


## Installation

#### GNOME 3

Drop _dmenu\_move_ in folder `~/.local/share/nautilus/scripts/`.

Make it executable:

    $ chmod 755 ~/.local/share/nautilus/scripts/dmenu_move

Then to bind a keyboard shortcut to the script, create or edit `~/.config/nautilus/scripts-accels` with a line like:

    <Control>m dmenu_move

Restart nautilus for changes to take effect:

    $ nautilus -q

You can also optionally install _dmenu\_go_ in your user _PATH_. We recommend dropping it in `~/.local/bin/`.

Make it executable:

    $ chmod 755 ~/.local/bin/dmenu_go

Associate it to a keyboard shortcut. Go to `Settings` > `Keyboard Shortcuts`, all the way down and click on the `+` to add a custom shortcut.

![gnome_shortcut_settings](/gnome_shortcut_settings.png)


## Usage

Just select any number of files in nautilus and press the keyboard shortcut configured in `~/.config/nautilus/scripts-accels`.

You will be prompted for a destination.

If the destination is unreachable, an error message will be displayed.

Otherwise files will be moved there.

In case of mistake, last operation can be reverted by calling _dmenu\_move_ with the special `UNDO` destination.

If you also installed _dmenu\_go_, you can press its shortcut anytime to select a destination to spawn a new Nautilus window to.

## Configuration

You must define a list of alias / location couples in file `~/.config/dmenu_move_bookmarks.set`.

Here is an example minimal configuration:

```
# standard stuff
home ~
documents ~/Documents
desktop ~/Desktop
music ~/Music
pictures ~/Pictures
videos ~/Videos

# standard config folders
fonts ~/.fonts
home-bin ~/.local/bin

# specific config folders
conf/emacs ~/.emacs.d
conf/chromium ~/.config/chromium/Default
```

## Dependencies

 - bash
 - awk
 - sed
 - dmenu (from package `suckless-tools` on Debian-based systems)
 - GNOME / Nautilus (obviously)


## Compatibility

This documentation only talks about GNOME 3.

But this script was originally made for GNOME 2. So I assume it should work just fine under [MATE](https://mate-desktop.org/).


## Implementation details

_awk_ is used to parse configuration file and remove.

_sed_ is used for handling special characters.

_dmenu_ prompts the user for destination folder selection.

In case of error, _notify-send_ will create a popup.
