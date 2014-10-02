Logitech K810 keyboard Linux Bluetooth pairing
==============================================

Solution for a persistent connection
------------------------------------

Set keyboard discoverable:

`hcitool scan`

Copy mac address XX:XX:XX:XX:XX:XX:

`sudo bluez-simple-agent hci0 XX:XX:XX:XX:XX:XX`

Which will hopefully return something like:

```
    DisplayPasskey (/org/bluez/537/hci0/..., 123456)
```

The number at the end of the string represents the PIN you need to enter for pairing. Enter those numbers on your bluetooth device and confirm with return. On success you should get:

```
	Release
	New device (/org/bluez/...)
```

Set device as trusted:

`sudo bluez-test-device trusted XX:XX:XX:XX:XX:XX yes`

You might have a connection now, but i still needed to:

`sudo bluez-test-input connect XX:XX:XX:XX:XX:XX`

Reboot and hope for the best.


Creating device failed: `org.bluez.Error.AlreadyExists`
-------------------------------------------------------

Reset pairing:

`sudo bluez-simple-agent hci0 XX:XX:XX:XX:XX:XX repair`

Start over.

---

Stolen from [here](http://devasive.blogspot.ch/2012/11/ubuntu-1204-persistent-bluetooth-pairing.html).
