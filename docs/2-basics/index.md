# Unser Erstes Repository

[Vorheriges Kapitel](/git-workshop/1-prep/) | [Zurück zur Übersicht](/git-workshop/) | [Nächstes Kapitel](/git-workshop/3-merge-requests/)

**Um gleich mal richtig loszulegen, legst du dir ein Übungs-Repository an. Wir
beschäftigen uns hier mit den Basis-git-Befehlen.**

## Git Sagen, Wer Du Bist

Bevor wir irgendetwas tolles mit git anstellen, müssen wir dem Programm erst mal
bekannt machen, mit wem es da überhaupt zu tun hat. Vielleicht weißt du schon,
dass git ein System zur Versionskontrolle (engl. Version Control System, VCS)
ist. Angenommen du arbeitest an Code, der durch git verwaltet wird, dann kannst
du jederzeit den aktuellen Stand der Code Base festhalten, also eine
Momentaufnahme machen. Diese Momentaufnahme wird dann von git gespeichert,
zusammen mit der Information, wer diesen Schnappschuss wann erstellt hat. Damit
git also weiß, wer da vorm Rechner sitzt, hinterlegst du deine Daten. Das
Terminal hast du ja sicher schon offen?

```bash
git config --global user.name "Wladimir Workshopteilnehmer"
git config --global user.email "wowl1234@hs-karlsruhe.de"
```

Wichtig ist dabei, dass du als E-Mail-Adresse die Adresse hinterlegst, mit der
du dich auch bei GitHub angemeldet hast. So kann GitHub deine Arbeit auch mit
deinem Account verknüpfen. Dir ist vielleicht der Zusatz `--global` aufgefallen.
Damit legst du die systemweite Einstellung fest. git erlaubt es dir auch, in
verschiedenen Projekten verschiedene Adressen und Namen zu nutzen, z. B. wenn du
für die Arbeit oder die Uni andere Accounts verwenden musst. Dazu später mehr.

Falls du mal wissen musst, welche Werte du hinterlegt hast, kannst du die
Einstellungen mit folgenden Befehlen einsehen:

```bash
git config --global user.name
git config --global user.email
```

## Ein Projekt, Erst Mal Ohne Git

Okay, git kennt uns. Dann kümmern wir uns jetzt mal um ein Projekt, mit dem wir
arbeiten können. Um alles so einfach wie möglich zu halten, lassen wir erst mal
die Finger von Java-, Python- oder sonstigem Code. Stattdessen legen wir uns ein
git-Tagebuch mit simplen Text-Dateien an:

```bash
cd ~
mkdir git-diary
cd git-diary
```

Kurze Erläuterung: Du begibst dich in dein Heimverzeichnis, legst einen neuen
Ordner für unser Tagebuch-Projekt an und öffnest diesen Ordner. Er ist, da wir
ihn gerade erst erstellt haben, natürlich leer. Lass uns das ändern.

> Wir benutzen hier jetzt einen Weg, eine Datei rein über die Kommandozeile
> anzulegen. Das ist natürlich für "richtige" Projekte nicht sehr praktisch, da
> willst du natürlich mit einem gescheiten Editor arbeiten. Du kannst auch gerne
> den gerade erstellten Ordner in einem Texteditor deiner Wahl (Visual Studio
> Code, Sublime, Notepad, Eclipse, irgendwas von JetBrains, etc.) öffnen, wenn
> dir das lieber ist. Für git bleiben wir aber erst mal im Terminal.

Wir erzeugen uns eine Text-Datei mit dem Namen `entry_1.txt` unterhalb des
Projekt-Verzeichnisses, die einen kurzen Satz enthält.

```bash
echo "Das ist mein erster Tagebucheintrag." > entry_1.txt
```

Du kannst dir jetzt gerne die Verzeichnisliste sowie den Dateiinhalt anzeigen
lassen, um dich davon zu überzeugen, dass das geklappt hat.

```bash
ls
cat entry_1.txt
```

Jetzt haben wir ein Tagebuch-Projekt, sowie darin unseren ersten Eintrag. Wie du
siehst, sind das einfach nur Ordner und Dateien auf deinem Computer. **Daran
ändert sich auch nichts, wenn wir gleich git benutzen.** Deine Verzeichnisse und
Dateien bleiben immer Verzeichnisse und Dateien.

## Aus dem Projekt ein Repository machen

