# Inhalt <!-- omit in toc -->

- [1. Abstract](#1-abstract)
- [2. Vorüberlegungen](#2-vorüberlegungen)
- [3. Text finden](#3-text-finden)
  - [Text vorbereiten](#text-vorbereiten)
- [4. Text analysieren](#4-text-analysieren)
  - [Automatische Analyse](#automatische-analyse)
  - [Manuelle bw. semi-automatische Analyse](#manuelle-bw-semi-automatische-analyse)
    - [Figuren identifizieren](#figuren-identifizieren)
    - [Zwischenergebnis 1](#zwischenergebnis-1)
    - [Verfeinerung des Zwischenergebnisses](#verfeinerung-des-zwischenergebnisses)
    - [Zwischenergebnis 2](#zwischenergebnis-2)
    - [Zwischenergebnis 3](#zwischenergebnis-3)
    - [Verfeinerung der PER-Liste](#verfeinerung-der-per-liste)
    - [Kurzer Exkurs zu Worthäufigkeiten](#kurzer-exkurs-zu-worthäufigkeiten)
    - [Verteilung der Figuren über den Text](#verteilung-der-figuren-über-den-text)
    - [Aussagen über Figuren erheben](#aussagen-über-figuren-erheben)
- [5. Figurenverzeichnis aus Ergebnissen der Textanalyse erstellen](#5-figurenverzeichnis-aus-ergebnissen-der-textanalyse-erstellen)
  - [Erweiterungen](#erweiterungen)
    - [XML-Ressource erstellen (statt Tabelle)](#xml-ressource-erstellen-statt-tabelle)
- [6. Übertragbarkeit auf andere Forschungsinteressen](#6-übertragbarkeit-auf-andere-forschungsinteressen)

# 1. Abstract

Das Forschungsdesign "korpusbasierte Textanalyse" zeigt beispielhaft das Zusammenspiel der verschiedenen Dienste und Ressourcen, die von CLARIAH-DE angeboten werden. Die Aufgabe ist es, ein Verzeichnis der in einem Roman auftretenden Figuren zu erstellen. Daraus entstehen die folgenden Teilaufgaben
- Roman in digitaler Form finden (s. [Text finden](#3-text-finden))
- Text automatisch annotieren lassen, um u. a. Personen (= Figuren) finden zu können (s. [Text analysieren](#4-text-analysieren))
- Anhand von Konkordanzen und Ko-Okkurrenzen Beschreibungen der Figuren generieren
- Aus den Personen und den Beschreibungen ein Verzeichnis erstellen (s. [Figurenverzeichnis erstellen](#5-figurenverzeichnis-aus-ergebnissen-der-textanalyse-erstellen))

Die hier dargestellte Vorgehensweise ist auf jede Forschungsfrage übertragbar, in der Begriffe dadurch bestimmt werden sollen, dass die Häufigkeit und der Ko-Text der auf sie verweisenden Ausdrücke analysiert werden. Hierauf wird im [letzen Abschnitt](#6-übertragbarkeit-auf-andere-forschungsinteressen) noch einmal eingegangen.

# 2. Vorüberlegungen

Das Figurenverzeichnis soll neben den Namen der Figuren auch Ausschnitte aus dem Text präsentieren, die die jeweilige Figur möglichst gut charakterisieren.

TODO:
- evtl. weitere Absichten ergänzen
  - Netzwerk
  - Metadaten aus anderen Quellen (z. B. GND) etc.)
    - GND-Abfrage basteln
      - curl https://lobid.org/gnd/search?q=Heidi -o "test_heidi_gnd.txt" findet zwar allerhand Zeug, darunter auch Verweise auf das Buch, mir ist aber noch nicht gelungen, die Abfrage auf die Figur "Heidi" zu beschränken
      - Laut Wikipedia kann der Entitätentyp "Person" (Kürzel: "p") weiter unterteilt werden, wobei literarische Figuren als "pxl" codiert werden (s. https://de.wikipedia.org/wiki/Gemeinsame_Normdatei#Entit%C3%A4tencodierung")
      - wie dies als Filter eingesetzt wird, habe ich aber noch nicht verstanden
      - 

# 3. Text finden
TODO:
- beschreiben, welche Art Date
- die großen Möglichkeiten nennen und eine daraus auswählen
  - TextGrid
  - DTA

## Text vorbereiten
Es bietet sich an, einen Roman in Kapitel zerlegt zu analysieren, da dies z. B. erlaubt, das Auftreten und die Charakterisierung von Figuren im Verlauf der Handlung zu beschreiben. Die Zerlegung in Kapitel folgt dabei der Überlegung, dass die Einteilung in Kapitel in konventionellen Romanen in einer Beziehung zum Handlungsfortschritt steht. Dies kann beim ausgewählten Text unterstellt werden, da er eine fortschreitende Handlung erzählt, also z. B. keines der Kapitel einen Rückblick auf vorangegangene Ereignisse bietet.

Die Zerlegung von reinem Text ist je nach Größe auch manuell recht schnell machbar, wenn hierfür ein Text-Editor zur Verfügung steht, der die Suche nach regulären Ausdrücken erlaubt. <a name="texteditor">In Frage kommen z. B.</a> [Sublime Text](https://www.sublimetext.com/), [Notepad++](http://notepad-plus-plus.org/) oder [VS Code](https://code.visualstudio.com/). Um bequem nach den Kapitelanfängen und -enden suchen zu können, ist es von großem Vorteil, die Titel der Kapitel zu kennen. Eine kurze Suche bei z. B. [Projekt Gutenberg](https://www.projekt-gutenberg.org/spyri/heidi1/index.html) (oder einer Bibliothek der Wahl) bringt bereits ein brauchbares Ergebnis:


{% include image.html url="images/heidi_kapitel_projekt_gutenberg.png" description="Inhaltsverzeichnis von _Heidi_ auf der Webseite von _Projekt Gutenberg_" %}


TODO: regex (.+\n)+ erläutern. Auf Tutorials zu Regex verweisen (auch auf Testumgebungen wie https://regexr.com/, https://regex101.com/)
Die Suche nach den einzelnen Kapiteln lässt sich als regulärer Ausdruck nun folgendermaßen formulieren:

`[Titel des zu findenden Kapitels][Zeilenumbruch][beliebiger Text][Titel des folgenden Kapitels][Zeilenumbruch]`

Suche nach dem Kapitel "Fräulein Rottenmeier hat einen unruhigen Tag":

`Fräulein Rottenmeier hat einen unruhigen Tag\n(.+\n)+Im Hause Sesemann geht's unruhig zu\n`

Der Text-Editor findet nun sowohl die beiden Kapitel-Titel als auch allen Text dazwischen. Das Suchergebnis kann bequem kopiert und in eine neue Datei eingefügt werden. Um die Reihenfolge der Kapitel auch bei der späteren Analyse verwenden zu können, sollten die Dateinamen eine fortlaufende Kapitelzählung enthalten, also z. B. `heidi_kap_1_zum-alm-oehi-hinauf.txt`

# 4. Text analysieren

Die Analyse des Textes wird in zwei großen Schritten durchgeführt, die jeweils eine Anzahl von Teilschritten enthalten. Der erste große Schritt ist die [automatische Analyse](#automatische-analyse), an dessem Ende der Text in annotierter, also mit Zusatzinformation versehener, Form vorliegt. Um Personenbezeichnungen automatisch erkennen zu können, muss der Text in einzelne Wortformen (= Tokens) zerlegt werden. Es bietet sich an, auch eine Lemmatisierung durchzuführen, also jede Wortform mit der Zusatzinformation zu versehen, von welcher Grundform sie abgeleitet wurde: Das Lemma der Worform _ging_ ist in diesem Sinne _gehen_. Im Anschluss folgt die _named entity regocnition_ (NER), die neben Institutionen auch Personenennamen erkennt und markiert. Im [zweiten Schritt](#manuelle-bw-semi-automatische-analyse) werden die Zusatzinformationen dazu genutzt, die im Roman vorkommenden Figuren zu identifizieren. Für die 

## Automatische Analyse

TODO: 
- Tokenisierung, Lemmatisierung, NER beschreiben (evtl. einfach mit Screenshots)
- mehr als nur Weblicht für Annotation zeigen? (Hinweis reicht vielleicht, mit Screenshot der Diensteliste)
- Weblicht-Abfragen

Für die automatische Annotation von Text steht eine [Vielzahl von Werkzeugen](https://www.clariah.de/ueber-uns/diensteliste) zur Verfügung. Unsere Forschungsfrage erfordert es, den annotierten Text durchsuchen zu können. Zusätzlich zu den Annotationswerkzeugen benötigen wir also auch eine zusätzliche Software, die dies leistet. Da es fas so viele Ausgabeformate von Annotationswerkzeugen gibt wie Werkzeuge selbst, bietet es sich an, bei der Suche nach geeigneter Software gleich im Blick zu behalten, dass der annotierte Text nur ein Zwischenergebnis ist. Eine der bequemsten Möglichkeiten, die alle Anforderungen erfüllt, ist der Service [WebLicht](https://weblicht.sfs.uni-tuebingen.de/weblichtwiki/index.php/Main_Page), der für Angehörige von Forschungseinrichtungen kostenlos genutzt werden kann. Für sehr große Korpora, also z. B. Zeitungskorpora, die aus Tausenden von Einzeltexten bestehen können, sind andere Dienste eventuell besser geeignet. Die Annotation kann zwar durchaus auch bei einer Vielzahl an Texten über [WebLicht as a service](https://weblicht.sfs.uni-tuebingen.de/WaaS/) realisiert werden, es ist in einem solchen Fall jedoch vorteilhaft ein anderes (evtl. selbst gehostetes) Korpusverwaltungssystem zu nutzen (z. B. [CQPweb](https://cwb.sourceforge.io/cqpweb.php)).






## Manuelle bw. semi-automatische Analyse

TODO:
- Strategie für Weiterverarbeitung beschreiben
  - irgendwas mit häufigste Figuren werden weiterbehandelt oder so
    - Korrekturmöglichkeiten der Liste prüfen (manuelle Annotation als Tabelle oder so? In die dann auch Textkenntnis einfließen kann oder nicht. Textkenntnis evtl. über Metadatenabfrage von Bibliotheken oder Inhaltsangaben oder so)

### Figuren identifizieren
Das annotierte Korpus kann direkt in WebLicht oder in [TüNDRA](https://weblicht.sfs.uni-tuebingen.de/Tundra/), der _Tübingen aNnotated Data Retrieval Application_ genutzt werden. 

{% include image.html url="images/tundra_upload_tcf_annotated_corpus.png" description="Upload eines eigenen Korpus im TCF-Format in TÜNDRA" %}

Nach dem Upload können über die Suchanfrage `[_ne="PER"]` alle Wörter angezeigt werden, die als _Person_ (Tag: _PER_) erkannt wurden. Zur verwendeten Anfragesprache gibt es ein [kleines Handbuch](https://weblicht.sfs.uni-tuebingen.de/Tundra/help) und ein [Tutorial](https://weblicht.sfs.uni-tuebingen.de/Tundra/tutorial).

{% include image.html url="images/tundra_query_per.png" description="Suchanfrage, um alle mit _PER_ annotierten Wörter zu finden" %}

Das Ergebnis der Suchanfrage wird u. a. als Konkordanz dargestellt, also als eine Liste der gefundenen Wörter und ihren Fundstellen.

{% include image.html url="images/tundra_result_conc_query_per.png" description="Konkordanz aller als _PER_ getaggten Wörter. Als Umgebung des Suchausdrucks wird der Satz angezeigt, in der er gefunden wurde." %}

Die Suchergebnisse werden auch als aggregierte Liste dargestellt. Als Standardeinstellung gibt WebLicht hier lediglich die Gesamtanzahl der Fundstellen an. Über die Option _Add/Remove Columns_ kann die Darstellung verfeinert werden:

{% include image.html url="images/tundra_refine_stats_query_per.png" description="Spalte *_ne* und _token_ in der Statistik-Tabelle hinzufügen." %}

Werden weitere Spalten hinzugefügt, werden die ausgewählten Kategorien in der Zählung berücksichtigt.

{% include image.html url="images/tundra_result_refined_stats_query_per.png" description="Anzeige, welche Wörter als _PER_ getaggt wurden und wie häufig sie im Korpus auftreten." %}

### Zwischenergebnis 1

Die Liste aller als _PER_ getaggten Wörter ist die Grundlage für das Figurenverzeichnis. Da sie auf Token, also Wortformen beruht, werden manche Namen in flektierter Form extra aufgelistet (z. B. "Heidi" und "Heidis"). Ein bereinigtes Figurenverzeichnis könnte also so aussehen:
* Heidi
* Rottenmeier
* Sesemann
...

### Verfeinerung des Zwischenergebnisses

Da es sich bei "Rottenmeier" und "Sesemann" um Nachnamen handelt, wäre es von Vorteil, hier noch einen Vornamen oder zumindest eine Anredeform hinzuzufügen. Ein Blick in die Konkordanzen von `[token="Rottenmeier"]` zeigt, dass "Rottenmeier" praktisch immer ein "Fräulein" vorausgeht. Diese These kann überprüft werden, indem die Suchabfrage um ein vorangestelltes "Fräulein" erweitert wird. In der hier verwendeten Anfragesprache wird dies realisiert, indem die Anfragen nach "Fräulein" und "Rotttenmeier" in der richtigen Reihenfolge durch einen Punkt verknüpft werden: `[token="Fräulein"] . [token="Rottenmeier"]`

{% include image.html url="images/tundra_fraeulein_rottenmeier_query_and_result.png" description="Suchergebnisse für _Fräulein Rottenmeier_." %}

Allerdings stimmt die Anzahl der Fundstellen nicht überein: "Rottenmeier" kommt 135 mal im Korpus vor, "Fräulein Rottenmeier" jedoch nur 127 mal. Es muss also acht Okkurrenzen von "Rottenmeier" geben, denen ein anderes Wort als "Fräulein" vorangeht. Um diese zu finden, muss also die Suchanfrage `[token="Fräulein"] . [token="Rottenmeier"]` so manipuliert werden, dass alle Okkurrenzen von _Nicht "Fräulein" gefolgt von "Rottenmeier"_ gefunden werden. Als Suchanfrage formuliert sieht das so aus: `[token!="Fräulein"] . [token="Rottenmeier"]`. Die Kombination aus Ausrufezeichen und Gleichheitszeichen wird als "nicht gleich" interpretiert. Das Ergebnis der Anfrage ist:

{% include image.html url="images/tundra_not_fraeulein_rottenmeier_query_and_result.png" description="Suchergebnisse für Nicht &quot;Fräulein&quot; gefolgt von &quot;Rottenmeier&quot;." %}

Da nun alle 135 Vorkommen von "Rottenmeier" geprüft sind, kann der Eintrag im Figurenverzeichnis in "Fräulein Rottenmeier" geändert werden. 

Dieselben Schritte gilt es nun für "Sesemann" und alle anderen potenziellen Einträge vorzunehmen. Da die These "Rottenmeier" bezieht sich immer auf "Fräulein Rottenmeier" nur aufgrund von Vorwissen über den Text aufgestellt werden kann, bietet es sich, eine allgemeinere Anfrage zu formulieren, die einfach alle Wörter anzeigt, die direkt vor "Sesemann" auftreten und auch die Flektionsform "Sesemanns" berücksichtigen, die ja laut PER-Liste zweimal im Text auftritt. Da TüNDRA (bzw. auch der in WebLicht eingebaute Viewer) reguläre Ausdrücke unterstützt, ist es relativ einfach, eine Suchanfrage zu formulieren, die sowohl "Sesemann" als auch "Sesemanns" findet und statt "Fräulein" jedes beliebige Token davor als Ergebnis zurückliefert: `[token=/.+/] . [token=/Sesemann(s)?/]`. Die runden Klammern im Suchausdruck nach "Sesemann" erzeugen eine Gruppe (hier bestehend aus dem Buchstaben _s_) und das Fragezeichen legt fest, dass diese Gruppe "0 oder einmal" auftreten darf. 

{% include image.html url="images/tundra_any_token_sesemann_query_and_result.png" description="Suchergebnisse für _beliebige Buchstabenkette gefolgt von 'Sesemann'_" %}

Die Tabelle unter "Statistics" zeigt, welche Wörter wie oft vor "Sesemann" auftreten. Wir wissen nun also, dass die Einträge im Figurenverzeichnis um "Frau Sesemann", "Herr Sesemann" und "Klara Sesemann" erweitert werden können. Der folgende Ausschnitt aus den Konkordanzen zeigt eine Form im Genitiv und eine Verwendung einer Phrase die "Hause Sesemann" enthält. "Hause" und "Hauses" gehen "Sesemann" insgesamt elf Mal voraus. Es gibt also mindestens elf Fundstellen für "Sesemann(s)", die nicht direkt einer der Figuren zugeordnet werden können. Für das folgende Zwischenergebnis spielt dies erst einmal keine Rolle.

### Zwischenergebnis 2

1. Heidi
2. Fräulein Rottenmeier
3. Herr Sesemann
4. Frau Sesemann
5. Klara Sesemann

Diese Liste zeigt nicht nur, dass die Vorgehensweise erfolgreich ist, sie zeigt bei näherer Betrachtung auch, dass Textkenntnis für bestimmte textanalytische Aufgaben unerlässlich ist. Denn wir wissen zwar, dass der Großvater eine wichtige Figur im Buch ist, er kommt in unserer Liste aber bisher nicht vor. Dies liegt vermutlich daran, dass der Named Entity Recognizer das Wort "Großvater" nicht als Person erkannt hat, weshalb es in unserer ursprünglichen Liste fehlt. Da "Großvater" auch flektiert als "Großvaters" auftreten kann, müssen wie also eine Suchanfrage formulieren, die beide Wortformen abdeckt. Hierfür eignet sich z. B. `[token=/Großvater(s)?/]`. Die Anfrage liefert 198 Treffer zurück:

{% include image.html url="images/tundra_grossvater_query_and_result.png" description="Suchergebnisse für _Großvater_ und _Großvaters_." %}

Die Häufigkeit, mit der bestimmte Ausdrücke in einem Text verwendet werden, lässt erste Rückschlüsse darauf zu, worum es in diesem Text geht. Die Abfrage der Häufigkeiten aller als "PER" getaggter Wörter zeigt, dass Heidi 701 mal direkt genannt wird (647 als "Heidi", 54 als "Heidis") und damit die am häufigsten genannte Figur im Text ist. Nach dieser Liste ist Fräulein Rottenmeier die am zweithäufigsten genannte Figur (135 Nennungen); da der Großvater jedoch 198 mal genannt wird, verdrängt er sie von diesem Platz. 

### Zwischenergebnis 3

Die bisherigen Anfragen liefern nicht nur Erkenntnisse über die Häufigkeit, mit der Figurenbezeichnungen verwendet werden. Da das Figurenverzeichnis nicht nur die Namen der Figuren, sondern auch Zusatzinformationen aus dem Text enthalten soll, ist es sinnvoll z. B. anhand der Konkordanzen können auch erste Thesen über den Charakter einer Figur zu bilden. Da nun mehr Informationen darzustellen sind, bietet sich die Tabellenform an.

{% include table_pers_1.html %}

Die Konkordanz, die zur Charakterisierung des Großvaters dient, gibt noch einen weiteren Hinweis. Der Kapitel-Titel "Beim Großvater" lässt vermuten, dass "Öhi" eine alternative Bezeichnung für die Figur "Großvater" ist. Eine kurze Recherche in den Konkordanzen bestätigt dies, weshalb die Häufigkeitsangabe in der Tabelle oben korrigiert werden muss. Da wir bereits wissen, dass statt "Öhi" auch "Alm-Öhi" verwendet werden kann, müssen wir eine Suchanfrage formulieren, die die Ausdrücke "Alm-Öhi", "Öhi", "Großvater" und "Großvaters" findet: `[token=(/(Alm-)*Öhi(s)?/ | /Großvater(s)?/)]`. Diese Suchanfrage findet insgesamt 291 Fundstellen, also fast 100 mehr als die Anfrage für "Großvater(s)?"

{% include image.html url="images/tundra_alm_oehi_grossvater_query_and_result.png" description="Suchergebnisse für _Alm-Öhi_, _Öhi_, _Alm-Öhis_, _Öhis_, _Großvater_ und _Großvaters_." %}

### Verfeinerung der PER-Liste

Es ist sinnvoll, die PER-Liste auf der Grundlage der bisherigen Erkenntnisse zu bereinigen, so dass
+ die unflektierten und flektierten Formen unter einem Eintrag zusammengefasst werden
+ auch Figurennennungen berücksichtigt werden, die von der _named entity recognition_ nicht als Person erkannt wurden.

Für dieses Tutorial führen wir die Bereinigung nur beispielhaft für alle Figurenbezeichnungen durch, die mindestens 100 mal im Text vorkommen. Für ein echtes Forschungsprojekt muss je nach Figurenanzahl eine sinnvolle Strategie entwickelt werden, welche Figurennennungen auf diese Weise bearbeitet werden. Auch hier ist die Häufigkeit eine durchaus sinnvolle Kategorie. Als Grundlage nehmen wir die als CSV- oder Textdatei heruntergeladene Ergebnistabelle für die Abfrage [_ne="PER"]. Sollte diese nicht vollständig sein (was beim Download manchmal passiert), kann die gesamte Tabelle auch einfach direkt von der Webseite kopiert und in eine Textdatei eingefügt werden. In diesem Fall wird jedes Feld auf eine eigene Zeile gesetzt und kann durch Suchen & Ersetzen wieder in eine Komma- oder TAB-separierten Datei verwandelt werden, die in Excel oder LibreOffice Calc oder einem ähnlichen Programm bearbeitet werden kann. Die Suchen müssen in einem Text-Editor durchgeführt werden, der reguläre Ausdrücke versteht ([s. o.](#texteditor "z. B. Sublime, VS Code, Notepad++").

Hinweis zum Suchen und Ersetzen: 

1. Zeilenumbruch nach Dezimalzahl durch Platzhalter _UMBRUCH_ ersetzen
   1. Suchen-Feld: `(\d+\.\d+)\n` (der Ausdruck in runden Klammern wird als Gruppe gefunden und gespeichert, _\n_ steht für "newline". Sollten Sie Windows verwenden müssen Sie evtl. stattdessen _\r\n_ für "carriage return" gefolgt von "newline" suchen.)
   2. Ersetzen-Feld: `$1 UMBRUCH` (_$1_ ruft den gespeicherten Ausdruck ab)
2. Alle (verbleibenden) Zeilenumbrüche durch TAB ersetzen
   1. Suchen-Feld: `\n`
   2. Ersetzen-Feld: `\t`(steht für Tabulator)
3. _UMBRUCH_ überall durch Zeilenumbruch ersetzen
   1. Suchen-Feld: `UMBRUCH`
   2. Ersetzen-Feld: `\n`


Die ursprüngliche Tabelle wurde um die Angaben zu "Großvater(s)" und "(Alm-)*Öhi(s)" ergänzt. Da dies die Gesamtanzahl an Nennungen und damit auch die Prozentangaben beeinflusst, wurde beides neu berechnet. Um eine übersichtlichere Präsentation zu ermöglichen, wurde eine Spalte "Nennform" eingefügt. Als Zwischenschritt wurden zwei Spalten als Sortierhilfe eingefügt, in Sortierhilfe 1 steht die Anzahl der Nennungen, durch Sortierhilfe 2 kann die Reihenfolge der Wortformen (inkl. Summenzeile) beibehalten werden.

{% include image.html url="images/tundra_per_sorting_help.png" description="Zwischenschritt mit Sortierhilfe" %}

Nach Einfügen einer Spalte "Nennform" und Ausbleden der Sortierspalten, sieht das Ergebnis so aus:

{% include image.html url="images/tundra_per_cleaned_and_enhanced.png" description="Tabelle der häufigsten (> 100) Figurenbezeichnungen" %}

### Kurzer Exkurs zu Worthäufigkeiten

Absolute Häufigkeiten sind in korpusbasierten Textanalysen nur dann sinnvoll, wenn das gesamte Korpus aus genau einem Text besteht, wie es hier der Fall ist. Um aber z. B. Aussagen darüber zu treffen, ob der Name einer Hauptfigur eines Romans in Text A häufiger genannt wird als in Text B, müssen relative Häufigkeiten verwendet werden, da sonst z. B. unterschiedliche Textlängen nicht in den Vergleich einfließen. Textlängen werden üblicherweise durch die Gesamtanzahl der Tokens ausgedrückt. Um herauszufinden, aus wie vielen Tokens der vorliegende Text besteht, können wir nach allen Buchstabenketten auf der Token-Ebene suchen: `[token=/.+/]

{% include image.html url="images/tundra_tokens_query_and_result.png" description="Suchergebnisse für die Suche nach allen Wortformen." %}

Der Text besteht aus insgesamt 60424 Tokens in 2285 Sätzen. Die häufigsten Tokens dienen der Punktuation oder gehören der Klasse der sogenannten Synsemantika (Funktionswörter) an. Erst auf Rang 8 erscheint das erste Autosemantikum (Inhaltswort): "Heidi". Die darauf folgenden Wortformen sind wiederum Funktionswörter. Diese Rangfolge entspricht den Erwartungen an natürliche Sprache, wie z. B. ein Vergleich mit einer Statistik des [Wortschatzes Leipzig](https://cls.corpora.uni-leipzig.de/de/deu_easynews_2014/3.2.1_The%20Most%20Frequent%2050%20Words.html) zeigt:

{% include image.html url="images/wortschatz_leipzig_worthaeufigkeiten_vollstaendig.png" description="Auszug aus der Liste der 50 häufigsten Wörter in deutschen Nachrichtentexten" %}

Dass Funktionswörter die Liste anführen ist nicht verwunderlich. Sie sind ausnahmslos in jedem Text vertreten, der den natürlichsprachlichen Konventionen folgt. Als durchaus auffällig kann angesehen werden, dass im vorliegenden Roman die Wortform "es" bereits auf dem fünften Platz auftaucht. Da zwei Ränge davon von Punktuationszeichen besetzt sind, diese in der angeführten Statistik jedoch nicht aufgeführt werden, ist im Vergleich "es" im Roman auf Platz 3, in der Auswertung der Nachrichtentexte jedoch erst auf Platz 16. Aufgrund unserer Textkenntnis wissen wir, dass "Heidi" durch "es" pronominalisiert wird, was also zum konventionellen Gebrauch von "es" hinzukommt und so (vermutlich) die Rangfolge stark beeinflusst. Eine genauere Untersuchung sprengt den Rahmen dieses Tutorials. Eine mögliche Vorgehensweise wäre, den gesamten Text daraufhin auszuwerten, wie häufig "es" als Pronominalisierung von "Heidi" verwendet wird.

Relative Häufigkeiten werden für die Analyse eines einzelnen Textes auch dann wichtig, wenn dieser Text nicht mehr als Ganzes, sondern z. B. kapitelweise untersucht wird. Um prüfen zu können, ob eine Figur in einem Kapitel häufiger als in einem anderen genannt wird, genügt die absolute Häufigkeit nicht mehr, sondern sie muss in ein Verhältnis zur Anzahl aller Wörter im jeweiligen Kapitel gesetzt werden. 

TODO:
- zwei Kapitel zur Demonstration relativer Häufigkeiten in WebLicht untersuchen
- relative Häufigkeiten (zu allen Tokens) von Heidi etc. berechnen  


### Verteilung der Figuren über den Text

Neben der Häufigkeit, mit der Figurenbezeichnungen auftreten, ist auch ihre Verteilung über den Text eine interessante Größe. Wenn der Text nicht in Kapitel zerlegt vorliegt, müssen andere Möglichkeiten gefunden werden, um den Text zu zerlegen und so Aussagen darüber zu ermöglichen, wie häufig welche Figur wann genannt wird. Die Textanalyse-Umgebung [Voyant](https://voyant-tools.org) zerlegt ein Korpus, das aus einem einzigen Text besteht, standardmäßig in zehn Teile. Neben weiteren Werkzeugen zeigt es die Verteilung von Wörtern auf diese zehn Teile als Grafik:

{% include image.html url="images/voyant_characters_dispersion_fulltext_corpus.png" description="Verteilung der häufigsten Figuren auf den in Zehntel zerlegten Text in Voyant" %}

In Voyant können nicht nur einzelne Texte, sondern auch Korpora aus mehreren Texten geladen werden. Dies erlaubt es auch, die Verteilung der Figurennennungen kapitelweise zu visualisieren. Allerdings muss hierfür die Benennung der Dokumente so angepasst werden, dass die Kapitelzählung richtig interpretiert wird. Wir dies nicht getan, erhält man beispielsweise folgendes Ergebnis:

{% include image.html url="images/voyant_chapter_corp_wrong_order.png" description="Unerwartete Kapitelreihenfolge in Voyant aufgrund nicht-numerischer Interpretation der Zahlen in den Dateinamen" %}



TODO
- WebLicht prüfen (Satzzählung)
- Voyant
- Ergebnis der Verteilung ist Hinweis auf Wichtigkeit (gleichmäßig = wichtig)

### Aussagen über Figuren erheben
TODO:
- Strategien beschreiben / ausprobieren
  - Kollokationen / Ko-Okkurrenzen berechnen und prüfen, ob die Konkordanzen, die die meisten der häufigen Wörter enthalten aussagekräftige Beschreibungen der Figuren liefern
  - 



# 5. Figurenverzeichnis aus Ergebnissen der Textanalyse erstellen
TODO:
- Wörterbuchartige Liste (als Tabelle, darin auch Häufigkeitsverlauf von Voyant verarbeiten)
- Netzwerke 
  - welche Figuren treten häufig miteinander auf?
  - welche Wörter treten häufig mit welcher Figur auf?
  - Netz aus Figuren und häufigsten Kollokationen

## Erweiterungen 
### XML-Ressource erstellen (statt Tabelle)

# 6. Übertragbarkeit auf andere Forschungsinteressen
TODO:
- kurz zeigen, dass die Vorgehensweise immer angewendet werden kann, wenn es um Begriffsbestimmung im weitesten Sinn geht
- auf Annotationslehrpfad verweisen
- evtl. Bakers Fuchsjagd kurz als Beispiel dafür zeigen, dass auch hier Ko-Text-Analysen (gepaart mit Metadaten) die Grundlage der Vorgehensweise bilden 