Lade die .NET-SDK hier herunter: https://dotnet.microsoft.com/en-us/download/dotnet/8.0
 
 # Workflow

* Ocaml Code in das F#-Projekt (z.B. in Assignment.ml) kopieren.
* Code mit Jetbrains Rider bearbeiten und Testen (in Program.fs oder mit F# Interactive)
* Code aus dem F#-Projekt in das Artemis Repository einfügen und pushen.

# Unterschiede zwischen OCaml und F#

* Die Parameter vieler binärer Operatoren (wie <, =, +, *) ... können in F# von unterschiedlichen Typen sein. In OCaml
  müssen sie vom gleichen Typ sein.
    * Bei den Vergleichsoperatoren (wie <, =, ...) gibt derzeit keine Kompatibilitätsprüfung in diesem Projekt. Die
      Typen der Operanden müssen beachtet werden. Spätestens beim Betrachten des zurückkopierten Codes in VSCode sollte
      man allerdings die Fehler sehen und ausbessern können.
    * Die arithmetischen Operatoren (wie +, *) wurden in `OcamlCompability.ml` überschrieben, sodass die sich wie in
      OCaml verhalten. Diese sollte
      am Anfang jeder anderen .ml oder .fs Datei mit `open OcamlCompability` eingebunden werden.
    * Außerdem wurden float Operatoren wie in OCaml in `OcamlCompability.ml` hinzugefügt.
* In F# brauchen die Elemente von Typdeklarationen anders als in OCaml keine `;` am Ende, wenn sie in unterschiedlichen
  Zeilen stehen. Der F#-Formatierer entfernt sie aber dennoch, auch bei .ml Dateien, obwohl bei
  diesen dadurch ein Fehler entsteht. Daher sollte man entweder die betroffenen Typdeklarationen in eine
  andere Datei verschieben (die man dann mit `open Dateiname` importieren kann) und diese nicht Formatieren oder nur den
  sicheren Teil der Datei formatieren, indem man diesen
  Teil markiert und dann "Reformat Selection" über die Context-Actions ausführt.
* F# hat strenge Standardregeln bezüglich der Einrückung von Kindausdrücken wie z.B. bei `match` und `if`. Diese kann
  man irgendwie ausschalten (siehe Fehlermeldung), deren Beachtung macht den Code aber besser lesbarer.

# Weitere Hinweise

* In Rider können .ml, .mli, .fs und .fsi Dateien im Kontextmenü hinzugefügt werden. Wähle Show all Files im
  Rider-Explorer in der Solution-Ansicht aus, um die Dateien zu sehen.
* Die Reihenfolge spielt in F# eine Rolle und kann in der Solution-Ansicht angepasst werden. In der Regel sollte sie von
  oben nach unten `OcamlCompability.ml > [evtl irgendwelche Dateien mit Typdeklarationen] > Assignment.ml > Program.fs` sein.
* Kompatibilität mit .ml und .mli Dateien erfordert eine bestimmte Konfiguration. Bei Interesse siehe `ocaml2.fsproj`
  für mehr
  Informationen.
* Die print-Methoden funktionieren nicht in .ml Dateien. Deswegen ist Program eine .fs Datei.
* Interface Definitionen (.mli, .fsi) werden auch unterstützt. Sie müssen in der Solution-Ansicht über der jeweiligen
  Implementierung stehen. Möglicherweise müssen dann Typannotationen auch in der Implementierung hinzugefügt werden,
  wenn sich der Typ, der in der Definition festgelegt ist, nicht aus der Implementation erschließen lässt.