Der Begriff **Repository** ist im Rahmen dieses Workshops neu. Als Repository
(auf deutsch einfach nur Aufbewahrungsort oder Lager) bezeichnen wir ein von git
verwaltetes Verzeichnis. Damit aus einem langweiligen Verzeichnis ein mit
Superkräften ausgestattetes Repository wird, reicht ein einfacher git-Befehl:

```bash
git init
```

Wenn du diesen Befehl ausgeführt hast, wird außer der Ausgabe "Initialized empty
Git repository..." nicht viel passiert sein. Aber wenn du mit `ls -a` versteckte
Dateien anzeigen lässt, siehst du, dass neben deiner Tagebuch-Datei ein
`.git`-Verzeichnis angelegt wurde. In diesem Verzeichnis musst du nichts
machen. git managed alles für dich.

Was machen wir also als erstes mit unserem schicken Repository? Erst mal den
Status checken.

```bash
git status
```

Mit diesem Befehl kannst du jederzeit den aktuellen Zustand deines Repositorys
abfragen. Lass uns die Ausgabe dieses Befehls Zeile für Zeile durchgehen:

> `On branch master`

Wir befinden uns aktuell auf dem branch (Zweig) `master`. Okay. Merken wir uns.
Erst mal nicht so wichtig.

> `No commits yet`

Es gibt noch keine Commits. Commits sind die Momentaufnahmen des Zustands eines
Projekts, über die wir eingangs schon gesprochen haben. Da wir noch keine
Momentaufnahme gemacht haben, sind git auch noch keine bekannt. Logisch. Wie du
dir vielleicht denken kannst, gibt es git-Befehle zum Erstellen eines solchen
Schnappschusses. Die werden wir gleich kennen lernen.

> `Untracked files:`
>
> `(use "git add <file>..." to include in what will be committed)`
>
> `    entry_1.txt`

Git hat unseren Tagebucheintrag also schon gefunden, meldet aber aktuell noch,
dass diese Datei nicht getrackt wird. D. h., git verwaltet diese Datei noch
nicht für uns. Außerdem spoilert git hier schon, was wir als nächstes machen
müssen.

> `nothing added to commit but untracked files present (use "git add" to track)`

Hier fasst git netterweise nochmal den Status zusammen. Außerdem werden wir
nochmals darauf hingewiesen, was wir machen müssen, wenn wir unseren
Tagebucheintrag mit git verwalten wollen. Dann machen wir das mal.

## Die erste Datei committen

Bevor wir gleich unseren ersten Commit machen, sollten wir noch über die
**Staging Area** reden. Die Staging Area ist ein Bereich, in dem du Änderungen
an diversen Dateien sammeln kannst, bevor du sie dann in einem Schnappschuss
festhältst. Falls du eine Metapher dazu brauchst: Du ziehst um, und räumst dein
Bücherregel aus. Die Bücher räumst du in Umzugskartons. Dabei achtest du darauf,
die von dir sorgsam ausgearbeitete Anordnung nicht kaputt zu machen. Du räumst
alle Thriller in eine Box, alle Fantasy-Bücher in eine andere, und eine ganz
große Kiste füllst du mit Fachbüchern über Informatik. Möglicherweise mistest du
einige in die Jahre gekommene Bücher aus oder entscheidest dich um. Die Kisten
sind deine Staging Area, die geduldig darauf warten, dass du mit ihrem, von dir
zusammengestellten Inhalt zufrieden bist. Wenn du eine Kiste als "fertig
gepackt" empfindest, machst du einen Deckel drauf, und die Umzugshelfer nehmen
die gesamte Kiste und räumen sie in den Umzugsvan. Du kannst jetzt (im Rahmen
dieser Metapher) keine Änderungen mehr am Inhalt dieser Kiste vornehmen. Der
Vorgang des Deckel-drauf-und-ab-ins-Auto ist der Commit.

Übertragen auf die Software-Entwicklung erlaubt dir die Staging Area, an
mehreren Stellen in einer Code Base zu arbeiten, dann aber nur die Dateien
zusammen zu commiten, die etwas miteinander zu tun haben. So sind deine Beiträge
zu Coding-Projekten (hoffentlich) nachvollziehbar, atomar und ohne seltsame
Nebeneffekte an Stellen, wo man sie nicht erwartet.

Gennug der Theorie. Wir haben unseren Tagebucheintrag und wollen ihn committen.
Fügen wir ihn also unser Staging Area hinzu. Das machen wir mit dem
`add`-Befehl.

