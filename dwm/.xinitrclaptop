#!/bin/sh

dte(){
	dte="$(date "+%a %b %d,%Y %I:%M %p %Z")"
	echo -e " $dte"
}

battery(){
	battery="$(cat /sys/class/power_supply/BAT0/capacity)%"
	echo -e "Bat: $battery"
}


while true; do
        xsetroot -name "$(dte) | $(battery)"
        sleep 1m # update time every minute
done &

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

nitrogen --restore &
picom &
xbindkeys -f ~/.xbindkeysrc
exec dwm

