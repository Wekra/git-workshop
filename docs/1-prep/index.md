# Alles Wichtige Vorbereiten

[Zurück zur Übersicht](/git-workshop/) | [Nächstes Kapitel](/git-workshop/2-basics)

**Wir installieren alle nötigen Programme und erstellen uns einen
GitHub-Account, den wir dann noch gemeinsam einrichten.**

## Git installieren

> Wenn du git bereits installiert hast, und weißt wie du es im Terminal aufrufen
> kannst (d. h. die Eingabe `git --version` produziert keinen Fehler, sondern
> gibt die Versionsnummer zurück), kannst du diesen Teil überspringen.

### Für Windows

Git kannst du für Windows auf der offiziellen
[Git-Download-Seite](https://git-scm.com/download/win) herunterladen. Nach dem
Download startest du die Installation mit einem Doppelklick auf die Datei. Dabei
kannst du in sämtlichen Schritten einfach immer die Voreinstellung bestätigen.
Wer eine Schritt-für-Schritt-Anleitung mit Screenshots möchte, findet diese bei
[Heise Tipps&Tricks](https://www.heise.de/tipps-tricks/Git-auf-Windows-installieren-und-einrichten-5046134.html).

Öffne die frisch installierte *Git Bash* und tipp den folgenden Befehl ein:

```bash
git --version
```

Die Ausgabe sollte die Angabe einer Git-Version sein.

### Für Mac

Mac-Nutzer können einfach ein Terminal öffnen und dort eingeben:

```bash
git --version
```

Wenn das Programm nicht installiert ist, erscheint eine Abfrage, die dir
anbietet, git für dich zu installieren. Probiere dann obigen Befehl erneut. Du
solltest die installierte git-Versionsnummer zurück erhalten.

### Für Linux

Installiere git über den Paket-Manager deiner Linux-Distribution. Für
Debian-basierte Systeme (z. B. Ubuntu) ist dies:

```bash
sudo apt install git
```

Nach der Installation solltest du mit der Eingabe von

```bash
git --version
```

die installierte Verionsnummer angezeigt bekommen.

## Ein Wort zum Terminal

Wir verbringen in diesem Workshop viel Zeit auf der Kommandozeile (die Begriffe
Kommandzeile, Command Line Interface (CLI) und Terminal verwenden wir hier
synonym). Falls der Umgang damit für dich noch etwas ungewohnt ist, halb so
wild. Freunde dich mit ihr an, denn sie ist enorm praktisch für die tägliche
Arbeit beim programmieren. Hier kurz die wichtigsten allgemeinen Befehle, die du
in diesem Workshop gebrauchen kannst:

```bash
pwd
```

Mit dem Befehl `pwd` (print working directory) erfährst du, wo im Dateisystem du
dich gerade befindest.

```bash
cd  pfad/zu/einem/verzeichnis
```

Mit dem `cd`-Befehl (change directory) wechselt du in ein Verzeichnis. In
welches, das hängt davon ab, was du hinten dran schreibst. Mit dem Befehl `cd ~`
gelangst du übrigens jederzeit in dein Heimverzeichnis.

```bash
ls
```

Mit dem List-Befehl `ls` listest du die im aktuellen Verzeichnis enthaltenen
Dateien und Unterordner auf. Profis nutzen `ls -l` für eine Anzeige der Inhalte
in Listenform und `ls -a`, um auch versteckte Dateien anzuzeigen.

```bash
cat eine_datei.txt
```

Der `cat`-Befehl ist eine einfache Möglichkeit, den Inhalt von Dateien zu sehen.

## GitHub-Account einrichten

Wir nutzen in diesem Workshop GitHub als zentrale Plattform. Viele von euch
haben dort schon einen Account. Super. Diesen könnt ihr einfach nutzen. Wenn ihr
noch keinen Account habt, könnt ihr euch unter
[github.com/join](https://github.com/join) einfach einen anlegen.

## SSH-Key anlegen und benutzen

> Falls ihr auch schon einen SSH-Key bei GitHub für euren aktuellen Computer
> hinterlegt habt, könnt ihr diesen Schritt ebenfalls überspringen.

Damit wir git und GitHub in Kombination möglichst effektiv nutzen können,
brauchen wir noch eine kleine Sache: Einen SSH-Key. Wenn ihr nicht genau
versteht warum wir ihn brauchen, was er ist und wie er funktioniert, ist das für
den Anfang nicht besonders schlimm. Kurz gesagt ist das für eine zentrale
Git-Repository-Verwaltung wie GitHub eine Möglichkeit zu überprüfen, dass Code,
der über euren Account hochgeladen wird, auch wirklich von eurem Computer kommt.
Und zwar ohne dass ihr jedes Mal euren GitHub-Nutzernamen und Passwort angeben
müsst.

### SSH-Key Anlegen

Um einen SSH-Key (genauer: ein SSH-Schlüsselpaar) zu erstellen, benutzen wir das
Terminal und starten im Heimverzechnis:

```bash
cd ~
```

Sie mit dem Befehl `ls -a` nach, ob das Verzeichnis `.ssh` existiert. Wenn ja,
hast du vermutlich schon mal einen SSH-Key angelegt unfd findest in diesem
Verzeichnis zwei Dateien:

```bash
cd .ssh

ls -a
  id_rsa
  id_rsa.pub
```

Falls nicht, umso besser. Dann kannst du dir jetzt einen nagelneuen Schlüssel
anlegen:

```bash
ssh-keygen -t ed25519 -C "die-mail-adresse-deines-github-accounts@email.com"
```

Dieser Befehl fragt dich ein paar Dinge. Zunächst möchte er wissen, wo das
Schlüsselpaar gespeichert werden soll. Hier kannst du mit `Enter` den
voreingestellten Pfad übernehmen. Dann kannst du noch ein Passwort vergeben und
bestätigen. Wir empfehlen dir **im Rahmen dieses Workshops**, kein Passwort zu
vergeben. Dieses musst du ansonsten nämlich bei jeder Interaktion mit GitHub
eingeben, was die ganze Sache unnötig verkompliziert und in die Länge zieht.
Bitte sieh das aber nicht als allgemeingültige Empfehlung!

Vergiss bitte nicht, die Mail-Adresse in den Anführungszeichen durch die zu
ersetzen, mit der du dich bei GitHub registriert hast.

Das `-t ed25519` bestimmt übrigens, welche Verschlüsselung für deinen neuen Key
zum Einsatz kommt. Manchmal findest du auch alternative Anleitungen mit
folgendem Befehl:

```bash
ssh-keygen -t rsa -b 4096 -C "die-mail-adresse-deines-github-accounts@email.com"
```

Das ist auch okay, statt ED25519 wird hier RSA mit einer Länge von 4096 Bit
verwendet. Beides ist nach aktuellem Ermessen sehr sicher. Hey, Kryptographie in
Action! Aber wir schweifen ab.

Nachdem du diesen Befehl zu Ende ausgeführt hast, befinden sich in deinem
`.ssh`-Verzeichnis nun zwei Dateien, genannt `id_ed25519` und `id_ed25519.pub`
oder, wenn du den zweiten Befehl genommen hast, `id_rsa` und `id_rsa.pub`. Die
Endung `.pub` steht für *public*, die ist der öffentliche Schlüssel, den du
weitergeben darfst und auch gleich an GitHub weitergeben wirst. Die erste Datei
ohne Endung ist dein privater Schlüssel. Sie sollte deinen Computer niemals
verlassen.

Abschließend müssen wir den SSH-Key noch unserem `ssh-agent` bekannt machen.
Dieses Programm übernimmt für uns später im Hintergrund die Authenifizierung.

```bash
ssh-add ~/.ssh/id_ed25519
```

bzw.

```bash
ssh-add ~/.ssh/id_rsa
```

Fertig. Jetzt müssen wir GitHub nur noch mitteilen, welchen Schlüssel wir da
gerade erstellt haben; und dass es unserer ist.

### SSH-Key bei GitHub hinterlegen

Wenn ihr nach eurer Registrierung noch bei GitHub angemeldet seid, führt euch
der Link auf [github.com/profile/settings](https://github.com/settings/profile)
zu eurer Account-Einstellungs-Seite. Dort gibt es links den Punkt **SSH and GPG
keys**. Nach einem Klick darauf habt ihr oben rechts die Möglichkeit, über **New
SSH Key** einen neuen Schlüssel hinzuzufügen. Als Titel könnt ihr einen
möglichst aussagekräftigen Namen eintragen, z. B. *MacBook Fabian* oder
*Arbeits-Laptop*, damit ihr wisst, zu welchem Gerät der Schlüssel gehört. Nun
müssen wir noch den Schlüssel selbst hinzufügen.

Angenommen du befindest dich noch im gerade genutzten `.ssh`-Verzeichnis
(überprüfe das gerne mit `pwd`), kannst du dir den Inhalt deines öffentlichen
Schlüssels mit `cat` anzeigen lassen:

```bash
cat id_ed25519.pub
```

bzw 

```bash
cat id_rsa.pub
```

Dieser beginnt mit `ssh-ed25519` oder `id-rsa` und endet mit deiner
Mail-Adresse. Dazwischen befindet sich eine lange, zufällige Zeichenkette.
Koiere das *alles* in das **Key**-Feld bei GitHub und speichere danach mit einem
Klick auf **Add SSH Key**. Das war's!

<details>
<summary>SSH? ED25519? `ssh-add`? Hä?</summary>
Falls dir nicht genau klar ist, was da gerade passiert ist, mach dir nichts
draus. Da ist ein notwendiger Schritt, um effizient mit GitHub (bzw. mit jedem
Git-Anbieter da draußen) arbeiten zu können. Das hat nicht wirklich was mit git
direkt zu tun, ist aber als Vorbereitung nötig. Wir werden uns im Rest des
Workshops nicht mehr wirklich damit befassen. (Außer du hast ein Passwort für
deinen Schlüssel vergeben, dann wünschen wir dir viel Spaß beim Tippen...)
Spätestens in einer Kryptographie-Vorlesung werden dir SSH und das
Public/Private-Key-Verfahren aber wieder über den Weg laufen. Für Interessierte:
[Wikipedia über das Public-Key-Verfahren](https://de.m.wikipedia.org/wiki/Public-Key-Authentifizierung).
</details>

## Zusammenfassung

* Wir haben Git installiert und wissen, wie wir es in einem Terminal aufrufen
  können.
* Wir kennen die wichtigsten Befehle zum Navigieren und Anzeigen im Terminal:
  `pwd`, `cd`, `ls` und `cat`.
* Wir haben einen GitHub-Account.
* Wir erstellten einen SSH-Key, um unseren Computer für GitHub "freizuschalten".

Jetzt können wir richtig loslegen :)

[Zurück zur Übersicht](/git-workshop/) | [Nächstes Kapitel](/git-workshop/2-basics)