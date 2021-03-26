# Vorbereitende Schritte

Im ersten Schritt werden einige hilfreiche Tools installiert:

* Windows Terminal
* Chocolatey
* mkcert

## Windows Terminal installieren

**Aus dem Microsoft-Store:**

Im [Microsoft-Store](https://aka.ms/terminal) ist  das Programm verfügbar.

**Von GitHub:**

Aus dem [GitHub-Repo](https://github.com/microsoft/terminal/releases) kann Windows Terminal installiert werden, wenn kein Zugriff auf den Windows Store besteht. Diese Version muss allerdings manuell aktuell gehalten werden.

## Chocolatey installieren

Chocolatey ist ein Paketmanager für Windows.
Installiert wird er über die administrative PowerShell. Diese kann über ++windows+x++ gestartet werden.

!!! powershell ":zap:PowerShell"
    ```ps1
    Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
    ```

## SSL-Zertifikate vorbereiten
mkcert generiert die lokalen ssl-Zertifikate im Windows Zertifikatspeicher, die später von DDEV genutzt werden.
Dafür werden in einem zweiten Schritt die Umgebungsvariablen gesetzt, damit die WSL-Umgebung den Zertifikatsspeicher von Windows nutzt.

In der administrativen PowerShell (++windows+x++) folgende Befehle ausführen:
!!! powershell ":zap:PowerShell"
    ```ps1
    mkcert -install
    setx CAROOT "$(mkcert -CAROOT)"; If ($Env:WSLENV -notlike "*CAROOT*") {setx WSLENV "CAROOT/up:$Env:WSLENV"}
    ```

## homebrew in der WSL
Innerhalb der WSL muss homebrew installiert werden. Dazu wird sie gestartet:
!!! powershell "PowerShell"
    ```ps1
    wsl -d <Umgebungsname>
    ```
In der WSL-Konsole wird nun homebrew installiert:

!!! warning "Achtung"
    Homebrew sollte in ```/home/linuxbrew/.linuxbrew``` installiert werden.

!!! wsl "WSL"
    ```zsh
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

Nach der Installation muss ```brew``` noch so eingerichtet werden, dass es auch nach einem Neustart noch verfügbar ist:
!!! wsl "WSL"
    ```zsh
    test -d /home/linuxbrew/.linuxbrew && eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)
    test -r ~/.bash_profile && echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.bash_profile
    echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.profile
    ```
