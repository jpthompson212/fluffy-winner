# Machine Setup tips/tricks

## Installs

- scoop (package manager/isntaller)
- VSCode (editor)
- eza (better ls)
- oh-my-posh (pretty terminals)
- git (for scoop and everything else)
- everything search
- FiraCode Nerd Font
- Clink (improvements to cmd)
- Docker (along with WSL2)
- Install 7-zip
  - Run `C:\Users\JThompson\scoop\apps\7zip\current\install-context.reg`

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
    oh-my-posh init pwsh --config C:\Users\<user>\scoop\apps\oh-my-posh\current\themes\cinnamon.omp.son' | Invoke-Expression
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
eval "$(oh-my-posh init bash --config /c/Users/JThompson/scoop/apps/h-my-posh/current/themes/cinnamon.omp.json)"
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
  load(io.popen('oh-my-posh --config="C:/Users/<user>/scoop/apps/h-my-posh/current/themes/cinnamon.omp.json" --init --shell cmd'):read"*a"))()
  ```
  