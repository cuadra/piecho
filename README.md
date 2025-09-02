# pi0player
Steps and code to turn a Pi Zero into an audio player
## Equipment
1. USB powered speaker
2. Raspberry Pi Zero

## Setup
1. Use Raspberry Pi Imager to install Raspberry OS Lite
2. Boot Pi Zero and Login
3. Use `raspi-config` to enter config options
4. Choose System Settings > Auto Login

## Install Dependencies
1. Update Linux w/ `apt-get update`
2. Install mpg123 w/ `sudo apt install mpg123`
3. Optional: Install vim w/ `sudo apt install vim`

## Save Audio
1. SSH into Pi and save audio

## Create Startup script to autoplay music
1. Create .sh file
2. chmod +x [name].sh
3. crontab -e
4. @reboot path/to/file.sh

## Choose correct sound card
Check sound card devices `aplay -l`
1. `sudo [nano|vim] ~/.asoundrc`
2. add `pcm.!default { type hw card 1 [or 0] }`
3. add `ctl.!default { type hw card 1 [or 0] }`
4. Run sh script to check that you hear the sound from the correct output.
