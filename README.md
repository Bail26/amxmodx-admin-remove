# AMX Mod X — Console `amx_removeadmin` Utility

This plugin replaces your exisiting admin.amxx and adds a console command to remove an admin entry (non-immune) (by SteamID / IP / name fragment)
from the AMX Mod X admins file and requests a reload of the admin list so changes take effect immediately.

**Command (console-only):**
```
amx_removeadmin "STEAMID_or_IP_or_name_fragment"
```
Example:
```
amx_removeadmin "STEAM_1:0:12345678"
amx_removeadmin "1.2.3.4"
amx_removeadmin "SomePlayerName"
```

> **Important:** This plugin edits your admins file (users.ini) on disk. It *backs up* the file before modifying it.

## How it works (summary)
1. The console command is registered via `register_concmd()` and accepts a single string argument.  
2. The plugin reads the admins file (path configurable), creates a backup, filters out any lines that match the provided identifier (SteamID/IP/substring match on name).  
3. Writes the filtered content back to the admins file.  
4. Calls a server console command to reload the admin list (default `amx_reloadadmins`) — update this if your server uses a different reload command.
5. Prints a console summary of how many lines were removed and where backup was saved.

## Installation & Usage
1. Compile `admin.sma` with AMX Mod X Dev 1.9.0 (or any build).
2. Replace your originial admin.sma with one into `addons/amxmodx/plugins/`.
3. From server console (RCON or local console), run:
```
amx_removeadmin "STEAM_1:0:12345678"
```
5. Check console reload confirmation.

---
Made for Hlds/ reHLDS / AMX Mod X environments
