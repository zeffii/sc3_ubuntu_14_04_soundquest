# sc3_ubuntu_14_04_soundquest

Day 1 (day 23, since the Holy Post. )

Don't read this unless you are equally as baffled as I am regarding getting sounds out of supercollider on ubuntu. My problems with Jack started years ago after upgrading from 11.04 to 12.04. Prior to that with Jack1 I could even use ASIO_WINE and run windows programs with ASIO support. It was pretty amazing. The upgrade pissed on that parade, like a drunk on st. Patrick's day - just an endless stream of getting nowhere but wet.

I'm writing this repository to chronicle my experience and hopefully it will conclude in some oscillations. The weak semblance of story reflects a weakened spirit, whose light is not yet dulled because there are other ways to make sound on linux (sunvox especially has made things tollerable, but it isn't opensource and I feel rude to ask someone else to code feature requests... and there's never a guarantee that requests are going to happen. fuck that, if I have an idea I want to try it ).

some commands:

### pacmd

**show all pulseaudio detected soundcards**
```
pacmd
>>> list-sinks
```
[output here](https://gist.github.com/zeffii/04c87cf25e2b20e69eea)

Yes, looks like i have alsa.card_name = "M Audio Audiophile192" . That's right, i remember buying it. I think this means that this line must exist in `/home/zeffii/.config/SuperCollider/startup.scd`

```
Server.local.options.device = "M Audio Audiophile192";
```
? who knows.. information is out there, but BARF almost too disparate to read, or maybe i'm not receptive enough to the overal message.


### [sudo] aplay -l

```
**** List of PLAYBACK Hardware Devices ****
card 0: Intel [HDA Intel], device 0: ALC882 Analog [ALC882 Analog]
  Subdevices: 0/1
  Subdevice #0: subdevice #0
card 0: Intel [HDA Intel], device 1: ALC882 Digital [ALC882 Digital]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: Audiophile192 [M Audio Audiophile192], device 0: ICE1724 [ICE1724]
  Subdevices: 0/1
  Subdevice #0: subdevice #0
card 1: Audiophile192 [M Audio Audiophile192], device 1: ICE1724 IEC958 [ICE1724 IEC958]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
```

Weird that the index is pacmd of audiophile was 0 but here it is listed as card 1, device 0. should this concern me?

### lspci -v | grep -A7 -i "audio"

```
00:1b.0 Audio device: Intel Corporation NM10/ICH7 Family High Definition Audio Controller (rev 01)
	Subsystem: ASUSTeK Computer Inc. Device 81d8
	Flags: bus master, fast devsel, latency 0, IRQ 47
	Memory at febfc000 (64-bit, non-prefetchable) [size=16K]
	Capabilities: <access denied>
	Kernel driver in use: snd_hda_intel

00:1c.0 PCI bridge: Intel Corporation NM10/ICH7 Family PCI Express Port 1 (rev 01) (prog-if 00 [Normal decode])
--
01:00.0 Multimedia audio controller: VIA Technologies Inc. VT1720/24 [Envy24PT/HT] PCI Multi-Channel Audio Controller (rev 01)
	Subsystem: VIA Technologies Inc. Device 3632
	Flags: bus master, medium devsel, latency 64, IRQ 21
	I/O ports at 8c00 [size=32]
	I/O ports at 8880 [size=128]
	Capabilities: <access denied>
	Kernel driver in use: snd_ice1724
```

## SC server and Catia show signal. 

I'm even able to record the signal using Audacity. So this seems to be about routing Jack Dummy to Pulse Audio

![shome](https://cloud.githubusercontent.com/assets/619340/7198538/83ffac9e-e4ed-11e4-919f-e4ee62f0cba7.png)

http://www.alsa-project.org/main/index.php/Asoundrc



