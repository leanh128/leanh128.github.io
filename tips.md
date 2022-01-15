# Edit Linux Mint - Cinamon's height

Edit cinnamon-settings/modules/cs_panel.py

# disable super key

gsettings set org.gnome.mutter overlay-key ''

# change icon size for covering broken monitor

edit : `/usr/share/gnome-shell/extensions/ubuntu-dock@ubuntu.com/dash.js`
* Move `this._initializeIconSize(this.iconSize);` below `this._monitorIndex = monitorIndex;` in `_init()`
* Edit function `_initializeIconSize(max_size)`
```js
_initializeIconSize(max_size) {
    let max_allowed = baseIconSizes[baseIconSizes.length-1];
    max_size = Math.min(max_size, max_allowed);

    if (Docking.DockManager.settings.get_boolean('icon-size-fixed')){
        if (this._monitorIndex == Main.layoutManager.primaryIndex){
            this._availableIconSizes = [max_size];
        } else {
            this._availableIconSizes = [84];
        }
    }
    else {
        this._availableIconSizes = baseIconSizes.filter(function(val) {
            return (val<max_size);
        });
        this._availableIconSizes.push(max_size);
    }
}
```
