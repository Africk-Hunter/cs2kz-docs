# Setting Up A LAN Server

There are 4 steps for setting up a CS2KZ **LAN** server:

1. [Server Setup](#server-setup): Setting up the actual server itself.
2. [Metamod Setup](#metamod-setup): Installing and setting up Metamod: Source.
3. [KZ Plugins](#kz-plugins): Adding essential plugins to make KZ work properly.
4. [Maps](#adding-maps): Adding KZ maps to the server.

<br>

> [!WARNING]
> This guide is for **ONLY** for windows devices

## Server Setup

### 1. Folder Preparation

1. Create a folder called ``cs2kz_server`` on the drive you want the server to be on.

2. Inside of ``cs2kz_server`` create another folder called ``steamcmd``

>[!DANGER]
> Note that the folder which will be used for the server is **REQURIED** to be on a drive with a least
> ``35GB`` of free space!

>[!NOTE]
> The main folder (``cs2k_server``) can be named anything you want, the name given in this guide is to make the rest of the
> instructions more simple.

### 2. Installing SteamCMD

1. Navigate to the [SteamCMD Download Page](https://developer.valvesoftware.com/wiki/SteamCMD#Downloading_SteamCMD).

2. Under step ``[1]`` click the download link to download the ``zip`` file.

3. Extract the contents of the ``zip`` into the ``steamcmd`` folder.



### 3. Installing the Server

1. Locate ``SteamCMD.exe`` in the folder it was extracted to and run it. It will install all of the required Steam components.

2. Once it's done, type ``login anonymous`` in the terminal that was opened and press enter.

3. Next type in ``app_update 730 validate`` and press enter. This will begin the installation of the server and may take a very long time
depending on your internet and drive speeds.

>[!DANGER]
> Do **NOT** close the terminal until it outputs ``Success! App '730' fully installed.``!

### 4. Adding a Steam GSLT Token

1. Navigate to [Steam GSLT Tokens](https://steamcommunity.com/dev/managegameservers) (log in with steam if you aren't already).

2. At the bottom under `Create a new game server account` set the App ID as ``730`` and click ``Create``

3. Keep this window open as we will need the token for the next step.

### 5. Running the Server

1. Navigate back to the ``cs2kz_server`` folder and create a new file called ``start.bat``.

2. Right click ``start.bat``, click ``Edit``, and add this text into it:

```txt
cd ".\steamcmd\steamapps\common\Counter-Strike Global Offensive\game\bin\win64\"
start cs2.exe -dedicated +map de_dust2 +sv_setsteamaccount YOUR_TOKEN_HERE
```
> [!WARNING]
> Ensure that you replace ``YOUR_TOKEN_HERE`` with your Steam GSLT Token.

3. You should now be able save the file, close the text editor, and run it by double-clicking on it. It should run a terminal.
If you get a prompt to give CS2 access through your firewall, press yes.

### 6. Connecting to the Server

> [!WARNING]
> You have to run your own game before running the server, otherwise it will not let you launch your game!

You can connect to the server by either:

1. Opening the in-game Community Server Browser and navigating to the ``LAN`` tab, and pressing connect on the server

OR

2. Opening the in-game console and typing in ``connect localhost``

## Metamod Setup

### Installing Metamod: Source

1. Open [Metamod: Source (Dev 2.0x) Downloads](https://www.sourcemm.net/downloads.php/?branch=master) and download the
latest Build for your operating system (Windows/Linux).

2. You should have downloaded a ``zip`` (Windows) or ``tar.gz`` (Linux) file, extract it and move the whole ``addons`` folder into 
the ``\csgo\`` folder of the server.

> [!INFO]  
> The `\csgo\` folder can be found in:
> ```FilePath
> \cs2kz_server\steamcmd\steamapps\common\Counter-Strike Global Offensive\game\
>```
> If you have followed this guide exactly as explained.

3. Open the ``gameinfo.gi`` file in a text editor (such as notepad), the file can be found in the same ``\csgo\`` folder.

4. Ignore any warnings about editing the file, and add:
```txt
Game    csgo/addons/metamod
```
to the top of the section with similar inputs (see image below), and save the file.<br><br>
When complete, it should look like this:

<button onclick="document.getElementById('gameinfo-image').classList.toggle('shown')" class='gameinfoButton'>Example Image</button>

<img id="gameinfo-image" class='hidden' src="/images/gameinfo.png">

## KZ Plugins

### Installing the KZ Plugin

1. Open [cs2kz-metamod releases](https://github.com/KZGlobalTeam/cs2kz-metamod/releases) and download the latest ``(pre-) release`` for your operating system.

2. Extract the ``zip`` (Windows) or ``tar.gz`` (Linux), then drag the ``addons`` and ``cfg`` folders into the ``\csgo\`` folder (The same folder used in the [Metamod Setup](#metamod-setup) step).

### Installing Optional Plugins

#### Jumpstat/Quake sounds support

1. Open [MultiAddonManager](https://github.com/Source2ZE/MultiAddonManager/releases) Releases and download the latest release for your operating system (Windows/Linux).

2. Extract the ``zip`` (Windows) or ``tar.gz`` (Linux), then drag the ``addons`` and ``cfg`` folders into the ``\csgo\`` folder.

#### Database Support

1. Open [SQLMM's Releases](https://github.com/zer0k-z/sql_mm/releases) and download the latest release for your operating system (Windows/Linux).

2. Extract the ``zip`` (Windows) or ``tar.gz`` (Linux), then drag the ``addons`` and ``cfg`` folders into the ``\csgo\`` folder.

#### Language Support

1. Open [GetClientCvarValue's](https://github.com/komashchenko/ClientCvarValue/releases) Releases and download the latest release for your operating system (Windows/Linux).

2. Extract the ``zip`` (Windows), then drag the ``addons`` and ``cfg`` folders into the ``\csgo\`` folder.

## Maps

1. Open up [Steam Workshop](https://steamcommunity.com/workshop/browse/?appid=730&searchtext=kz_) and look for a map or collection of maps

2. Edit the ``start.bat`` (created in [Server Setup](#server-setup)) and add either ``+host_workshop_map`` or ``+host_workshop_collection`` command along with the
``ID`` of the map/collection to the 2nd row on the file. If you've followed this guide exactly as instructed it should look something like this:

```AddingMap
cd ".\steamcmd\steamapps\common\Counter-Strike Global Offensive\game\bin\win64\"
start cs2.exe -dedicated +map de_dust2 +sv_setsteamaccount GSLT_TOKEN +host_workshop_map MAP_ID
```

or

```AddingCollection
cd ".\steamcmd\steamapps\common\Counter-Strike Global Offensive\game\bin\win64\"
start cs2.exe -dedicated +map de_dust2 +sv_setsteamaccount GSLT_TOKEN +host_workshop_collection COLLECTION_ID
```

Replacing ``MAP_ID``/``COLLECTION_ID`` with the correct ID & ``GSLT_TOKEN`` with your token.

> [!INFO]
> Although maps can be manually added into files, ``FastDL`` does not exist for CS2, so using workshop instead is recommended.

> [!WARNING]
> Currently the CS2 Workshop doesn't require you to use a GSLT token for maps, but this could change in the future.