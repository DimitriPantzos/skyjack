# [SkyJack](dimitripantzos.com)

SkyJack is a drone engineered to autonomously seek out, hack, and wirelessly take full control over any other drones within wireless or flying distance, creating an army of zombie drones under your control.

## Overview

Today Amazon announced they're planning to use unmanned drones to deliver some packages to customers within five years. Cool! How fun would it be to take over drones, carrying Amazon packages…or take over any other drones, and make them my little zombie drones. Awesome.

Using a Parrot AR.Drone 2, a Raspberry Pi, a USB battery, an Alfa AWUS036H wireless transmitter, aircrack-ng, node-ar-drone, node.js, and my SkyJack software, I developed a drone that flies around, seeks the wireless signal of any other drone in the area, forcefully disconnects the wireless connection of the true owner of the target drone, then authenticates with the target drone pretending to be its owner, then feeds commands to it and all other possessed zombie drones at my will.

SkyJack also works when grounded as well, no drone is necessary on your end for it to work. You can simply run it from your own Linux machine/Raspberry Pi/laptop/etc and jack drones straight out of the sky.


------

### Software

#### SkyJack
[SkyJack](http://samy.pl/skyjack) (available from github) is primarily a perl application which runs off of a Linux machine, runs aircrack-ng in order to get its wifi card into monitor mode, detects all wireless networks and clients around, deactivates any clients connected to Parrot AR.drones, connects to the now free Parrot AR.Drone as its owner, then uses node.js with node-ar-drone to control zombie drones.

I detect drones by seeking out any wireless connections from MAC addresses owned by the Parrot company, which you can find defined in the [Registration Authority OUI](http://standards.ieee.org/develop/regauth/oui/oui.txt).

#### aircrack-ng

I use [aircrack-ng](http://www.aircrack-ng.org/) to put our wireless device into monitor mode to find our drones and drone owners. I then use aireplay-ng to [deauthenticate](http://www.aircrack-ng.org/doku.php?id=deauthentication) the true owner of the drone I'm targeting. Once deauthenticated, I can connect as the drone is waiting for its owner to reconnect.

#### node-ar-drone
I use [node-ar-drone](https://github.com/felixge/node-ar-drone) to control the newly enslaved drone via Javascript and [node.js](http://nodejs.org).


### Hardware

#### Parrot AR.Drone 2
The [Parrot AR.Drone 2](http://www.amazon.com/gp/product/B007HZLLOK/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B007HZLLOK&linkCode=as2&tag=samypl0c-20) is the drone that flies around seeking other drones, controlled from an iPhone, iPad or Android, and is also the type of drone SkyJack seeks out in order to control. SkyJack is also capable of seeking out Parrot AR.Drone version 1.

The Parrots actually launch their own wireless network which is how the owner of the drone connects. We take over by deauthenticating the owner, then connecting now that the drone is waiting for its owner to connect back in, exploiting the fact that we destroyed their wireless connection temporarily.

## Questions?

Feel free to contact me with any questions!

You can reach me at <dimitri@dimitripantzos.com>.
