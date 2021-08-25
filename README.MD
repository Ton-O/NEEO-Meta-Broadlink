### NEEO/Meta Broadlink
## What's this?

This repository contains an example of my Broadlink driver. 
It is used to allow NEEO to call Broadlink devices over the meta-package (see (https://github.com/jac459/meta).

It is ONLY an example of how to create a custom driver. The custom driver requires
- Meta; The excellent package of JAC459 for hosting various custom drivers with a lot of added functonality on top of NEEO.
- NEEO/Meta-plus; an extension to meta (see https://github.com/Ton-O/NEEO-Meta-Plus)

## How to use
From the custom driver (or direrctly through http-calls if you want), you can perform the following actions:
- xmit:   send infrared codes that are in naive Broadlink format
- xmitGC: send infrared codes that are in NEEO's native format (Glbal Cache) 
- rcve:   Learn infrared codes in naive Broadlink format
- rcveGC: Learn infrared codes in NEEO's native format (Glbal Cache) 
- GCToBroad: Convert Infrared codes that are in NEEO's native format into Broadlink codes (Global Cache) 
- BroadtoGC: Convert Infrared codes that are in Broadlink format (Global Cache) into NEEO's native format 

Below is an overview of possible parameters:
1 host: specify the IP-address of your broadlink device; is resolved during Meta discovery
2 type: then type of Broadlink device; is resolved duriung Meta discovery
3 mac: the MAC-address of Broadlink device; is resolved during Meta discovery
4 stream: the data that needs to be send (the IR-codes)
In all cases, the first 3 paramaters are required. Parameter 4 is not required when using rcve or rcveGC. 

This is an example of sending native NEEO IR-codes via Broadlink using a custom driver and meta;


         "BACK":{"label":"","type":"http-get", "command":"$BroadlinkSendsendir,1:1,1,36000,1,1,96,32,16,32,16,16,16,16,16,32,32,16,16,16,16,16,16,16,16,16,16,16,16,16,16,16,32,32,16,16,32,16,16,16,16,16,16,16,16,3037"},

Where $BroadlinkSend is defined as
BroadlinkSend":"http://127.0.0.1:5000/xmitGC?host=192.168.0.9&&type=0x6539&&mac=a043b0542a78&stream=

An example for learning data isn't available at this mmoment, but learning is quitre simple:
- Send an http-request like this: http://127.0.0.1:5000/rcve
- The white button on the Broadlink will start illuminating coinstantly
- Point the remote that needs to be learned owards the Broadlink device and press the button to be learned.
- The white button on the Broadlink will go off
 
 The learning is complete. In the log of PythonManager.py, you can find the code that was learned.