# mf-fix
Applies MediaFoundation fixes to games running through Wine/Proton

Easily adds Media Foundation support to a Wine prefix. This project is heavily based on the scripts from z0z0z, https://github.com/z0z0z/mf-installcab and https://github.com/z0z0z/mf-install

The primary changes in this script are the ability for it to override the symbolic links Proton uses (which are not normally writeable by the user) and (optionally) automatically copying the mfplat.dll to the game's directory.

Example usage:
`./mf-fix.sh -e "/path/to/game/directory/" /path/to/wine/prefix/`

# Usage
Usage: mf-fix [OPTIONS] [PREFIX PATH]

Options:

    -v | --verbose : Enable verbose info messages

    -n | --noconfirm : Skip confirmation before utilizing sudo to override the symbolic links Proton uses in its prefixes (if that is needed)

    -e | --executable <PATH> : Path of the directory containing the executable of the game you are patching

    -h | --help : Print this help message


Proton tends to use symbolic links for the files inside its prefixes. These sym links tend to disallow write permissions to users, which is why sudo is utilized to overwrite those files.


Executable path can either lead to the executable or its containing folder. This is used at the end of the script to copy mfplat.dll to the game's directory. If this option is omitted, you will need to copy the dll into the game's directory yourself.


<PREFIX WPATH> is the path to the Wine prefix (the directory containing the 'drive_c' directory)

Absolute paths to the prefix are preferrable, I am unsure if relative paths will work properly for overwriting files


Exit codes:

    0 : Success

    1 : Unknown option

    2 : Invalid path given

    3 : Wine prefix path is not set

    4 : Given path does not appear to be a valid Wine prefix

    5 : Executable path does not exist

    6 : Attempting to get the directory containing executable at provided path resulted in a file path or a non-existant directory
    

# Notes
1) Currently, the verbose and no confirm options are not implimented

2) Since I was having a rough time understanding exactly how it works, this script currently uses the `installcab.py` file from the mf-installcab repository from z0z0z (https://github.com/z0z0z/mf-installcab). I would prefer to have it contained in a single file, so that is a planned change
