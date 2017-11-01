# vinyl0r
From analog audio output (vinyl player) to webstreaming

1. getting stuff together
You'll need a Raspberry Pi (I'm using RPi Zero w because it's small), an external soundcard like the [Behringer UCA222](https://www.amazon.de/Behringer-U-Control-UCA222-Interface-Soundkarte/dp/B0023BYDHK) should be pretty comfortable. Others might work too. And also, if not already integrated, you'll need an amplifier, like [this one](https://www.amazon.de/Musical-Fidelity-V90-LPS-Phonovorverst%C3%A4rker-MC-Tonabnehmer/dp/B00E5BY9SO/ref=sr_1_1?s=musical-instruments&ie=UTF8&qid=1509493902&sr=8-1&keywords=V90+LPS). But you can also use a different one.

2. Connect everything!
If your vinylplayer got an old DIN-connector, cut it and replace it with [cinch](https://www.amazon.de/Goobay-Cinchstecker-schwarz-high-quality/dp/B000L0ZO78/ref=sr_1_4?ie=UTF8&qid=1509494006&sr=8-4&keywords=cinch+stecker).
Now connect your vinyl player to the preamp, from the preamp via cinch to the audio IN on the usb soundcard and then just plug the usb thing into the raspberry. Straight forward.

3. Using Raspbian
Install raspbian on your raspberry and configure the networkstuff and SSH. Use google if you've no idea how to achieve this.

4. icecast & darkice
You'll use darkice to get your audiostuff from your device to something to work with. Yes, icecast will work with it.
So basically darkice is doing the invisible work while icecast is publishing everything as a stream.

5. install and configure darkice
It all starts with this:
```sudo apt-get install darkice```

Grab a copy of `darkice.cfg` and place it into the `/etc` folder on the raspberry.
Adjust some settings (like the password) if you want. Otherwise it will just work somehow.

If you have no idea what your device is called use `arecord -l`.
```
**** List of CAPTURE Hardware Devices ****
card 1: CODEC [USB Audio CODEC], device 0: USB Audio [USB Audio]
  Subdevices: 0/1
  Subdevice #0: subdevice #0
```

Yes, "Subdevices" is what you are looking for. It's for this part in the config:

```
[input]
device        = hw:1,0 
```

easy.

6. Install and configure Icecast

```
sudo apt-get install icecast2 
```

While the installation runs you'll configure it. No hard stuff here.

7. browse it

Take the IP address of the raspberry, add port 8000 to it (or whatever is configured) and add the mountpoint (see configfile).
It should look like this:

```http://192.168.0.9:8000/raspi.```

It's working. Nice. If not, start again. It IS working!
