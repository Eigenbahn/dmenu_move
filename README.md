# dmenu_move

Move files fast with Nautilus and dmenu.


## Introduction

_dmenu\_move_ is a Nautilus script, i.e. a custom scripted action for [Nautilus](https://wiki.gnome.org/action/show/Apps/Files?action=show&redirect=Apps%2FNautilus), GNOME file manager.

It allows user to move all selected files to a destination from a user-defined list.

The destination selection is achieved through [dmenu](https://tools.suckless.org/dmenu/) from [suckless.org](https://suckless.org/).


## Installation

#### GNOME 3

Drop _dmenu\_move_ in folder `~/.local/share/nautilus/scripts/`.

Make it executable:

    $ chmod 755 ~/.local/share/nautilus/scripts/dmenu_move

Then to bind a keyboard shortcut to the script, create or edit `~/.config/nautilus/scripts-accels` with a line like:

    <Control>m dmenu_move

Restart nautilus for changes to take effect:

    $ nautilus -q


## Usage

Just select any number of files in nautilus and press the keyboard shortcut configured in `~/.config/nautilus/scripts-accels`.

You will be prompted for a destination.

If the destination is unreachable, an error message will be displayed.

Otherwise files will be moved there.

In case of mistake, last operation can be reverted by calling _dmenu\_move_ with the special `UNDO` destination.


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


## Implementation details

_awk_ is used to parse configuration file and remove.

_sed_ is used for handling special characters.

_dmenu_ prompts the user for destination folder selection.

In case of error, _notify-send_ will create a popup.
