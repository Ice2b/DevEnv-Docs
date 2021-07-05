# Zusätzliche Einstellungen

## Powerlevel Fonts
Für die korrekte Darstellung von Glyphen in den Terminals ist es wichtig, dass die Schriftarten Glyphen beinhalten. Diese Schriftarten können über PowerShell nachinstalliert werden:
!!! powershell ":zap:PowerShell"
    ```ps1
    git clone https://github.com/powerline/fonts.git
    Set-ExecutionPolicy Bypass -Scope Process -Force; .\Fonts\install.ps1
    ```

## :material-linux: oh-my-zsh und Powerlevel10k

!!! wsl "WSL"
    Zuerst müssen [zsh](https://www.zsh.org/) und git installiert werden:
    ```zsh
    sudo apt install zsh git
    ```
    Danach kann oh-my-zsh über curl installiert werden:
    ```zsh
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
    ```
    Abschließend sollte zsh noch zur Standard-Shell gemacht werden:
    ```zsh
    chsh -s $(which zsh)
    ```
    Powerlevel10k ist ein Theme für oh-my-zsh, welches einige hilfreiche Dinge beinhaltet. Die [Dokumentation](https://github.com/romkatv/powerlevel10k) ist recht umfangreich.
    ```zsh
    git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
    ```
    Aktiviert wird das Theme, indem in der Datei `.zshrc` die Zeile `ZSH_THEME="robbyrussell"` zu `ZSH_THEME="powerlevel10k/powerlevel10k"` geändert wird.

## :material-linux: Zusätzliche Kommandos für DDEV

!!! wsl "WSL"
    Um nicht jedes Mal ```ddev exec php bin/console``` vor Symfony-Befehle schreiben zu müssen, bietet DDEV die Möglichkeit, eigene Kommandos zu definieren. Mit dem folgenden Befehl werden unter ~/.ddev/commands/web/ drei neue Kommandos erstellt (DDEV muss mindestens ein Mal gestartet worden sein):

    - ddev console: ddev exec php bin/console
    - ddev doctrine: ddev exec php bin/console doctrine:
    - ddev yarn: ddev exec yarn

    ```zsh
    echo 'H4sIAAAAAAAAA+3VT2+CMBgGcM58ik69Glv+SMLJw/YFluxkdqhQhQwKaesc337ABjNuGe6AzuT5XRrghTZNn5eokLrIhDUmWgt8vxlZ4NPjseU6zGIe9TzKWEA9izK69F2L0FFX9WmvDVeEWPqw/7Vu6PmNmt4tNqlcbLhObHs6JfdCRyotTVrIkDzuJdFVvi1kRaKPg0JSqdNYEJMIchCb5rbhqRSqeflJ850I+9L1NuM7/UzWXNVDU/DwxvMyq0smcSxe+8Kcv4hQSJOaakIKdfI0LiKj6inCmBteL1SEkRLciIltl0lJmuV3pbOVfe0NvTHd5o45x2D+Pfck/4w6HvJ/CWfnvzsodSzznMtYn9MJ+pcGW0FfeRryr37wvSRWRUnm8+0PnaBvGrPVtbf4X6u4kmPPMZR/x23z7wZLlwYsaP7/DmXI/yUM5r85IOdEva0bjHn3NcOz7Cja7e0DN1FSR7m9wJ8cAAAAAAAAAAAAAAAAAOBv3gEgZVTfACgAAA==' | base64 -d | tar zxf - -C ~/.ddev/commands/web/
    ```
