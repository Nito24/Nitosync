# Nitosync
This script provides a simple way of syncing files at the time of opening and closing the specified program with the help of RSync.
This is quite usefull for syncing save files of emulators and such between multiple devices. I made this with the aim of being able to play the same savefiles in my PC and SteamDeck in a seamless way and without this compromising the portable's battery life. Other solutions to this problem were thins such as Syncthing which, in my opinion took too many resources from the SteamDeck as it is allways running in the background. My solution (although not perfect in any way) doesn't compromise as many resources as it only runs when asked. Furthermore, this solution works more in line with how Steams own cloud save syncrhonization works.

https://www.027182.xyz/nitosync.mp4

Dependencies:
  - Rsync
  - Notify-Send

This script uses Rsync to syncrhonice files over ssh so setting up keys is essensial. Doing this ensured that ssh passwords will not be stored as plain text. It also provides us with enough security to port forward the server's ssh port so that files can be synced from the internet and not only LAN (if you plan on doing this you will probably need to setup a dynamic DNS too to avoid changing the IP manually every time it changes).

Syncing files using Nitosync:

This little script reads the default config and then, if asked, overides the desired values with an extra config file. The thinking behind this is that values such as the server's IP, user, port... can be kept in the global configuration and other values such as diferent save directories and emulator paths can be changed with their own configs. With this, we can have a config file which only overides the necessary values per system/emulator fom example, a config file for ps2 and another for megadrive.
A sample config file can be found in this repo.

Nitosync installation is purely manual, you can decide where to save the script (/usr/bin or similar is recommended). Config files can also be saved where one desires (although I would chose a normal location such as ~/.config/nitosync which is actually the default location stated in the scipt).

For use with the SteamDeck as it has an inmmutable OS rather than unlocking it I chose to store the whole scipt and config files in ~/.config/nitosync. The only drwback is that nitosync will not be recogniced as a command and you have to add the folder to the $PATH or just use the full path when calling it.

At the end of the day, you would tweak the config files to your necessities and then would change your emulators shortcuts so that they point to Nitosync with -c to the desired config and it would automatically just sync everithing for you. On a SteamDeck you would edit the shortcuts of each game so that instead of pointing to the emulator and the game they would point to Nitosync and the game (specifiying the -c).

Nitosync also counts with automatic backups and an option to do a full sync (really usefull for first runs if you already have saves).
