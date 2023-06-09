# Starship

The following shows how I configured the Starship shell prompt for different OS.

## Linux/WSL
### Install
```bash
:~$ curl -sS https://starship.rs/install.sh | sh
```
then add the following to `./bashrc`
```bash
eval "$(starship init bash)"
```

## Windows
### Install
```powershell
 PS C:\Users\[username]> winget install --id Starship.Starship
```

#### PS setup
Make sure you can run scripts in PowerShell
```powershell
PS C:\Users\[username]> Get-ExecutionPolicy -List

        Scope ExecutionPolicy
        ----- ---------------
MachinePolicy       Undefined
   UserPolicy       Undefined
      Process       Undefined
  CurrentUser       Undefined
 LocalMachine       Undefined
PS C:\Users\[username]> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
PS C:\Users\[username]> Get-ExecutionPolicy -List

        Scope ExecutionPolicy
        ----- ---------------
MachinePolicy       Undefined
   UserPolicy       Undefined
      Process       Undefined
  CurrentUser    RemoteSigned
 LocalMachine       Undefined
```

add `Invoke-Expression (&starship init powershell)` to the PS profile
```powershell
PS C:\Users\[username]> echo $PROFILE
C:\Users\[username]\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1
PS C:\Users\[username]> notepad $PROFILE
```

or, if you want, create it as follows and then edit it
```powershell
PS C:\Users\[username]> if (!(Test-Path -Path $PROFILE)) {  New-Item -ItemType File -Path $PROFILE -Force }
```
#### Bash
insert the following in `~/.bashrc`
```bash
eval "$(starship init bash)"
```

If you do not have the file `/.bash_profile` or `~/.bash_login`, you will receive a warning saying you are missing those files and that one of them will be created for you.


## Configure
> It is important to have a [Nerd Font](https://www.nerdfonts.com/) installed otherwise the glyphs will not be visible. I use [Hack](https://github.com/ryanoasis/nerd-fonts/tree/master/patched-fonts/Hack) and [Source Code Pro](https://github.com/ryanoasis/nerd-fonts/tree/master/patched-fonts/SourceCodePro).

Create the configuration file `starship.toml` in the `~/.config/` folder:
```bash
:~$ mkdir -p ~/.config && touch ~/.config/starship.toml #create the folder and then create the file inside that folder
```

or 
```powershell
PS C:\Users\[username]> New-Item -Path 'C:\Users\[username]\.config' -ItemType Directory
PS C:\Users\[username]> New-Item -Path 'C:\Users\[username]\.config\starship.toml' -ItemType File
```

More details about the configuration can be found in the [official documentation](https://starship.rs/config/#prompt). Note also that some color are written using an [ANSI number](https://i.stack.imgur.com/KTSQa.png)