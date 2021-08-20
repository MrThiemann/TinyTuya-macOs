# TinyTuya-macOs
Phyhton-Modul zur Tuya Schnittstelle

* Als erstes installiert man sich `Phyton3`
> https://www.python.org/downloads/macos/

* Anschließend wird `pip` benötigt.
Hier gibt es verschiedene Möglichkeiten, dieses zu installieren.
> https://pip.pypa.io/en/latest/installation/
> 


Folgendes ist ein Python-Skript, das eine Bootstrapping-Logik verwendet, um pip zu installieren.
* Lade das Skript herunter von https://bootstrap.pypa.io/get-pip.py
* Öffne das Terminal, "cd" in den Ordner mit der Datei get-pip.py und führe folgenden code aus:

````
python3 get-pip.py
````

## TinyTuya Setup
Installiere die `pip3` und `Phyton3` Module:
````
pip3 install pycryptodome
`````

### TinyTuya installieren
```
pip3 install tinytuya
```

## Tuya Device - Vorbereitung
> Das Steuern und Überwachen von Tuya-Geräten in Ihrem Netzwerk erfordert Folgendes:
> * Adress - Die Netzwerkadresse (IPv4) des Geräts, z.B. 10.0.1.100
> * Device ID - Die eindeutige Kennung für das Tuya-Gerät
> * Version - Die verwendete Tuya-Protokollversion (3.1 oder 3.3)
> * Local_Key - Local_Key – Der Sicherheitsschlüssel, der zum Verschlüsseln und Entschlüsseln der Kommunikation erstellt wurde

### Network Scanner
TinyTuya verfügt über einen integrierten Netzwerkscanner, mit dem Tuya-Geräte im lokalen Netzwerk gefunden werden können. 
Es zeigt Adresse, Geräte-ID und Version für jedes Gerät an.
````
python3 -m tinytuya scan

````

### Setup Wizard
TinyTuya verfügt über einen integrierten Einrichtungsassistenten, der die Tuya IoT Cloud Platform verwendet, um eine JSON-Liste (devices.json) aller Ihrer registrierten Geräte zu generieren. Dazu gehören der geheime Local_Key sowie der Name jedes Geräts.

Folge den Anweisungen unten, um den Local_Key zu erhalten:
 1. Lade die „Smart Life“-App herunter, die für iPhone oder Android verfügbar ist. Koppel alle Tuya-Geräte 
 > (dies ist wichtig, da Sie nicht auf ein nicht gekoppeltes Gerät zugreifen können)
 > * https://itunes.apple.com/us/app/smart-life-smart-living/id1115101477?mt=8
 > * https://play.google.com/store/apps/details?id=com.tuya.smartlife&hl=en
 2. Führe den TinyTuya-Scan aus, um eine Liste der Tuya-Geräte im Netzwerk ( zusammen mit der Geräteadresse, Geräte-ID und Versionsnummer (3.1 oder 3.3))  zu erhalten:
````
python3 -m tinytuya scan

````
3. Richte ein Tuya-Konto ein:
> Erstelle ein **Tuya Developer**-Konto auf iot.tuya.com
> Klicke auf das Symbol "Cloud" -> Erstellen ein neues Projekt (*Create Cloud Project*) (denken immer an den Autorisierungsschlüssel: *Access ID/Client ID:* und *Access Secret/Client Secret:* für den nächsten Schritt)
> Klicke wieder auf das Symbol "Cloud" -> Projektübersicht -> Verknüpftes Gerät (*Devices*) -> Geräte nach App-Konto verknüpfen (*Link Tuya App Account*)
> Klicke auf „App-Konto hinzufügen“ (*Link Tuya App Account*) und es wird ein QR-Code angezeigt. Scanne  den QR-Code direkt in der Smart Life-App auf dem Telefon. Hierfür einfach unten links auf "Profil" drücken und oben recht das erste Symbol wählen. Wenn Du den QR-Code scannst, werden alle in der  „Smart Life“-App registrierten Geräte mit dem Tuya IoT-Projekt verknüpft.
4. Run Setup Wizard:
> Führe auf dem Mac den TinyTuya-Setup-Assistenten aus, um die Local_Keys für alle registrierten Geräte abzurufen:
````
python3 -m tinytuya wizard
````
> Der Assistent fordert Dich zur Eingabe des API-ID-Schlüssels, des API-Geheimnisses und der API-Region (us, eu, cn oder in) aus deinem oben genannten Tuya IoT-Projekt auf. Es wird auch nach einer Beispiel-Geräte-ID gefragt. Verwenden hier eine aus Schritt 2 (oben) oder finden diese in der Geräteliste deines Tuya IoT-Projekts.
> Der Assistent fragt die Tuya IoT Cloud-Plattform ab und druckt eine JSON-Liste aller deiner registrierten Geräte mit dem "Namen", der "ID" und dem "Schlüssel" der  registrierten Geräte. Die "Schlüssel" in dieser Liste sind die Local_Key der Geräte, die sie für den Zugriff auf dein Gerät verwenden.
> Zusätzlich zur Anzeige der Geräteliste erstellt der Assistent eine lokale Datei devices.json. (Diese findest Du im Finder unter: Benutzer -> Benutzername) TinyTuya verwendet diese Datei, um zusätzliche Details zum Scannen von Ergebnissen von tinytuya.scanDevices() bereitzustellen oder wenn wir `python3 -m tinytuya` ausführen, um unser lokales Netzwerk zu scannen.
> Der Assistent fragt am Schluss, ob wir alle Geräte abfragen möchten. Wenn Sie dies tun, wird der Status aller Geräte in Datensätzen angezeigt und eine Snapshot.json-Datei mit den Ergebnissen erstellt. (Diese liegt ebenfall in unserem Benutzerordner)


Weitere Informationen könnt ihr direkt bei TinyTuya finden: https://pypi.org/project/tinytuya/#description

Besucht uns auch gerne auf Discord (**Smarthome YourSelf**) : https://discord.gg/f7TFNeeK2d
