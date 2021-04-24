# Arch-Linux
My Arch Linux Setup

Display manager:
        $ sudo pacman -S lightdm lightdm-gtk-greeter
        $ sudo pacman -S lightdm-gtk-greeter-settings
        $ sudo nano /etc/lightdm/lightdm.conf
        [Seat:*]
        ...
        greeter-session=lightdm-yourgreeter-greeter
    Now enable the service:
        $ sudo systemctl enable lightdm

Check my video driver
    lspci | grep -e VGA -e 3D

Bluetooth
        $ sudo pacman -S bluez blueman bluez-utils
        $ modeprobe btusb
    Enable and Start bluetooth service:
        $ sudo systemctl enable bluetooth && sudo systemctl start bluetooth

Remove beep sound:
        $ sudo mkdir /etc/modeprobe.d
        $ sudo vim /etc/modprobe.d/nobeep.conf
            blacklist pcspkr blacklist snd_pcsp
        $ reboot

Network:
        $ sudo pacman -S dialog wpa_actiond ifplugd wpa_supplicant
        $ ip link
        $ sudo systemctl enable dhcpcd && sudo systemctl start dhcpcd
        $ sudo systemctl enable dhcpcd@enp0s31f6 && sudo systemctl start dhcpcd@enp0s31f6
        $ sudo systemctl enable dhcpcd@wlp2s0 && sudo systemctl start dhcpcd@wlp2s0
    You should also enable dhclient service:
        $ sudo systemctl enable dhclient && sudo systemctl start dhclient
        $ sudo systemctl enable dhclient@enp2s0 && sudo systemctl start dhclient@enp2s0
        $ sudo systemctl enable dhclient@wlp3s0 && sudo systemctl start dhclient@wlp3s0
    start and enable is NetworkManager
        $ sudo systemctl start NetworkManager.service && sudo systemctl enable NetworkManager.service
        $ sudo pacman -S network-manager-applet
    applet can be run by:
        $ nm-applet

Sound Server:
    $ sudo pacman -S pavucontrol alsa-firmware alsa-utils alsa-plugins pulseaudio-alsa pulseaudio
    Note: you can either use pavucontrol or alsamixer command in terminal to choose sound card

https://www.unixmen.com/top-things-installing-arch-linux/

