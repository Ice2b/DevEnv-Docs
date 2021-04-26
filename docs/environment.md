# Installation der Entwicklungsumgebung
Nachdem die [Vorbereitung](preparations.md) abgeschlossen ist, kann nun die Entwicklungsumgebung eingerichtet werden.

## Prüfen der Voraussetzungen

Bevor ddev installiert wird, sollte einmal geprüft werden, ob auch alles funktioniert hat.

!!! wsl "WSL"
    === "Zertifikatsspeicher"
        Hier sollte in der Ausgabe der Windows-Pfad stehen (also etwas in der Art: ```/mnt/c/Users/<username>/AppData/Local/mkcert```)
        ```zsh
        echo $CAROOT
        ```
    === "Docker"
        Hier sollte in der Ausgabe die Docker-Version angezeigt werden (Docker version 20.10.5, build 55c4c88)
        ```zsh
        docker -v
        ```

## ddev installieren
In WSL werden nun gcc und DDEV installiert:

!!! wsl "WSL"
    ```zsh
    brew install gcc && brew tap drud/ddev && brew install ddev
    ```

## ngrok installieren
!!! wsl "WSL"
    ```zsh
    cd /tmp
    wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip
    sudo unzip ngrok-stable-linux-amd64.zip -d /usr/local/bin
    ```

## PHPStorm installieren
Die aktuellste Version kann [hier](https://www.jetbrains.com/de-de/phpstorm/download/download-thanks.html?platform=linux) gefunden werden. Der Download kann abgebrochen werden, der Link zur Datei findet sich unter der Überschrift.
!!! wsl "WSL"
    ```zsh
    cd /tmp
    wget https://download.jetbrains.com/webide/PhpStorm-2020.3.3.tar.gz
    sudo tar -xzf PhpStorm-*.tar.gz -C /opt --one-top-level=PhpStorm --strip-components=1
    sudo ln -s /opt/PhpStorm/bin/phpstorm.sh /usr/local/bin/phpstorm
    ```
    Ab jetzt kann phpstorm durch den Befehl ```phpstorm``` überall gestartet werden. Es empfiehlt sich jedoch, einen Alias anzulegen:
    ```zsh
    echo alias phpstorm='phpstorm ./ nosplash </dev/null &>/dev/null &' >> ~/.bash_aliases
    ```
    Dieser startet PhpStorm im Hintergrund mit dem aktuellen Verzeichnis und verwirft alle Aus- und Eingaben aus stdin/stdout.

## Grafische Umgebung vorbereiten
!!! info "GWSL"
    Die einfachste Variante ist wahrscheinlich [GWSL](https://opticos.github.io/gwsl/). Diese App muss nur installiert werden (aus dem Windows-Store oder von Git) und funktioniert dann direkt.
    Hierzu sollte die [Dokumentation](https://opticos.github.io/gwsl/help.html) bei Problemen konsultiert werden.

Um Fenster aus der WSL heraus anzeigen zu können, müssen noch einige Schritte vollzogen werden:

* X-Server unter Windows installieren ([VcXsrv](https://sourceforge.net/projects/vcxsrv/), [X410^:euro:^](https://x410.dev/), [MobaXterm^:euro:^](https://mobaxterm.mobatek.net/))
* Server in WSL-Umgebung bekannt machen

!!! wsl "WSL"
    Abhängigkeiten installieren:
    ```zsh
    sudo apt update && sudo apt install libatk1.0 libatk-bridge2.0 libxtst6 libxi6 libpangocairo-1.0 libcups2 libnss3 xdg-utils
    ```
    Die Information über den Server zur Profidatei in WSL hinzufügen:
    ```zsh
    echo DISPLAY=$(awk '/^nameserver/ {print $2; exit;}' </etc/resolv.conf):0.0 >> ~/.profile
    ```

## Zusätzliche Einstellungen in PhpStorm
PhpStorm lauscht auf IPv6, was ein Problem für XDebug darstellt. Dies kann unter
Help --> Edit custom VM options geändert werden. In der sich öffnenden Datei muss am Ende `#!java -Djava.net.preferIPv4Stack=true` hinzugefügt werden.

--8<-- "includes/abbreviations.md"
