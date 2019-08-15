# RegSLScan
A command line tool for scanning registery key permissions. 

Made by Henri Aho with Microsoft Visual Studio Community Edition 2017.

# Background
This tool was inspired by a recent Steam local privilege escalation issue patched in Aug 13th 2019.

The issue was caused by a background service, Steam Client Service, that on startup gave non-admins 
full access to ```HKLM\Software\Valve\Steam``` and it's subkeys. Users could delete one of the subkeys
and then create a symbolic link with same name as the deleted subkey and link it to a restricted registery key. 
This would cause the Steam Client Service to grant users full access on the symbolic link' target subkey
compromising system security.

This tool was created to find similiar vulnerabilities in other programs and services.

# Features
This tool scans registery keys under Local Machine (HKLM) and lists out any keys non-admins have access to create symbolic links in.
With the list developers and security enthusiasts may search for similar vulnerabilities in their systems Steam had prior to Aug 13th 2019 patch.

# Usage
RegSlScan is intended to be run from a commandline console.

Commandline syntax examples:
```
RegSlScan.exe
RegSlScan.exe Software\Valve
```

If no commandline parameters are given. RegSLScan scans all subkeys in Local Machine (HKLM) recursively.
If a parameter such as "Software\Valve" is given, the speficied key (under HKLM) and it's subkeys are scanned instead.



# Example output
```
> .\RegSLScan.exe Software
Searching for keys non-admins can create symbolic links in...
Software\Blizzard Entertainment
Software\Epic Games
Software\EpicGames\Unreal Engine\4.0
Software\Microsoft\DRM
Software\Microsoft\Speech_OneCore\AudioPolicy
Software\Microsoft\Speech_OneCore\CloudPolicy\OneSettings
Software\Microsoft\Speech_OneCore\CloudSettings
Software\Microsoft\Speech_OneCore\Settings\OnlineSpeechPrivacy
...
```