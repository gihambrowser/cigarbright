# Cigar
A fully functional open source Agar.io server implementation, written in Node.js. Cigar is based on the same code as Ogar, but introduces features that can only be used with unofficial clients.

## Using the official client
If you are not interested in additional features and only want to connect with the most recent version of the official client, [Ogar](https://github.com/forairan/Ogar) is probably better suited for you. Cigar was [forked](https://en.wikipedia.org/wiki/Fork_(software_development)) from Ogar in order to add features not supported by the official client.

## Obtaining and Using
If you are on Windows, Cigar no longer requires an installation of node.js to run. Simply launch the batch file that is included to run the server. The rest of this section is for non Windows users.

As Cigar is written in Node.js, you must have Node.js and its "ws" module installed to use it (Unless you are using the Windows binary). You can usually download Node using your distribution's package manager (for *nix-like systems), or from [the Node website](http://nodejs.org). To install the "ws" module that is required, open up your system command line (cmd for windows, terminal for mac) and type "npm install ws". If you are on Linux, you can use the install script which would also automatically install node.js and ws. 

```sh
~$ git clone git://github.com/CigarProject/Cigar.git Cigar
~$ npm install ./Cigar
~$ npm start
```

Currently, Cigar listens on the following addresses and ports:
* *:88 - for the master server
* *:443 - for the game server

Please note that on some systems, you may have to run the process as root or otherwise elevate your privileges to allow the process to listen on the needed ports. **If you are getting an EADDRINUSE error, it means that the port required to run Cigar is being used. Usually, Skype is the culprit. To solve this, either close out skype, or change the serverPort value in gameserver.ini to a different port. You will have to change your connection ip to "127.0.0.1:PORT"**

Once the game server is running, you can connect (locally) by going to the agar.io website. Once the game is loaded, in your address bar, replace agar.io with javascript:connect("ws://127.0.0.1:443",""); and press enter.

## Configuring Cigar
Use "gameserver.ini" to modify Cigar's configurations field. Player bots are currently basic and for testing purposes. To use them, change "serverBots" to a value higher than zero in the configuration file. To add/remove bot names, edit the file named "botnames.txt" which is in the same folder as "gameserver.ini". Names should be separated by using the enter key.

## Custom Game modes
Cigar has support for custom game modes. To switch between game modes, change the value of "serverGamemode" in the configurations file to the selected game mode id and restart the server. The current supported game modes are:

Id   | Name
-----|--------------
0    | Free For All
1    | Teams
2    | Experimental (As of 6/13/15)
10   | Tournament
11   | Hunger Games
12   | Zombie Mode
20   | Rainbow FFA - Hint: Use with "setAcid(true)"

## Console Commands
The current available console commands are listed here. Command names are not case sensitive, but config settings are.

 - Addbot [Number]
   * Adds [Number] of bots to the server. If an amount is not specified, 1 bot will be added.
 - Ban [IP]
   * Prevents anyone with the banned IP from joining.
 - Banlist {clear}
   * Shows a list of currently banned IPs. You can clear the banlist by typing "clear" as the 2nd parameter.
 - Board [String 1] [String 2] [String 3] ...
   * Replaces the text on the leaderboard with the string text.
 - Boardreset
   * Resets the leaderboard to display the proper data for the current gamemode
 - Change [Config setting] [Value]
   * Changes a config setting to a value. Ex. "change serverMaxConnections 32" will change the variable serverMaxConnections to 32. Note that some config values (Like serverGamemode) are parsed before the server starts so changing them mid game will have no effect.
 - Clear
   * Clears the console output
 - Color [Player ID] [Red] [Green] [Blue]
   * Replaces the color of the specified player with this color.
 - Food [X position] [Y position] [Mass]
   * Spawns a food cell at those coordinates. If a mass value is not specified, then the server will default to "foodStartMass" in the config.
 - Gamemode [Id]
   * Changes the gamemode of the server. Warning - This can cause problems.
 - Kill [Player ID]
   * Kills all cells belonging to the specified player.
 - Killall
   * Kills all player cells on the map.
 - Mass [Player ID] [Number]
   * Sets the mass of all cells belonging to the specified player to [Number].
 - Playerlist
   * Shows a list of connected players, their IP, player ID, the amount of cells they have, total mass, and their position. 
 - Pause
   * Pauses/Unpauses the game.
 - Select [Server ID]
   * Selects the specified server, using an ID of 0 will select the master server. All commands will affect the selected server. Only available when the master server is running.
 - Status
   * Shows the amount of players currently connected, time elapsed, memory usage (memory used/memory allocated), and the current gamemode.
 - Tp [Player ID] [X position] [Y position]
   * Teleports the specified player to the specified coordinates.
 - Unban [IP]
   * Unbans the specified IP.
 - Virus [X position] [Y position] [Mass]
   * Spawns a virus cell at those coordinates. If a mass value is not specified, then the server will default to "virusStartMass" in the config.
   
The master server commands are differnet than the game server commands:
 - Add [Server IP] [Server Port] [Region Name]
   * Adds an existing server to the master server list
 - All {Command}
   * Executes the command on all game servers
 - Create [Region Name] [Game mode]
   * Creates a server and adds it to the master server list. 
 - Select [Server ID]
   * Same as the game server command.
 - Serverlist
   * Displays the list of servers that are connected, their ID, region, gamemode, and connected players.
 - Remove [Server ID]
   * Removes the selected server ID from the server list.

## Contributing
Please see [CONTRIBUTING.md](https://github.com/forairan/Ogar/blob/master/CONTRIBUTING.md) for contribution guidelines.

## License
Please see [LICENSE.md](https://github.com/forairan/Ogar/blob/master/LICENSE.md).
