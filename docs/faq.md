# Häufige Probleme
## HTTPS funktioniert nicht unter Windows

Folgende Probleme können dazu führen:

### Die Zertifikate wurden unter Windows nicht generiert

!!! powershell ":zap:PowerShell"
    ```ps1
    mkcert -install
    ```
    Nach Ausführung des Befehls sollte das Verzeichnis `%LOCALAPPDATA%\mkcert` existieren und zwei Dateien beinhalten:
    ```
    📂 %LOCALAPPDATA%
    ┣╸📂 mkcert
    ┃  ┣╸📃 rootCA.pem
    ┃  ┗╸📃 rootCA-key.pem
    ```

### Der Zertifikatspeicher ist nicht in WSL verfügbar

Es kann sein, dass das Verzeichnis nicht korrekt in WSL gemappt wurde oder die Umgebungsvariable nicht richtig gesetzt ist.

!!! wsl "WSL"
    ```zsh
    echo $CAROOT
    ```
    Dieser Befehl sollte `/mnt/c/Users/<username>/AppData/Local/mkcert` ähnlich sehen. Ist dies nicht der Fall, so muss die Umgebungsvariable neu gesetzt werden.

!!! powershell ":zap:PowerShell"
    ```ps1
    setx CAROOT "$(mkcert -CAROOT)"; If ($Env:WSLENV -notlike "*CAROOT*") {setx WSLENV "CAROOT/up:$Env:WSLENV"}
    ```

### localhost ist unter Windows nicht auf die WSL weitergeleitet

--8<-- "includes/abbreviations.md"
