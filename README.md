#Description:
Cfg Console Variables anomaly happens time by time, and caused by Valve bug:
values can not be read from cfg-files and remains by default if you reach some limit
of the number of lines in server.cfg / or cfg-files in total / or by chance.

This problem is described more in the topic: https://forums.alliedmods.net/showthread.php?t=307696

Also, this plugin check:
- if some cfg files contain wrong values that exceed max/min value allowed or max. length.
- unused (non-existent) ConVars.
- duplicated ConVars.
#Commands:
- "sm_convar_anomaly_show" - to compare values in cfg files with actual in-game Cvar to find anomalies/unused cvars.
- "sm_convar_anomaly_fix" - to attempt to fix Cvar anomalies (log will be short - only info about fixes).

By default, log-file is located at "addons/sourcemod/logs/CVar_Anomaly.log"
#Settings (ConVars):
- "convar_anomaly_autofix" - fix Cvar anomaly automatically before each map start? (0 - off, 1 - on {default}).
- "convar_anomaly_roundstart" - Do additional check/fix on each round start (0 - Disabled, 1 - Enabled)
- "convar_anomaly_fix_nondefault" - Include all convars in fix even those who have non-default value, but different from cfg (0 - Fix default values only, 1 - Fix all)
- "convar_anomaly_server_last" - 0 - process cfg files in default Valve order [server.cfg go first], 1 - broke rules and overwrite convars by server.cfg file). This include files in 'convar_cfg_files_include'
- "convar_cvar_check_areas" - Areas to check for (-1 - All, 1 - difference in values, 2 - nonexistent convars, 8 - overflows, 16 - duplicate convars)
- "convar_anomaly_logpos" - where to write log? (1 - client conlose, 2 - server console, 4 - file, 1+2+4=7 - all places).
- "convar_cfg_files_include" - if you need more cfg-files to process, place them here, separated by star (*)
- "convar_cfg_files_exclude" - if you need exclude some cfg-files from processing, place them here, separated by star (*)
- "convar_cvar_names_exclude" - if you need concrete ConVars to exclude from processing, place them here, separated by star (*)
#Warning: some plugins / game specifically change its ConVars in-game process, so the final report is not necessarily accurate.

#Using:
TODO.
For most cases, it's enough just to copy .smx file to addons/sourcemod/plugins
#Conflicts:
Map configs plugins:
- Extended Map configs by Milo, - if you using it, you have to set "convar_anomaly_roundstart" to 0
- Map configs from berni - incompatible at all
- some plugins may start to throw an error "Cannot create entity when no map is running". Fix for this error should come from plugin authors, not me.
#Recommended plugins:
[ANY] Restart empty server
#Credits:
Silvers - for initial parser and nice plugins I studied on.
hmmmmm - for floating point operation tips.
Neuro Toxin - for raw IsNumeric() function
#Related plugins:
Buffer Overflow Fixer - Good to fix Cvar on earlier stage than my plugin, but require DHooks extensions and SM 1.8+
Cvar Configs Updater - good for commenting unused convars in cfg files to decrease probability of issue