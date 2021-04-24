Can you guys let me know if this is everything I would need to do to switch over?

1   remove lightdm (pacman -Rs lightdm).

2   remove /usr/share/xessions and /etc/lightdm

3   install xorg-init

4   move any programs i want to launch on start from .xprofile to .xinitrc (also add xmonad here).

5  reboot, login, and execute startx

Auto startx when you login
    pgrep 'tmux|startx' || startx

---------------------------------------------------------------------------------------------------------------------

Getting rid of your display mananger

    $ systemctl dissable lightdm

    reboot, you should see a prompt asking for your username and password
    $ startx

    Auto startx
    $ vim .bash_profile

    if [[ ! $DISPLAY && $XDG_VTNR -eq 1 ]]; then
    exec startx   # remove the exec to remain logged in when your wm ends
    fi

    .xinitrc file
    #!/bin/sh
    userresources=$HOME/.Xresources
    usermodmap=$HOME/.Xmodmap
    sysresources=/etc/X11/xinit/.Xresources
    sysmodmap=/etc/X11/xinit/.Xmodmap
    # merge in defaults and keymaps
    if [ -f $sysresources ]; then
        xrdb -merge $sysresources
    fi
    if [ -f $sysmodmap ]; then
        xmodmap $sysmodmap
    fi
    if [ -f "$userresources" ]; then
        xrdb -merge "$userresources"
    fi
    if [ -f "$usermodmap" ]; then
        xmodmap "$usermodmap"
    fi
    # start some nice programs
    if [ -d /etc/X11/xinit/xinitrc.d ] ; then
    for f in /etc/X11/xinit/xinitrc.d/?*.sh ; do
    [ -x "$f" ] && . "$f"
    done
    unset f
    fi

    exec i3
---------------------------------------------------------------------------------------------------------------------
    How to Install i3 Window Manager in Linux

    Install i3
    $ sudo pacman -S i3
    Edit Xinitrc
    $ echo "exec i3" >> ~/.xinitrc
    Install Xorg
    $ sudo pacman -S xorg-server xorg-xinit
    Start i3
    $ startx

Sources:

https://blog.beardhatcode.be/2018/03/getting-rid-of-your-dm.html
https://www.reddit.com/r/archlinux/comments/9ahe6w/switching_from_a_displaymanager_lightdm_to_startx/
