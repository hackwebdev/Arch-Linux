popup-massage when using blueman bluetooth

$ sudo vim /etc/polkit-1/rules.d/81-blueman.rules 

polkit.addRule(function(action, subject) {
    if ((action.id == "org.blueman.network.setup" ||
         action.id == "org.blueman.dhcp.client" ||
         action.id == "org.blueman.rfkill.setstate" ||
         action.id == "org.blueman.pppd.pppconnect") &&
        subject.isInGroup("netdev")) {
        return polkit.Result.YES;
    }
});