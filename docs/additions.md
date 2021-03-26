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
