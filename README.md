### This project is a fork from CyrisXD's original Pwnagetty project and builds upon their hard work. 
I'm simply updating the project to work with the *jayofelony pwnagotchi build* and *MacOS* as the host. I'll aim to test with Linux in the near future and update as needed.
##### Happy pwning!


# Pwnagetty


Pwnagetty is a cli application written in NodeJS, to streamline the process of downloading handshakes from your Pwnagotchi, verify each PCAP file and convert them to the appropriate format (EAPOL or PMKID) ready for Hashcat cracking. All while keeping a log of converted files and BSSID's to eliminate duplicates in the future.

Pwnagetty favors PMKID's and will try to convert this first. If a PMKID is found within a PCAP file, it will ignore the EAPOL as it's not needed. If no PMKID is found, it will then make use of the EAPOL instead. This is why you may end up with more PMKID files and less HCCAPX files. 


## Requirements

Pwnagetty relies on the below. Make sure you have these installed *before* installing Pwnagetty.

[NODEJS](https://nodejs.org/en/) - (Built with NodeJS)

**Mac** users can install with:
```
brew install nodejs
```


[HCXPCAPNGTOOL](https://github.com/ZerBea/hcxtools) - (To verify and convert PCAP's)

**Mac** users can install with:
```
brew install hcxtools
```


[AIRCRACK-NG](https://www.aircrack-ng.org/) - (To extract BSSID's from PCAP's)

**Mac** users can install with:
```
brew install aircrack-ng
```


## Installation

Choose a directory you'd like to save this in then run the below.

```
git clone https://github.com/ciananlee/Pwnagetty.git
cd Pwnagetty
npm install
npm install -g

```
Edit the config to add your details inside of Pwnagetty/bin/index.js
You'll likely only need to change the username, password and handshakeDir.
```
//====================================
// SFTP Configuration - CHANGE THESE
//====================================
const config = {
    host: "10.0.0.2", // Set your Pwnagotchi IP
    username: "pi", // Set your SSH username
    password: "raspberry", // Set your SSH password, remember to change the default if you haven't already!
    handshakeDir: "/root/handshakes", // Set your handshake directory on the Pwnagotchi
    port: 22,
    localDir: "./pcap/",
    database: path.join(__dirname, "./db.json"),
};
```

## Usage
Connect your Pwnagotchi to your computer and wait for it to boot.
Navigate to an empty local directory in terminal and just run:
``` 
pwnagetty
```

Pwnagetty will then SFTP into your Pwnagotchi, create 3 local folders in your empty directory and do it's job.

You can use 
```
pwnagetty -r
```
to remove Pwnagotchi captured files after processing

## Disclaimer
This was built for educational purposes. (I had fun learning about await/async). It goes without saying, **do not use this tool against or with networks you do not have permission for. I am not liable for your actions.**
