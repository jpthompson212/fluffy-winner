# Machine Setup tips/tricks

> In all the following paths make sure to update <user> to your Windows username

## Installs

- scoop (package manager/isntaller)

    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
    ```

- git (version control)
- VSCode (editor)
- eza (better ls)
- corretto21-jdk (java dev kit)
- oh-my-posh (pretty terminals)
- git (for scoop and everything else)
- everything-alpha (god tier search)
- FiraCode Nerd Font (go to nerd font)
- clink (improvements to cmd)
- docker (along with WSL2)
- 7-zip
- windirstat (visual storage)
- winscp (ssh file transfers)
- sysinternals
  - process-explorer
  - procmon
  - sysmon
  - zoomit

    ```sh
    scoop install git
    scoop bucket add extras
    scoop bucket add nerd-fonts
    scoop bucket add sysinternals
    scoop bucket add java
    scoop bucket add versions
    scoop install vscode
    scoop install eza
    scoop install oh-my-posh
    scoop install everything-alpha
    scoop install FiraMono-NF
    scoop install clink
    scoop install 7zip
    scoop install zoomit
    scoop install process-explorer
    scoop install procmon
    scoop install sysmon
    scoop install windirstat
    scoop install winscp
    scoop install corretto21-jdk
    ```

- Run `C:\Users\<user>\scoop\apps\7zip\current\install-context.reg`
- Run `C:\Users\<user>\scoop\apps\vscode\current\install-context.reg`

## Setting up Terminal

- add nerd font to powershell and cmd profiles

- add gitbash to terminal
  - Duplicate powershell profile
  - Rename that profile to git-bash
  - Change the executable shell to `C:\Users\<user>\scoop\apps\git\current\bin\bash.exe`
  - Change icon to `C:\Users\<user>\scoop\apps\git\current\mingw64\share\git\git-for-windows.ico`

- open powershell and run `notepad $PROFILE`
  - Add the following to that file and save it.

    ```sh
    oh-my-posh init pwsh --config 'C:\Users\<user>\scoop\apps\oh-my-posh\current\themes\cinnamon.omp.json' | Invoke-Expression
    function My-Func {
            [alias('ls')]
            param(
                [string]$Path # path for ls
            )
            eza.exe -lab --group-directories-first --git --icons $Path
    }
    ```

- open git-bash profile
- Open your .bashrc file from 'C:\Users\<user>'
- Add the following to that file and save it.

```sh
eval "$(oh-my-posh init bash --config /c/Users/<user>/scoop/apps/oh-my-posh/current/themes/cinnamon.omp.json)"
```

- add `alias ls="eza.exe -lab --group-directories-first --git --icons Path"` to your ~/.bashrc file

- open command prompt profile
  - Open a command prompt
  - Make a file called 'doskey_macros.txt' at %USERPROFILE%
    - Add this content to that file `ls = eza.exe -lab --group-directories-first --git --icons $1`
  - Run `clink autorun install --allusers` in cmd
  - Run `clink info` and then in your 'scripts' directory make a file named 'oh-my-posh.lua'
  - In that file add the following:

  ```sh
  load(io.popen('oh-my-posh --config="C:/Users/<user>/scoop/apps/oh-my-posh/current/themes/cinnamon.omp.json" --init --shell cmd'):read"*a"))()
  ```

  - Run the following to add the ls alias
 
  ```
  reg add "HKCU\Software\Microsoft\Command Processor" /v Autorun /d "doskey /macrofile=\"C:\Users\<user>\doskey_macros.txt\"" /f
  reg query "HKCU\Software\Microsoft\Command Processor" /v Autorun
  ```

## Setup WSL

- Run `wsl --install -d Ubuntu`
- open an ubuntu terminal
- Run `sudo apt install zsh`
- Run `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`
- Run `curl -s https://ohmyposh.dev/install.sh | bash -s -- -d ~ -t ~`
- Add `eval "$(~/oh-my-posh init zsh --config ~/themes/cinnamon.omp.json)"` to ~/.zshrc
- Follow instructions [here](https://github.com/eza-community/eza/blob/main/INSTALL.md) to install eza
- Add `alias ls="eza -lab --group-directories-first --git --icons $Path"` to the ~/.zshrc
