# Counter-Strike: Source LAN Surf Server with TAS

This is a small repository I've created to guide people on how to create a LAN server with Crash Forts TAS tools and a seamless offline surfing experience. See the note at the end for CSGO.

## Steps

1. Download SteamCMD from the Valve wiki: https://developer.valvesoftware.com/wiki/SteamCMD#Downloading_SteamCMD

2. Run SteamCMD as Administrator

3. Enter the following text in the following order:
- `force_install_dir C:\srcds`
- `login anonymous`
- `app_update 232330 validate`
- SteamCMD will now download the server files to the specified directory.

4. Once the download is finished, download the latest version of Metamod: https://www.sourcemm.net/downloads.php?branch=stable

5. Navigate to your recently created srcds directory, and open the `srcds\cstrike` folder.

6. Drop the entire `addons` directory from the Metamod download directly into your `srcds\cstrike` directory. If you've done it right, you should have `srcds\cstrike\addons`

7. Download the latest version of Sourcemod: https://www.sourcemod.net/downloads.php?branch=stable

8. Drop both the `addons` and the `cfg` directories from the Sourcemod download directly into your `srcds\cstrike` directory, once again.

9. Download this entire repository.

10. Drop the `addons` and the `cfg` directories from this repository into your `srcds\cstrike` directory, for the final time.

11. Go into the `srcds\cstrike\cfg` directory and rename either `server (trick).cfg` or `server (skill.cfg)` to just `server.cfg`, depending on which type of surf you want to play.

12. Now open Counter-Strike: Source, join a server and type `status` in console.

13. Copy your Steam ID. It should look like this: `STEAM_0:1:XXXXXX`

14. Navigate to the `srcds\cstrike\addons\sourcemod\configs` directory and open `admins_simple.ini`

15. Underneath the existing text, paste your Steam ID in quotation marks followed by `99:z` on the same line, if done correctly it should look like  this: `"STEAM_0:1:XXXXX" "99:z"`

16. Save `admins_simple.ini`

17. Navigate back to your root `C:\srcds` directory.

18. Right click `srcds.exe` and click `Create shortcut`

19. Right click the newly created shortcut, and click `Properties`.

20. In the target line, copy paste the following after the existing text: `srcds -console -game cstrike -insecure +sv_lan 1 +map de_dust`. Add `-tickrate 100` if you want to play tricksurf.
- If done right, the target line should look something like this: `C:\srcds\srcds.exe srcds -console -game cstrike -insecure +sv_lan 1 +map de_dust`

21. Add any maps you want to play from this repository by dropping them into the `srcds\cstrike\maps` directory: https://github.com/OuiSURF/Surf_Maps

22. Run the shortcut as admin, and your server should start! You can join the server by moving to the Local/LAN tab of your in-game server browser. 
- Note: You should open CSS before running the server, because Steam thinks that you are already running the game otherwise.

23. Type `!map mapname` in chat to change maps.
- Type `!god` in chat to remove fall damage. If you die you can type `!respawn`
- Some maps may require you to raise `sv_maxvelocity`
- Open the Source Tool Assist menu with `!sta` (more instructions below).
- Enable/Disable Autostrafe with `!strafe`
- Enable/Disable Speedometer with `!speedometer`
- You may need to load a map twice for it to generate a nav file.
- You may want to change default runspeed from `250` to `260` with `!rcon sm_rs_playerspeed 260`

## Included in this repo:
1. Source Tool Assist by Crash Fort, see guide on how to use here: https://github.com/crashfort/SourceToolAssist
- This plugin supports real-time run-rewinding and fast-forwarding with keybinds, bind keys to `+sm_rewind` and `+sm_fastforward`
- It also supports zoning, a timer, and replay bots. 
- This tool can also be used for non-TAS replay recording and run timing. Significantly more lightweight than a surftimer.
- If there's a render bug in the replay bot, you can fix this by typing `!cvar sv_force_transmit_ents 1` in chat. Only Sourcemod can change this cvar.

2. Tickrate enabler by daemon32: https://github.com/daemon32/tickrate_enabler
- Allows for the `-tickrate` launch option in the shortcut.

3. RNGfix by jason-e: https://github.com/jason-e/rngfix
- Vast improvements to RNG physics. For Trick.surf, uphill is disabled, but it probably won't make a difference in TAS. (Source: Frag).

4. Ramp bug fix by Gammacase & Momentum Mod: https://github.com/GAMMACASE/MomSurfFix
- Fixes surf ramp bugs.

5. Autobhop by Abner: https://forums.alliedmods.net/showthread.php?p=1869895
- Allows for autobunnyhopping.

6. Deluxe Godmode by DarthNinja: https://forums.alliedmods.net/showthread.php?p=979550
- Allows for the `!god` command. Typing `god` in console doesn't always work.

7. Autostrafe by CloudRick: https://forums.alliedmods.net/showthread.php?p=2080600
- Adds an `!strafe` command that enables or disables autostrafing 100% synchronised with your mouse movements.

8. HeadBugFix by Gammacase & Momentum Mod: https://github.com/GAMMACASE/HeadBugFix
- Fixes the head boundary box popping up when ducking.

9. Normalized Run Speed by sneak-it: https://github.com/sneak-it/Normalized-Run-Speed
- Normalizes run speed across all weapons. 
- You may want to change the default speed from `250` to `260`
- You can change this in the generated rngfix config file or with `!rcon sm_rs_playerspeed 260`

10. Speedometer by Zee: https://github.com/zSkyworld/zSkyworld
- Adds a simple velocity HUD with `!speedometer`

## CSGO:
These are all compatible with CSGO but you will need to adjust a few things.

1. Instead of `app_update 232330 validate` in SteamCMD, type `app_update 740 validate` in SteamCMD.

2. Remove the tickrate enabler and the bhop plugin as CSGO does not require these. 
- There's a separate enabler for CSGO here: https://github.com/zer0k-z/tickrate_enabler_csgo
- You only need this if you are going to run 85.3 or 102.4 tick. CSGO natively supports 64 and 128.

3. Add the following cvars to your `server.cfg`:
- `sv_clamp_unsafe_velocities 0`
- `sv_autobunnyhopping 1`
- `sv_staminajumpcost 0`
- `sv_staminalandcost 0`
- `sv_staminamax 0`
- `sv_staminarecoveryrate 0`
- `sv_accelerate_use_weapon_speed 0`
- Change `sv_friction` from `4` to `5.2`
- Change `sv_mincmdrate` and `sv_minupdaterate` to the desired tickrate.
- Change `sv_maxcmdrate` and `sv_maxupdaterate` to the desired tickrate + 1.
- Change `sv_minrate` to the desired tickrate x 1000.

6. Adjust the launch shortcut to say `-game csgo` instead of `-game cstrike`.

7. Add the Movement Unlocker plugin by Peace-Maker: https://forums.alliedmods.net/showthread.php?t=255298
