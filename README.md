# AMX Mod X — Console `amx_removeadmin` Utility

This small plugin adds a console command to remove an admin entry (by SteamID / IP / name fragment)
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

> **Important:** This plugin edits your admins file on disk. It *backs up* the file before modifying it.
> Test on a local server first and review the file path `ADMINS_FILE` in the source before using on production.

## How it works (summary)
1. The console command is registered via `register_concmd()` and accepts a single string argument.  
2. The plugin reads the admins file (path configurable), creates a backup, filters out any lines that match the provided identifier (SteamID/IP/substring match on name).  
3. Writes the filtered content back to the admins file.  
4. Calls a server console command to reload the admin list (default `amx_reloadadmins`) — update this if your server uses a different reload command.
5. Prints a console summary of how many lines were removed and where backup was saved.

## Files in this repo
- `src/admin_remove.sma` — Pawn source (paste into your `scripting/` before compiling)
- `README.md` — this file
- `LICENSE` — MIT
- `.gitignore` — ignore build artifacts

## Installation & Usage
1. Compile `admin_remove.sma` with AMX Mod X Dev 1.9.0 (or compatible build).
2. Copy the compiled `.amxx` into `addons/amxmodx/plugins/`.
3. Put the `admin_remove.cfg` config or use default path, or edit the `ADMINS_FILE` define inside the source to point to your admins file (common locations: `addons/amxmodx/configs/users.ini` or `addons/amxmodx/configs/admins.ini`).
4. From server console (RCON or local console), run:
```
amx_removeadmin "STEAM_1:0:12345678"
```
5. Check console output for backup path & reload confirmation.

## Safety notes & tips
- The plugin makes a timestamped backup file before modifying admins. Always review backups if something goes wrong.
- The matching is **case-insensitive** and will remove lines containing the provided string anywhere in the line. Use exact SteamID for safest results.
- If your server’s admin reload command differs from `amx_reloadadmins`, change the `RELOAD_CMD` define near the top of the Pawn file.

---
Made for reHLDS / AMX Mod X environments. Test locally before production use.