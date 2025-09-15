
## Requirements
1. Raspberry Pi Zero + power supply
2. USB-powered speaker
3. MicroSD card + reader

## Setup
1. Use **Raspberry Pi Imager** to install **Raspberry OS Lite** on the SD Card.
2. Connect USB speaker.
3. Boot Pi Zero and log in.
4. Enter config
   ```
   raspi-config
   ```
    * Go to **System Options** > Auto Login.
## Install Dependencies
1. Update the system
   ```
   sudo apt-get update
   ```
3. Install [**mpg123**](https://www.mpg123.de/)
   ```
   sudo apt install mpg123
   ```
5. Optional: Install [**Vim**](https://github.com/vim/vim):
   ```
   sudo apt install vim
   ```

## Add Audio Files
1. use SSH or another transfer method to copy audio files to the Pi.
     * Example: `scp audio.mp3 pi@<ip-address>:~/`

## Create Startup script to autoplay music
1. Create a script file (e.g. player.sh):
   ```
   vim ~/player.sh
   ```
   * Insert the following code:
      ```
      while true
	      do
		      mpg123 ~/audio.mp3
		      sleep 300 # wait 5 minutes
	      done
      ```
3. Make it executable:
   ```
   chmod +x player.sh
   ```
4. Schedule it to run on boot: (do not use sudo)
   ```
   crontab -e
   ```
5. Add this line at the bottom:
   ```
   @reboot ~/player.sh
   ```
## Configure the Audio Output
1. Check available sound devices (Connect your speakers if you havent done so yet.)
   ```
   aplay -l
   ```
2. Create or edit the config file:
   ```
   sudo vim ~/.asoundrc
   ```
3. Set the default card to the USB device. (Not HDMI) In my case it was listed as '1' (The output number may change once you disconnect the HDMI.)
   ```
   pcm.!default { type hw card 1 }
   ctl.!default { type hw card 1 }
   ```
4. Run your script to confirm sound plays through the desired output:
   ```
   ./player.sh
   ```
## Troubleshooting
If mpg123 delivers an error similar to 'unable to set up output format' then you are attempting to play the audio through the wrong card.
