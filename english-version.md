# TinyTuya-macOs (english)
Phyhton module for the Tuya interface

* First you install `Phyton3`
> https://www.python.org/downloads/macos/

* Then `pip` is required.
There are various options for installing this.
> https://pip.pypa.io/en/latest/installation/


The following is a python script that uses bootstrapping logic to install pip.
* Download the script from https://bootstrap.pypa.io/get-pip.py
* Open the terminal, "cd" in the folder with the file get-pip.py and execute the following code:

````
python3 get-pip.py
````

## TinyTuya Setup
Install the `pip3` and` Phyton3` modules:
````
pip3 install pycryptodome
`````

### Install TinyTuya
```
pip3 install tinytuya
```

## Tuya Device - preparation
> Controlling and monitoring Tuya devices on your network requires the following:
> * Address - The network address (IPv4) of the device, e.g. 10.0.1.100
> * Device ID - The unique identifier for the Tuya device
> * Version - The Tuya protocol version used (3.1 or 3.3)
> * Local_Key - The security key created to encrypt and decrypt communications

### Network Scanner
TinyTuya has an integrated network scanner that can be used to find Tuya devices in the local network.
It shows the address, device ID and version for each device.
````
python3 -m tinytuya scan

````

### Setup Wizard
TinyTuya has a built-in setup wizard that uses the Tuya IoT Cloud Platform to generate a JSON list (devices.json) of all of your registered devices. This includes the secret Local_Key and the name of each device.

Follow the instructions below to get the Local_Key:
 1. Download the “Smart Life” app available for iPhone or Android. Pair all Tuya devices
 > (this is important as you will not be able to access an unpaired device)
 > * https://itunes.apple.com/us/app/smart-life-smart-living/id1115101477?mt=8
 > * https://play.google.com/store/apps/details?id=com.tuya.smartlife&hl=en
 2. Run the TinyTuya scan to get a list of the Tuya devices on the network (along with the device address, device ID and version number (3.1 or 3.3)):
````
python3 -m tinytuya scan

````
3. Set up a Tuya account:
> Create a **Tuya Developer** account on iot.tuya.com

> Click on the "Cloud" symbol -> Create a new project (*Create Cloud Project*) (always remember the authorization key: *Access ID / Client ID:* and *Access Secret / Client Secret:* for the next step)

> Click again on the "Cloud" symbol -> Project overview -> Linked device (*Devices*) -> Link devices by app account (*Link Tuya App Account*)

> Click on "Add App Account" (*Link Tuya App Account*) and a QR code will be displayed. Scan the QR code directly in the Smart Life app on the phone. To do this, simply click on "Profile" at the bottom left and select the first symbol at the top right. If you scan the QR code, all devices registered in the “Smart Life” app will be linked to the Tuya IoT project.
4. Run Setup Wizard:

> Run the TinyTuya setup wizard on the Mac to get the Local_Keys for all registered devices:
````
python3 -m tinytuya wizard
````
> The wizard asks you to enter the API ID key, the API secret and the API region (us, eu, cn or in) from your Tuya IoT project mentioned above. It will also ask for a sample device ID. Use one from step 2 (above) or find it in the device list of your Tuya IoT project.

> The wizard queries the Tuya IoT cloud platform and prints a JSON list of all your registered devices with the "name", the "ID" and the "key" of the registered devices. The "keys" in this list are the Local_Key of the devices that they use to access your device.

> In addition to displaying the device list, the wizard creates a local devices.json file. (You can find this in the Finder under: User -> Username) TinyTuya uses this file to provide additional details for scanning results from tinytuya.scanDevices () or when we run `python3 -m tinytuya` to scan our local network.

> At the end, the wizard asks whether we want to query all devices. When you do this, the status of all devices will be displayed in records and a Snapshot.json file will be created with the results. (This is also in our user folder)


You can find more information directly at TinyTuya: https://pypi.org/project/tinytuya/#description