```bash
git add entry_1.txt
```

Du gibst an, welche Datei der Staging Area hinzugefügt (denglisch "geaddet")
werden soll. Schauen wir uns den aktuellen Status an.

```bash
git status
```

Okay, wir sind immer noch auf dem master-Branch. Darum kümmern wir uns wie
gesagt später. Wir haben auch immer noch keine Commits. Aber wir sind ja gerade
dabei, das zu ändern. Jetzt wird es aber interessant: Da steht "changes to be
committed", gefolgt von einem Eintrag "new file: entry_1.txt". Unser Eintrag ist
also in der Staging Area gelandet. Die Datei ist in der Umzugskiste. Machen wir
jetzt also den Deckel drauf uns räumen sie in den Umzugswagen.

```bash
git commit -m "Add first entry"
```

Auch wenn das jetzt relativ unspektakulär aussieht, haben wir gerade unseren
ersten Commit gemacht. Nice. Das `-m` ist die Kurzversion von `--message` und
erlaubt es uns, eine Commit-Message anzugeben. **Bitte vergib immer sinnvolle
Commit-Messages**. Das ist wirklich wichtig. Es gehört aber zu jeder
erfolgreichen Informatik-Karriere, dass man in studentischen oder persönlichen
Projekten mal so Commit-Messages wie "Changed things", "this works but I don't
know how" oder "Mama sagt es gibt Essen" verfasst. Achte aber einfach darauf,
möglichst gut zu beschreiben, welche Änderungen du mit diesem Commit
festhältst, und leg pro Projekt eine Sprache für Commit-Messages fest. 

Wenn du jetzt noch mal `git status` ausführst, siehst du, dass wir uns auf dem
master-Branch befinden (Überraschung) und nichts zu committen haben, unser
"working tree" ist "clean". Das heißt: Der Zustand aller lokalen Dateien im
Repository entspricht dem Stand, der in git festgehalten ist.

Nun gibt es einen praktischen Befehl, der dir deine Commit-Historie
übersichtlich darstellt:

```bash
git log
```

Diese Historie enthält aktuell nur einen Commit, der dich als Autor ausweist und
den genauen Zeitstempel enthält; außerdem deine Commit-Message. Wenn du also
wissen willst, wer in einem git-Repository zuletzte gearbeitet hat, hilft dir
ein Blick auf `git log`.

## Ein Projekt auf GitHub anlegen und mit einem lokalen Repository verknüpfen

// TODO

* privates repo anlegen
* Remote festlegen und pushen
* Bedeutung lokal und remote

## Änderugen von Remote ins lokale Repository holen

// TODO

* Übertragene Dateien in GitHub anschauen und bearbeiten (neuer Commit)
* Lokal: git status / git pull / git status / git log / cat entry_1.txt

## Branches erstellen

// TODO

* mit cleanem Stand lokal
* git checkout -b my-branch git status / create file entry_2.txt / git add / git commit /
  git push -> neuer Branch! Achtung
* Switch zwischen den Branches lokal und auf GitHub


## Kontrollfragen

Erst überlegen, dann nachschauen!

<details>
<summary>Was ist ein Repository?</summary>
Als Repository bezeichnet man ein von git verwaltetes Verzeichnis.
</details>
<details>
<summary>Was ist ein Commit?</summary>
Ein Commit ist eine Momentaufnahme des Projekts zu einem bestimmten Zeitpunkt. Er enthält neben den Dateien des Projekts selbst auch Meta-Informationen wie den Autor und den Zeitpunkt.
</details>

## Zusammenfassung

* Wir haben ein git-Repository erstellt.
* Wir haben eine Datei committed.
* Wir haben ein Projekt auf GitHub angelegt und unser lokales Repository dorthin
  übertragen.
* Wir haben mit einem zweiten Commit auf GitHub das Prinzip von lokalen und
  remote Repositories nachvollzogen sowie uns `push` und `pull` angesehen. 
* Wir haben einen Branch angelegt, dort eine zweite Datei committed und beides
  nach GitHub übertragen und dort angeschaut.

Unser Repository hat jetzt zwei Zweige. Toll. Was bringt das? Weiter geht's mit
Teil 3!

[Vorheriges Kapitel](/git-workshop/1-prep/) | [Zurück zur Übersicht](/git-workshop/) | [Nächstes Kapitel](/git-workshop/3-merge-requests/)