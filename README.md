# Starship

The following shows how I configured the Starship shell prompt for different OS.

Here is how it looks before and after adding the `starship.toml` file on Ubuntu.
![terminal_ubuntu](/img/terminal_ubuntu.png)

## Linux/WSL
### Install
```bash
:~$ curl -sS https://starship.rs/install.sh | sh
```
then add the following to `/.bashrc`
```bash
eval "$(starship init bash)"
```
### Configure
> It is important to have a [Nerd Font](https://www.nerdfonts.com/) installed otherwise the glyphs will not be visible. I use [Hack](https://github.com/ryanoasis/nerd-fonts/tree/master/patched-fonts/Hack) and [Source Code Pro](https://github.com/ryanoasis/nerd-fonts/tree/master/patched-fonts/SourceCodePro).

Create the configuration file `starship.toml` in the `~/.config/` folder:
```bash
:~$ mkdir -p ~/.config && touch ~/.config/starship.toml #create the folder and then create the file inside that folder
```

More details about the configuration can be found in the [official documentation](https://starship.rs/config/#prompt). Note also that some color are written using an [ANSI number](https://i.stack.imgur.com/KTSQa.png)

If you want to use mine, then just copy it into the `.config/` folder.

## Windows
### Install
Check the current version of PowerShell with `$PSVersionTable`. The steps below were used for version 5.1 and 7.4.1

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
<!-- PowerShell 5.1 -->
PS C:\Users\[username]> echo $PROFILE
C:\Users\[username]\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1
PS C:\Users\[username]> notepad $PROFILE
```

```powershell
<!-- PowerShell 7.4.1 -->
PS C:\Users\[username]> echo $PROFILE
C:\Users\[username]\Documents\PowerShell\Microsoft.PowerShell_profile.ps1
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


### Configure
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

Do not forget to add the reference in the PS profile `C:\Users\...\Microsoft.PowerShell_profile.ps1`
```
$ENV:STARSHIP_CONFIG = "$HOME\.config\starship.toml"
Invoke-Expression (&starship init powershell)
```

More details about the configuration can be found in the [official documentation](https://starship.rs/config/#prompt). Note also that some color are written using an [ANSI number](https://i.stack.imgur.com/KTSQa.png)
