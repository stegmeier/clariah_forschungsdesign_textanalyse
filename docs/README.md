# Forschungsdesign "korpusbasierte Textanalyse" <!-- omit in toc -->

- [1. Kurzbeschreibung](#1-kurzbeschreibung)
- [2. Text finden](#2-text-finden)
  - [2.1. Text vorbereiten](#21-text-vorbereiten)
- [3. Text analysieren](#3-text-analysieren)
  - [3.1. Automatische Analyse und Annotation](#31-automatische-analyse-und-annotation)
  - [3.2. Manuelle bw. semi-automatische Analyse: Das annotierte Korpus nutzen](#32-manuelle-bw-semi-automatische-analyse-das-annotierte-korpus-nutzen)
    - [3.2.1. Figuren identifizieren](#321-figuren-identifizieren)
    - [3.2.2. Zwischenergebnis 1](#322-zwischenergebnis-1)
    - [3.2.3. Zwischenergebnis verfeinern](#323-zwischenergebnis-verfeinern)
    - [3.2.4. Zwischenergebnis 2](#324-zwischenergebnis-2)
    - [3.2.5. Zwischenergebnis 3](#325-zwischenergebnis-3)
    - [3.2.6. Verfeinerung der PER-Liste](#326-verfeinerung-der-per-liste)
    - [3.2.7. Kurzer Exkurs zu Worthäufigkeiten](#327-kurzer-exkurs-zu-worthäufigkeiten)
    - [3.2.8. Häufigkeitsverteilung der Figuren über den Text](#328-häufigkeitsverteilung-der-figuren-über-den-text)
    - [3.2.9. Aussagen über Figuren erheben](#329-aussagen-über-figuren-erheben)
- [4. Figurenverzeichnis aus Ergebnissen der Textanalyse erstellen](#4-figurenverzeichnis-aus-ergebnissen-der-textanalyse-erstellen)
- [5. Erweiterungen](#5-erweiterungen)
  - [5.1. Komplexere Abfragestrategien](#51-komplexere-abfragestrategien)
  - [5.2. Netzwerke von Figureninteraktionen](#52-netzwerke-von-figureninteraktionen)
  - [5.3. Ergebnis als XML-Ressource erstellen (statt Tabelle)](#53-ergebnis-als-xml-ressource-erstellen-statt-tabelle)
- [6. Übertragbarkeit auf andere Forschungsinteressen](#6-übertragbarkeit-auf-andere-forschungsinteressen)

# 1. Kurzbeschreibung

Das Forschungsdesign "korpusbasierte Textanalyse" zeigt beispielhaft das Zusammenspiel der verschiedenen Dienste und Ressourcen, die von CLARIAH-DE angeboten werden. Die Aufgabe ist es, ein Verzeichnis der in einem Roman auftretenden Figuren zu erstellen. Daraus entstehen die folgenden Teilaufgaben:

- Roman in digitaler Form finden (s. [Text finden](#3-text-finden))
- Text automatisch annotieren lassen, um u. a. Personen (= Figuren) finden zu können (s. [Text analysieren](#4-text-analysieren))
- Anhand von Konkordanz-Analysen Beschreibungen der Figuren erstellen
- Aus den Personen und den Beschreibungen ein Verzeichnis erstellen (s. [Figurenverzeichnis erstellen](#5-figurenverzeichnis-aus-ergebnissen-der-textanalyse-erstellen))

Neben der Untersuchung von Konkordanzen sind auch komplexere Such- und Analysestrategien sinnvoll. Auf diese wird unter [Erweiterungen](#5-erweiterungen) eingegangen.

Die hier dargestellte Vorgehensweise ist auf jede Forschungsfrage übertragbar, in der Begriffe dadurch bestimmt werden sollen, dass die Häufigkeit und der Ko-Text der auf sie verweisenden Ausdrücke analysiert werden. Hierauf wird im [letzen Abschnitt](#6-übertragbarkeit-auf-andere-forschungsinteressen) noch einmal eingegangen. 

<div class="todo">
TODO:
<ul>
<li>Am Ende Vorüberlegungen noch einmal auf Vollständigkeit prüfen</li>
</ul>
</div>

# 2. Text finden

Die Grundlage einer korpusbasierten Textanalyse ist ein Text in digitaler Form. Liegt der Text nur gedruckt vor, muss er gescannt und über OCR (_Optical Character Recognition_) in maschinenlesbaren Text überführt werden. Das hierzu notwendige Vorgehen ist nicht Teil dieses Tutorials. Die OCR ist auch dann notwendig, wenn der Text zwar digitalisiert wurde, aber nur als eine Sammlung von Bildern vorliegt. Auch PDF-Dateien können ausschließlich aus Bildern bestehen. Ist dies für den gewünschten Text der Fall, muss auch hier die OCR durchgeführt werden. Auch PDFs, aus denen der Text extrahiert werden kann, sind nicht immer die beste Grundlage, da der Export in ein reines Textformat häufig Probleme bereitet. Die verbreitetsten Probleme sind dabei "harte" Zeilenumbrüche, fehlende Leerzeichen zwischen Zeilenumbrüchen, Inhalte aus Fuß- und/oder Kopfzeilen (Seitenzahlen, Autornamen, Titelangaben), die nach dem Export mitten im Text stehen und die Trennungszeichen am Zeilenende. Alle diese (und evtl. weitere) Phänomene müssen geprüft und bereinigt werden, bevor der Text weiterverarbeitet werden kann.

Es ist aus diesem Grund von Vorteil, bereits entsprechend aufbereitete Texte zu verwenden. Verschiedene Repositorien bieten inzwischen einen Fundus an solchen Quellen an. Das [TextGrid Repositorium](https://textgrid.de) bietet in seiner [Digitalen Bibliothek](https://textgrid.de/digitale-bibliothek) eine Vielzahl an Texten aus Literatur, Philosophie, Kulturgeschichte und weiteren Kategorien an. Der Schwerpunkt liegt mit über 90.000 Texten auf der (historischen) Literatur. Das [Deutsche Text-Archiv (DTA)](https://www.deutschestextarchiv.de/), bestehend aus einem Kernkorpus und einer Erweiterung (DTAE) bietet sowohl Texte zum Download an als auch die direkte [Nutzung des gesamten Bestands als Korpus](https://www.deutschestextarchiv.de/doku/DDC-suche_hilfe). Die Texte verteilen sich auf die folgenden Kategorien (s. auch [die Erläuterungen zur Textauswahl](https://www.deutschestextarchiv.de/doku/textauswahl), denen die folgende Darstellung entnommen ist):

{% include image.html url="images/dta_ueberblick.png" description="Zusammensetzung des DTA-Korpus (Quelle: DTA)" %}

Auch das [Projekt Gutenberg](https://www.projekt-gutenberg.org/) eignet sich sehr gut, um digitale Texte in verarbeitbarer Form zu finden. Es ist allerdings darauf ausgelegt, dass die Texte im Browser gelesen werden und bietet keine Downloadmöglichkeit.

Wir nutzen für dieses Tutorial den Roman "Heidis Lehr- und Wanderjahre" von Johanna Spyri, der im TextGrid-Repositorium in verschienden Formaten [zum Download angeboten wird](https://textgridrep.org/search?query=heidi&order=&limit=).


## 2.1. Text vorbereiten
Es bietet sich an, einen Roman in Kapitel zerlegt zu analysieren, da dies z. B. erlaubt, das Auftreten und die Charakterisierung von Figuren im Verlauf der Handlung zu beschreiben. Die Zerlegung in Kapitel folgt dabei der Überlegung, dass die Einteilung in Kapitel in konventionellen Romanen in einer Beziehung zum Handlungsfortschritt steht. Dies kann beim ausgewählten Text unterstellt werden, da er eine fortschreitende Handlung erzählt, also z. B. keines der Kapitel einen Rückblick auf vorangegangene Ereignisse bietet.

Die Zerlegung von reinem Text ist je nach Größe auch manuell recht schnell machbar, wenn hierfür ein Text-Editor zur Verfügung steht, der die Suche nach regulären Ausdrücken erlaubt. <a name="texteditor" class="default_text_color">In Frage kommen z. B.</a> [Sublime Text](https://www.sublimetext.com/), [Notepad++](http://notepad-plus-plus.org/) oder [VS Code](https://code.visualstudio.com/). Um bequem nach den Kapitelanfängen und -enden suchen zu können, ist es von großem Vorteil, die Titel der Kapitel zu kennen. Eine kurze Suche bei z. B. [Projekt Gutenberg](https://www.projekt-gutenberg.org/spyri/heidi1/index.html) (oder einer Bibliothek der Wahl) bringt bereits ein brauchbares Ergebnis:


{% include image.html url="images/heidi_kapitel_projekt_gutenberg.png" description="Inhaltsverzeichnis von <em>Heidi</em> auf der Webseite von Projekt Gutenberg" %}

Die Suche nach den einzelnen Kapiteln lässt sich als regulärer Ausdruck nun folgendermaßen formulieren:

`[Titel des zu findenden Kapitels][Zeilenumbruch][beliebiger Text][Titel des folgenden Kapitels][Zeilenumbruch]`

Suche nach dem Kapitel "Fräulein Rottenmeier hat einen unruhigen Tag":

`Fräulein Rottenmeier hat einen unruhigen Tag\n(.+\n)+Im Hause Sesemann geht's unruhig zu\n`

Der Text-Editor findet nun sowohl die beiden Kapitel-Titel als auch allen Text dazwischen, der durch den (komplexen) regulären Ausdruck `\n(.+\n)+` dargestellt wird. Die Bedeutung der einzelnen Komponenten ist dabei wie folgt:

- `\n` steht für einen Zeilenumbruch (in Linux und Unix-Derivaten). Windows-Zeilenenden bestehen aus der Kombination eines Carriage-Returns, der durch `\r` dargestellt wird und einem Zeilenumbruch. Insgesamt also `\r\n`
- runde Klammern werden dazu genutzt, einzelne Komponenten zu Gruppen zusammenzufassen
 - der Punkt `.` steht für jeden beliebigen Buchstaben inkl. Leerzeichen
 - das Plus `+` ist ein sogenannter Quantor, der sich auf das Zeichen davor bezieht und bedeutet "1 oder mehr"
 - innerhalb der Gruppe wird also beliebiger Text mit Leerzeichen bis zu einem Zeilenumbruch gefunden; da hinter der Gruppe ein weiteres `+` folgt, wird die Gruppe so oft gefunden, bis der Text "Im Hause Sesemann ..." anfängt

Das Suchergebnis kann bequem kopiert und in eine neue Datei eingefügt werden. Um die Reihenfolge der Kapitel auch bei der späteren Analyse verwenden zu können, sollten die Dateinamen eine fortlaufende Kapitelzählung enthalten, also z. B. `heidi_kap_1_zum-alm-oehi-hinauf.txt`

**Hilfen zu regulären Ausdrücken:** Online stehen zahlreiche Tutorials, z. B. [Regular Expressions info (auf Englisch)](https://www.regular-expressions.info/quickstart.html), [SELFHTML (auf Deutsch)](https://wiki.selfhtml.org/wiki/Regul%C3%A4rer_Ausdruck) und Testumgebungen, z. B. [regex101 (auf Englisch)](https://regex101.com/), [regexr (auf Englisch)](https://regexr.com/) für reguläre Ausdrücke zur Verfügung.


# 3. Text analysieren

Die Analyse des Textes wird in zwei großen Schritten durchgeführt, die jeweils eine Anzahl von Teilschritten enthalten. Der erste große Schritt ist die [automatische Analyse](#automatische-analyse), an dessem Ende der Text in annotierter, also mit Zusatzinformation versehener, Form vorliegt. Um Personenbezeichnungen automatisch erkennen zu können, muss der Text in einzelne Wortformen (= Tokens) zerlegt werden. Es bietet sich an, auch eine Lemmatisierung durchzuführen, also jede Wortform mit der Zusatzinformation zu versehen, von welcher Grundform sie abgeleitet wurde: Das Lemma der Worform _ging_ ist in diesem Sinne _gehen_. Im Anschluss folgt die _named entity regocnition_ (NER), die neben Institutionen auch Personenennamen erkennt und markiert. Im [zweiten Schritt](#manuelle-bw-semi-automatische-analyse) werden die Zusatzinformationen dazu genutzt, die im Roman vorkommenden Figuren zu identifizieren. Für die 

## 3.1. Automatische Analyse und Annotation

Für die automatische Annotation von Text steht eine [Vielzahl von Werkzeugen](https://www.clariah.de/ueber-uns/diensteliste) zur Verfügung. Unsere Forschungsfrage erfordert es, den annotierten Text durchsuchen zu können. Zusätzlich zu den Annotationswerkzeugen benötigen wir also auch eine zusätzliche Software, die dies leistet. 

Da es fast so viele Ausgabeformate von Annotationswerkzeugen gibt wie Werkzeuge selbst, bietet es sich an, bei der Suche nach geeigneter Software gleich im Blick zu behalten, dass der annotierte Text nur ein Zwischenergebnis ist. Eine der bequemsten Möglichkeiten, die alle Anforderungen erfüllt, ist der browserbasierte Service [WebLicht](https://weblicht.sfs.uni-tuebingen.de/weblichtwiki/index.php/Main_Page), der für Angehörige von Forschungseinrichtungen kostenlos genutzt werden kann. Für sehr große Korpora, also z. B. Zeitungskorpora, die aus Tausenden von Einzeltexten bestehen können, sind andere Dienste eventuell besser geeignet. Die Annotation kann zwar durchaus auch bei einer Vielzahl an Texten über [WebLicht as a service](https://weblicht.sfs.uni-tuebingen.de/WaaS/) realisiert werden, es ist in einem solchen Fall jedoch vorteilhaft ein anderes (evtl. selbst gehostetes) Korpusverwaltungssystem zu nutzen (z. B. [CQPweb](https://cwb.sourceforge.io/cqpweb.php)).

Nach der Anmeldung über den Institutionszugang zeigt die browserbasierten WebLicht-Version einen Startbildschirm, auf dem durch Klicken auf "Start" das Upload-Formular aufgerufen werden kann.

{% include image.html url="images/weblicht_1_upload.png" description="Upload eines Textes auf WebLicht" %}

Im Anschluss kann ausgewählt werden, ob eine vordefinierte Werkzeugkette ("Chains") benutzt werden soll ("Easy Mode") oder ob die Werkzeuge einzeln vom Nutzer zusammengestellt werden sollen ("Advanced Mode").

{% include image.html url="images/weblicht_2_choose_mode.png" description="Upload eines Textes auf WebLicht" %}

Wir nutzen für den ersten Teil des Tutorials die vordefinierte Kette für die _Named Entity Recognition_ (NER):

{% include image.html url="images/weblicht_3_easy_mode_choose_ner_chain.png" description="Auswahl einer Werkzeugkette" %}

Nachdem alle Werkzeuge in der angegebenen Reihenfole angewendet wurden, kann der annotierte Text direkt online durchsucht oder heruntergeladen werden:

{% include image.html url="images/weblicht_4_view_and_download_results.png" description="Analyse in WebLicht mit Downloadmöglichkeiten" %}

## 3.2. Manuelle bw. semi-automatische Analyse: Das annotierte Korpus nutzen

Das annotierte Korpus ist die Grundlage für die Bearbeitung der Forschungsfrage. Durch die Zusatzinformationen können wir nun z. B. direkt eine Liste aller Wörter ausgeben lassen, die von der _Named Entity Recognition_ als Person erkannt wurden (s. [Figuren identifizieren](#figuren-identifizieren)). Darüber hinaus können wir die Textumgebung der Wörter, die als Person erkannt werden, in die Analyse mit einbeziehen. Auf diese Weise können wir z. B. prüfen, ob vielleicht unterschiedliche Personen mit demselben Nachnamen existieren (s. [Zwischenergebnis verfeinern](#zwischenergenis-verfeinern)) und wie die Figuren durch den Ko-Text charakterisiert werden (s. [Aussagen über Figuren erheben](#aussagen-über-figuren-erheben)). Wir beschränken uns dabei auf die häufigsten Figuren.

### 3.2.1. Figuren identifizieren
Das annotierte Korpus kann direkt nach der automatischen Annotation in WebLicht genutzt oder in [TüNDRA](https://weblicht.sfs.uni-tuebingen.de/Tundra/), der _Tübingen aNnotated Data Retrieval Application_ geladen und dort durchsucht werden. 

{% include image.html url="images/tundra_upload_tcf_annotated_corpus.png" description="Upload eines eigenen Korpus im TCF-Format in TÜNDRA" %}

Nach dem Upload können über die Suchanfrage `[_ne="PER"]` alle Wörter angezeigt werden, die als _Person_ (Tag: _PER_) erkannt wurden. "_ne" spricht die Ebene der _Named Entiy Recognition_ an, "PER" wählt alle als Person getaggte Tokens aus. Zur verwendeten Anfragesprache gibt es ein [kleines Handbuch](https://weblicht.sfs.uni-tuebingen.de/Tundra/help) und ein [Tutorial](https://weblicht.sfs.uni-tuebingen.de/Tundra/tutorial).

{% include image.html url="images/tundra_query_per.png" description="Suchanfrage, um alle mit <em>PER</em> annotierten Wörter zu finden" %}

Das Ergebnis der Suchanfrage wird u. a. als Konkordanz dargestellt, also als eine Liste der gefundenen Wörter und ihren Fundstellen.

{% include image.html url="images/tundra_result_conc_query_per.png" description="Konkordanz aller als <em>PER</em>getaggten Wörter. Als Umgebung des Suchausdrucks wird der Satz angezeigt, in der er gefunden wurde." %}

Die Suchergebnisse werden auch als aggregierte Liste dargestellt. Als Standardeinstellung gibt WebLicht hier lediglich die Gesamtanzahl der Fundstellen an. Über die Option _Add/Remove Columns_ kann die Darstellung verfeinert werden (*_ne* wählt die Ebene der _Named Entity Recognition_ aus; _token_ wählt die Ebene der Wortformen aus):

{% include image.html url="images/tundra_refine_stats_query_per.png" description="Spalte <em>_ne</em> und <em>token</em> in der Statistik-Tabelle hinzufügen." %}

Werden weitere Spalten hinzugefügt, werden die ausgewählten Kategorien in der Zählung berücksichtigt.

{% include image.html url="images/tundra_result_refined_stats_query_per.png" description="Anzeige, welche Wörter als <em>PER</em> getaggt wurden und wie häufig sie im Korpus auftreten." %}

### 3.2.2. Zwischenergebnis 1

Die Liste aller als _PER_ getaggten Wörter ist die Grundlage für das Figurenverzeichnis. Da sie auf Token, also Wortformen beruht, werden manche Namen in flektierter Form extra aufgelistet (z. B. "Heidi" und "Heidis"). Ein bereinigtes Figurenverzeichnis könnte also so aussehen:
* Heidi
* Rottenmeier
* Sesemann
...

### 3.2.3. Zwischenergebnis verfeinern

Da es sich bei "Rottenmeier" und "Sesemann" um Nachnamen handelt, wäre es von Vorteil, hier noch einen Vornamen oder zumindest eine Anredeform hinzuzufügen. Ein Blick in die Konkordanzen von `[token="Rottenmeier"]` zeigt, dass "Rottenmeier" praktisch immer ein "Fräulein" vorausgeht. Diese These kann überprüft werden, indem die Suchabfrage um ein vorangestelltes "Fräulein" erweitert wird. In der hier verwendeten Anfragesprache wird dies realisiert, indem die Anfragen nach "Fräulein" und "Rotttenmeier" in der richtigen Reihenfolge durch einen Punkt verknüpft werden: `[token="Fräulein"] . [token="Rottenmeier"]`

{% include image.html url="images/tundra_fraeulein_rottenmeier_query_and_result.png" description="Suchergebnisse für <em>Fräulein Rottenmeier</em>." %}

Allerdings stimmt die Anzahl der Fundstellen nicht überein: "Rottenmeier" kommt 135 mal im Korpus vor, "Fräulein Rottenmeier" jedoch nur 127 mal. Es muss also acht Okkurrenzen von "Rottenmeier" geben, denen ein anderes Wort als "Fräulein" vorangeht. Um diese zu finden, muss also die Suchanfrage `[token="Fräulein"] . [token="Rottenmeier"]` so manipuliert werden, dass alle Okkurrenzen von _Nicht "Fräulein" gefolgt von "Rottenmeier"_ gefunden werden. Als Suchanfrage formuliert sieht das so aus: `[token!="Fräulein"] . [token="Rottenmeier"]`. Die Kombination aus Ausrufezeichen und Gleichheitszeichen wird als "nicht gleich" interpretiert. Das Ergebnis der Anfrage ist:

{% include image.html url="images/tundra_not_fraeulein_rottenmeier_query_and_result.png" description="Suchergebnisse für <em>Nicht 'Fräulein' gefolgt von 'Rottenmeier'</em>." %}

Da nun alle 135 Vorkommen von "Rottenmeier" geprüft sind, kann der Eintrag im Figurenverzeichnis in "Fräulein Rottenmeier" geändert werden. 

Dieselben Schritte gilt es nun für "Sesemann" und alle anderen potenziellen Einträge vorzunehmen. Da die These "Rottenmeier" bezieht sich immer auf "Fräulein Rottenmeier" nur aufgrund von Vorwissen über den Text aufgestellt werden kann, bietet es sich, eine allgemeinere Anfrage zu formulieren, die einfach alle Wörter anzeigt, die direkt vor "Sesemann" auftreten und auch die Flektionsform "Sesemanns" berücksichtigen, die ja laut PER-Liste zweimal im Text auftritt. Da TüNDRA (bzw. auch der in WebLicht eingebaute Viewer) reguläre Ausdrücke unterstützt, ist es relativ einfach, eine Suchanfrage zu formulieren, die sowohl "Sesemann" als auch "Sesemanns" findet und statt "Fräulein" jedes beliebige Token davor als Ergebnis zurückliefert: `[token=/.+/] . [token=/Sesemann(s)?/]`. Die runden Klammern im Suchausdruck nach "Sesemann" erzeugen eine Gruppe (hier bestehend aus dem Buchstaben _s_) und das Fragezeichen legt fest, dass diese Gruppe "0 oder einmal" auftreten darf. 

{% include image.html url="images/tundra_any_token_sesemann_query_and_result.png" description="Suchergebnisse für <em>beliebige Buchstabenkette gefolgt von 'Sesemann'</em>" %}

Die Tabelle unter "Statistics" zeigt, welche Wörter wie oft vor "Sesemann" auftreten. Wir wissen nun also, dass die Einträge im Figurenverzeichnis um "Frau Sesemann", "Herr Sesemann" und "Klara Sesemann" erweitert werden können. Der folgende Ausschnitt aus den Konkordanzen zeigt eine Form im Genitiv und eine Verwendung einer Phrase die "Hause Sesemann" enthält. "Hause" und "Hauses" gehen "Sesemann" insgesamt elf Mal voraus. Es gibt also mindestens elf Fundstellen für "Sesemann(s)", die nicht direkt einer der Figuren zugeordnet werden können. Für das folgende Zwischenergebnis spielt dies erst einmal keine Rolle.

### 3.2.4. Zwischenergebnis 2

1. Heidi
2. Fräulein Rottenmeier
3. Herr Sesemann
4. Frau Sesemann
5. Klara Sesemann

Diese Liste zeigt nicht nur, dass die Vorgehensweise erfolgreich ist, sie zeigt bei näherer Betrachtung auch, dass Textkenntnis für bestimmte textanalytische Aufgaben unerlässlich ist. Denn wir wissen zwar, dass der Großvater eine wichtige Figur im Buch ist, er kommt in unserer Liste aber bisher nicht vor. Dies liegt vermutlich daran, dass der Named Entity Recognizer das Wort "Großvater" nicht als Person erkannt hat, weshalb es in unserer ursprünglichen Liste fehlt. Da "Großvater" auch flektiert als "Großvaters" auftreten kann, müssen wie also eine Suchanfrage formulieren, die beide Wortformen abdeckt. Hierfür eignet sich z. B. `[token=/Großvater(s)?/]`. Die Anfrage liefert 198 Treffer zurück:

{% include image.html url="images/tundra_grossvater_query_and_result.png" description="Suchergebnisse für <em>Großvater</em> und <em>Großvaters</em>." %}

Die Häufigkeit, mit der bestimmte Ausdrücke in einem Text verwendet werden, lässt erste Rückschlüsse darauf zu, worum es in diesem Text geht. Die Abfrage der Häufigkeiten aller als "PER" getaggter Wörter zeigt, dass Heidi 701 mal direkt genannt wird (647 als "Heidi", 54 als "Heidis") und damit die am häufigsten genannte Figur im Text ist. Nach dieser Liste ist Fräulein Rottenmeier die am zweithäufigsten genannte Figur (135 Nennungen); da der Großvater jedoch 198 mal genannt wird, verdrängt er sie von diesem Platz. 

### 3.2.5. Zwischenergebnis 3

Die bisherigen Anfragen liefern nicht nur Erkenntnisse über die Häufigkeit, mit der Figurenbezeichnungen verwendet werden. Da das Figurenverzeichnis nicht nur die Namen der Figuren, sondern auch Zusatzinformationen aus dem Text enthalten soll, ist es sinnvoll z. B. anhand der Konkordanzen können auch erste Thesen über den Charakter einer Figur zu bilden. Da nun mehr Informationen darzustellen sind, bietet sich die Tabellenform an.

{% include table_pers_1.html %}

Die Konkordanz, die zur Charakterisierung des Großvaters dient, gibt noch einen weiteren Hinweis. Der Kapitel-Titel "Beim Großvater" lässt vermuten, dass "Öhi" eine alternative Bezeichnung für die Figur "Großvater" ist. Eine kurze Recherche in den Konkordanzen bestätigt dies, weshalb die Häufigkeitsangabe in der Tabelle oben korrigiert werden muss. Da wir bereits wissen, dass statt "Öhi" auch "Alm-Öhi" verwendet werden kann, müssen wir eine Suchanfrage formulieren, die die Ausdrücke "Alm-Öhi", "Öhi", "Großvater" und "Großvaters" findet: `[token=(/(Alm-)*Öhi(s)?/ | /Großvater(s)?/)]`. Diese Suchanfrage findet insgesamt 291 Fundstellen, also fast 100 mehr als die Anfrage für "Großvater(s)?"

{% include image.html url="images/tundra_alm_oehi_grossvater_query_and_result.png" description="Suchergebnisse für <em>Alm-Öhi</em>, <em>Öhi</em>, <em>Alm-Öhis</em>, <em>Öhis</em>, <em>Großvater</em> und <em>Großvaters</em>." %}

### 3.2.6. Verfeinerung der PER-Liste

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

Nach Einfügen einer Spalte "Nennform" und Ausblenden der Sortierspalten, sieht das Ergebnis so aus:

{% include image.html url="images/tundra_per_cleaned_and_enhanced.png" description="Tabelle der häufigsten (> 100) Figurenbezeichnungen" %}

**Anmerkung zu der Häufigkeit von "Heidi":** Auf "Heidi" als Figur wird auch durch den Ausdruck "das Kind" Bezug genommen. Um die Häufigkeit, mit der dies geschieht jedoch verlässlich angeben zu können, muss jedes Vorkommen geprüft werden, ob nicht doch ein anderes Kind damit gemeint ist. Insgesamt wird die Phrase `[Artikel][Kind in allen Flektionsformen]` formuliert als `[pos="ART"] . [lemma="Kind"]` 226 Mal gefunden. In einer Untersuchung, die nicht nur Demonstrationszwecken dient, würde sich die Arbeit also nicht nur lohnen, sondern wäre eine Mindestanforderung.

### 3.2.7. Kurzer Exkurs zu Worthäufigkeiten

Absolute Häufigkeiten sind in korpusbasierten Textanalysen nur dann sinnvoll, wenn das gesamte Korpus aus genau einem Text besteht, wie es hier der Fall ist. Um aber z. B. Aussagen darüber zu treffen, ob der Name einer Hauptfigur eines Romans in Text A häufiger genannt wird als in Text B, müssen relative Häufigkeiten verwendet werden, da sonst z. B. unterschiedliche Textlängen nicht in den Vergleich einfließen. Textlängen werden üblicherweise durch die Gesamtanzahl der Tokens ausgedrückt. Um herauszufinden, aus wie vielen Tokens der vorliegende Text besteht, können wir nach allen Buchstabenketten auf der Token-Ebene suchen: `[token=/.+/]`

{% include image.html url="images/tundra_tokens_query_and_result.png" description="Suchergebnisse für die Suche nach allen Wortformen." %}

Der Text besteht aus insgesamt 60424 Tokens in 2285 Sätzen. Die häufigsten Tokens dienen der Punktuation oder gehören der Klasse der sogenannten Synsemantika (Funktionswörter) an. Erst auf Rang 8 erscheint das erste Autosemantikum (Inhaltswort): "Heidi". Die darauf folgenden Wortformen sind wiederum Funktionswörter. Diese Rangfolge entspricht den Erwartungen an natürliche Sprache, wie z. B. ein Vergleich mit einer Statistik des [Wortschatzes Leipzig](https://cls.corpora.uni-leipzig.de/de/deu_easynews_2014/3.2.1_The%20Most%20Frequent%2050%20Words.html) zeigt:

{% include image.html url="images/wortschatz_leipzig_worthaeufigkeiten_vollstaendig.png" description="Auszug aus der Liste der 50 häufigsten Wörter in deutschen Nachrichtentexten" %}

Dass Funktionswörter die Liste anführen ist nicht verwunderlich. Sie sind ausnahmslos in jedem Text vertreten, der den natürlichsprachlichen Konventionen folgt. Als durchaus auffällig kann angesehen werden, dass im vorliegenden Roman die Wortform "es" bereits auf dem fünften Platz auftaucht. Da zwei Ränge davon von Punktuationszeichen besetzt sind, diese in der angeführten Statistik jedoch nicht aufgeführt werden, ist im Vergleich "es" im Roman auf Platz 3, in der Auswertung der Nachrichtentexte jedoch erst auf Platz 16. Aufgrund unserer Textkenntnis wissen wir, dass "Heidi" durch "es" pronominalisiert wird, was also zum konventionellen Gebrauch von "es" hinzukommt und so (vermutlich) die Rangfolge stark beeinflusst. Eine genauere Untersuchung sprengt den Rahmen dieses Tutorials. Eine mögliche Vorgehensweise wäre, den gesamten Text daraufhin auszuwerten, wie häufig "es" als Pronominalisierung von "Heidi" verwendet wird.

### 3.2.8. Häufigkeitsverteilung der Figuren über den Text

Neben der Häufigkeit, mit der Figurenbezeichnungen auftreten, ist auch ihre Verteilung über den Text eine interessante Größe. Eine Figur, die nur in bestimmten Teilen eines Buches auftritt, spielt eine andere Rolle für das gesamte Buch, als eine Figur, die in jedem oder fast jedem Kapitel auftritt. Aber auch eine Figur, die in jedem Kapitel vorkommt, kann eine untergeordnete Rolle spielen. Daher ist es auch hier sinnvoll, die Häufigkeit, mit der eine Figur (bzw. ein Wort oder ein annotierte Kategorie wie _Per_) in einem bestimmten Textabschnitt genannt wird, in die Untersuchung der Verteilung einzubeziehen. Wenn aber z. B. nur das Personal eines bestimmten Textabschnittes bestimmt werden soll, genügt es zu prüfen, ob eine Figur genannt wird oder nicht. Wenn die Ergebnisse auch Rückschlüsse darauf zulässen, wie wichtig ein Ausdruck oder eine Kategorie für die Interpretation oder das Verstehen des Textabschnittes ist, muss die Häufigkeitsverteilung bestimmt werden. In diesem Zusammenhang werden die oben angesprochenen relativen Häufigkeiten auch für die Analyse eines einzelnen Textes wichtig, da nur so herausgefunden werden kann, ob eine Figur bzw. Ausdruck in einem Kapitel häufiger als in einem anderen genannt wird. Die relative Häufigkeit wird dabei als Verhältnis des gesuchten Ausdrucks zur Anzahl aller Wörter im jeweiligen Kapitel gesetzt verstanden.

Wenn der Text nicht in Kapitel zerlegt vorliegt, müssen andere Möglichkeiten gefunden werden, um den Text zu zerlegen und so Aussagen darüber zu ermöglichen, wie häufig welche Figur wann genannt wird. Die Textanalyse-Umgebung [Voyant](https://voyant-tools.org) zerlegt ein Korpus, das aus einem einzigen Text besteht, standardmäßig in zehn Teile. Neben weiteren Werkzeugen zeigt es die Verteilung von Wörtern auf diese zehn Teile auf der Grundlage der relativen Häufigkeiten innerhalb der Abschnitte als Grafik:

{% include image.html url="images/voyant_characters_dispersion_fulltext_corpus.png" description="Verteilung der häufigsten Figuren auf den in Zehntel zerlegten Text in Voyant" %}

Da wir den Text schon zu Beginn in Kapitel (= Teilkorpora) zerlegt haben, können wir die Häufigkeitsverteilung auf dieser Grundlage untersuchen. WebLicht bzw. TüNDRA hierfür zu nutzen, ist ein wenig umständlich, da jeder Text einzeln als Korpus geladen und durchsucht werden muss. Wenn eine sehr große Menge an Teilkorpora vorliegt, ist es besser, ein Korpusverwaltungssystem wie CQPweb, oder einen Service wie [Voyant](https://voyant-tools.org) zu nutzen. 

In Voyant können nicht nur einzelne Texte, sondern auch Korpora aus mehreren Texten geladen werden. Dies erlaubt es auch, die Verteilung der Figurennennungen kapitelweise zu visualisieren. Allerdings muss hierfür die Benennung der Dokumente so angepasst werden, dass die Kapitelzählung richtig interpretiert wird. Wird dies nicht getan, erhält man beispielsweise folgendes Ergebnis:

{% include image.html url="images/voyant_chapter_corp_wrong_order.png" description="Unerwartete Kapitelreihenfolge in Voyant aufgrund nicht-numerischer Interpretation der Zahlen in den Dateinamen" %}

Die Dateien müssen also entsprechend umbenannt werden (z. B. "01" statt "1" etc.). Ist dies geschehen, stellt Voyant die Ergebnisse in der richtigen Reihenfolge dar:

{% include image.html url="images/voyant_figurenverteilung_auf_kapitel.png" description="Verteilung der häufigsten Figuren (> 100) über die Kapitel" %}

<div class="todo_must">
TODO
- Voyant-Analyse ausführen und erläutern
</div>


### 3.2.9. Aussagen über Figuren erheben

Wie oben schon angedeutet, bieten Konkordanzen (die Textumgebung, in der Figuren genannt werden) eine gute Möglichkeit, mehr über einzelne Figuren zu erfahren. Die Möglichkeit, alle Konkordanzen ergebnisoffen zu lesen und zunächst kategorienfrei "interessante" Stellen zu markieren, ist vor allem dann sinnvoll, wenn der Gefahr entgegengewirkt werden soll, Kategorien zu verwenden, die aus irgendeinem Grund dem Text nicht angemessen sind. Ein eher formales Beispiel hierfür wäre eine Kategorisierung in "falsch" und "richtig" auf grammatischer Ebene, die die Pronominalisierung von "es" für "Heidi" als "falsch" annotieren würde. Ohne Perspektivierung, dass dies aus heutiger oder aus Sicht der Standardgrammatik falsch ist, wäre dies unangemessen. Angemessenheit der verwendeten Kategorien leitet sich ansonsten hauptsächlich aus der Fragestellung ab. Dementsprechend sind nur solche Kategorien angemessen, die es erlauben, die Fragestellung konstruktiv zu bearbeiten.

Wie wir eingangs dargestellt haben, soll das Personenverzeichnis auch Aussagen darüber treffen, wie eine Figur jeweils charakterisiert wird. Im Zusammenhang gelesene Konkordanzen sind hierfür sehr gut geeignet, wie die Charakterisierungen in [Zwischenergebnis 3](#zwischenergebnis-3) zeigen. Da es häufig zu zeitaufwendig ist, alle Konkordanzen zu lesen, können auch hier frequenzbasierte Strategien zum Einsatz kommen, indem für jede Figur geprüft wird, welche Wörter besonders häufig in ihrer Umgebung vorkommen. Hierauf wird unter [Erweiterungen](#5-erweiterungen) näher eingegangen


# 4. Figurenverzeichnis aus Ergebnissen der Textanalyse erstellen

<div class="todo_must">
TODO:
- Wörterbuchartige Liste (als Tabelle, darin auch Häufigkeitsverlauf von Voyant verarbeiten)
</div>


# 5. Erweiterungen

## 5.1. Komplexere Abfragestrategien

Die Auswertung von attributiven Adjektiven und von Ko-Okkurrenzen gehören unterschiedlichen Strategien an:

**<a name="strategie_1" class="default_text_color">Strategie 1</a>: Wortformen und/oder Lemmata zählen und auswerten, die in einem syntaktischen Verhältnis zum Suchwort stehen**, z. B.
   1. attributive Adjektive
   2. Prädikate inkl. Prädikativen in Sätzen, deren Subjekt die gesuchte Figur ist

**<a name="strategie_2" class="default_text_color">Strategie 2</a>: Wortformen und/oder Lemmata zählen und auswerten, die in der Nähe eines bestimmten Suchausdrucks auftreten (ohne dass das syntaktische Verhältnis zum Suchausdruck berücksichtig wird)**, z. B.
   1. Wörter im selben Satz wie die Figur
   2. Wörter, die in einem bestimmten Umkreis auftreten (z. B. 5 Wörter links und 5 Wörter rechts)

Sowohl Strategie 2.1 als auch Strategie 2.2 ruhen auf der Auswertung von Ko-Okkurrenzen (bzw. Kollokationen, falls das gemeinsame Auftreten als konventionalisiert verstanden werden kann wie z. B. das gemeinsame Auftreten von "Zähne" und "putzen".)

"Auswerten" kann in diesem Zusammenhang unterschiedliche Vorgehensweisen bezeichnen: Eine Wortliste nach Häufigkeit zu ordnen ist bereits eine Form der Auswertung der Zählung. Eine Wortliste nach Wortart und dann nach Häufigkeit zu ordnen, ist eine weitere Möglichkeit. Auf diese Weise können z. B. sehr gut Autosemantika von Synsemantika getrennt betrachtet werden, was die Thesenbildung darüber ermöglicht, worum (= Substantive) es im Text oder einem Textabschnitt geht und welche Bewertungen eine Rolle spielen (= Adjektive, adverbial gebrauchte Adjektive). Eine weitere Form der Auswertung wäre zu berechnen, ob die Häufigkeit, mit der eine Wortform oder ein Lemma mit einem Suchausdruck zusammen auftritt, statistisch signifikant ist (= überzufällig häufig bzw. häufiger als aufgrund des vorliegenden Wortmaterials erwartet). Anmerkung: Geht das Forschungsinteresse über Muster auf der Ebene der Lexik hinaus, können z. B. auch statistisch signifikante Ko-Okkurrenzen von Wortarten berechnet werden. Auch diese Berechnungen können vergleichend für bestimmte Umgebungen durchgeführt werden. Es können also z. B. Sätze, in denen eine bestimmte Figur bzw. ein bestimmter Suchausdruck auftritt, mit Sätzen verglichen werden, wo dies nicht der Fall ist oder in denen eine bestimmte andere Figur bzw. Suchausdruck auftritt. Auch hier können die Umgebungsbeschränkungen weiter differenziert werden, also z. B. der Verlauf über den Text in Kapitel oder einer ähnlichen Einteilung untersucht werden. 

Je nach Forschungsinteresse und Fragestellung spielt das Verstehen der Wortformen und Lemmata im Textzusammenhang eine große Rolle (= hermeneutische Interpretation). Alle genannten Unterstrategien können daher auch als Grundlage verstanden dafür verstanden werden, wie die vielversprechendsten Konkordanzen gefunden werden können. Diese werden dann wie oben bereits dargestellt im Zusammenhang gelesen und interpretiert.
   
Beide Strategien bzw. auch alle Unterstrategien können zu aussagekräftigen Ergebnissen führen. Die folgenden Tabellen präsentieren einen Überblick über die Strategien und die (technischen) Voraussetzungen für ihre Anwendung.

{% include strategie_1.html %}

**Anmerkungen zu Strategie 1**

Der Vorteil der [ersten Strategie](#strategie_1) kann darin liegen, dass die Ergebnisse eher direkt im Hinblick auf die Figur interpretiert werden können. Allerdings hängt dies in der zweiten Variante der ersten Strategie davon ab, dass möglichst alle Sätze korrekt geparst (= automatisch mit Zusatzinformation bezüglich der syntaktischen Relationen versehen) wurden. Eine weitere Hürde stellt die Abfrage und Weiterverarbeitung der Abfrageergebnisse dar. Das Korpusverwaltungssystem muss Abfragen ermöglichen, die als Ergebnis das gesamte Prädikat ausgeben.

*Anmerkung zu Strategie 1.1:*

Nominaler Kern ist jeweils &quot;Tochter&quot;. In 1b wird die NP &quot;die kleine Tochter&quot; durch die NP
&quot;der glücklichen Eltern&quot; ergänzt. Gezählt werden nun alle Ausdrücke außer &quot;Tochter&quot;. Wenn 1a und 1b in einem Text auftreten würden, wären die Frequenzen der Wortformen also:

- die: 2
- kleine: 2
- der: 1
- glücklichen: 1
- Eltern: 1

Die Zählung von Lemmata würde ergeben:

- d: 3 [&quot;d&quot; wird als Abkürzung für den bestimmten Artikel in manchen Lemmatisierern verwendet]
- glücklich: 3 [jeweils Lemma von &quot;glückliche&quot; und &quot;glücklichen&quot;]
- Eltern: 1

Voraussetzungen für die Nutzung:

Die Konstituenten (Phrasen) der einzelnen Sätze müssen mit einem Parser ausgezeichnet werden. Anforderungen an die Abfragemöglichkeiten: Die Ergebnisse der Abfragen müssen auf Tokenebene gezählt werden können. Möglichkeiten sind:
- die Tokens der Phrasen können direkt in der Arbeitsumgebung als Frequenzliste dargestellt werden
- die Phrasen können als Textdatei heruntergeladen werden und dann als neuer Text in WebLicht oder einem anderen Werkzeug in Tokens zerlegt werden.

*Anmerkung zu Strategie 1.2:*

Wie in Beispiel 1 wird wieder alles außer dem Subjekt gezählt:

- spielte: 1
- war: 1
- glücklich: 1

Voraussetzungen für die Nutzung:
Die Relationen zwischen den Satzkonstituenten müssen mit einem Parser ausgezeichnet werden. Die	Relationen müssen so abgefragt werden können, dass sie die Konstituenten zählbar ausgeben.


{% include strategie_2.html %}

**Anmerkungen zu Strategie 2**

Bei der [zweiten Strategie](#strategie_2) kann nicht davon ausgegangen werden, dass sich alle Wörter direkt auf die Figur bzw. den Suchausdruck beziehen. Dies ist vor allem bei der zweiten Variante der Fall, da hier auch satzübergreifend benachbarte Wörter berücksichtigt werden, die unter Umständen eine Figur charakterisieren, die im Satz zuvor genannt wurde. Dies ist vor allem dann der Fall, wenn eine hohe Zahl von Wörtern links und rechts vom Suchausdruck in die Zählung mit einfließt.

*Anmerkungen zu Strategie 2.1*

Die Abfragesprache muss es erlauben, einen Umkreis um einen Suchausdruck herum zu definieren.

*Anmerkungen zu Strategie 2.2*

Der Text muss auf die inhaltlichen Kriterien hin annotiert werden um die relevanten Textausschnitte in einer Abfrage ansprechen zu können. Diese Form der Aufbereitung ist sehr zeitaufwendig, da der gesamte Text entsprechend annotiert werden muss. Als Hilfe für die Annotationsaufgaben kommen externe Werkzeuge in Frage, z. B.: WebAnno (online verfügbar nutzbar unter](https://webanno.sfs.uni-tuebingen.de), die lokal nutzbare Weiterentwicklung von WebAnno, [INCEpTION](https://inception-project.github.io/), oder das eher für literaturwissenschaftliche manuelle Annotation entwickelte und online nutzbare System [CATMA](https://catma.de/). Einen Überblick über Annotationsaufgaben bietet das Tutorial [Lehrpfad Annotation](https://stegmeier.github.io/clariah_annotation_tutorial/#3annotation-in-den-geisteswissenschaften) und das Tutorial ["Manuelle Annotation"](https://fortext.net/routinen/methoden/manuelle-annotation) der Plattform [forText](https://fortext.net). Für die Arbeit mit den einzelnen Werkzeugen stehen jeweils eigene Tutorials und Handbücher zur Verfügung, die über die jeweiligen Webseiten zugänglich sind.

Das weitere Vorgehen hängt dann davon ab, in welcher Umgebung annotiert wurde und welche Auswertungsmöglichkeiten die jeweilige Plattform bietet. INCEpTION erlaubt z. B. den Import von TCF-Dateien (= Standardausgabeformat von WebLicht) oder auch die Einbindung von WebLicht-Tools. Alle Annotationsebenen können in INCEpTION über Korpussuchen angesprochen werden. Die relevanten Textteile können aber auch als Subkorpus aus der Annotationsplattform extrahiert und dann in WebLicht als neues Korpus analysiert werden. Sollen die relevanten Textteile geparst werden, ist es jedoch wichtig, möglichst immer vollständige Sätze zu extrahieren.

Wenn Texte in relevante Teile zerlegt werden, die z. B. ganze Textabschnitte umfassen, ist dies eine Art der strukturellen Annotation. Es kann daher durchaus lohnend sein, die Annotationen im XML-Format vorzunehmen oder als solche auszugeben und den strukturierten Text in ein Korpusverwaltungssystem wie [CQPWeb](https://cwb.sourceforge.io/cqpweb.php) zu importieren, da es in solchen Systemen möglich ist, Abfragen auf bestimmte Textteile zu beschränken oder aus bestimmten Textteilen Subkorpora zu erstellen.

## 5.2. Netzwerke von Figureninteraktionen
<div class="todo">
- Netzwerke 
  - welche Figuren treten häufig miteinander auf?
  - welche Wörter treten häufig mit welcher Figur auf?
  - Netz aus Figuren und häufigsten Kollokationen
</div>

## 5.3. Ergebnis als XML-Ressource erstellen (statt Tabelle)
<div class="todo">
- prüfen, ob es einen einfachen TEI-Standard für solche Ressourcen gibt
</div>

<div class="todo">
  - Metadaten aus anderen Quellen (z. B. GND) etc.) einbinden (in Verzeichnis und/oder in Korpus)
    - GND-Abfrage basteln
      - curl https://lobid.org/gnd/search?q=Heidi -o "test_heidi_gnd.txt" findet zwar allerhand Zeug, darunter auch Verweise auf das Buch, mir ist aber noch nicht gelungen, die Abfrage auf die Figur "Heidi" zu beschränken
      - Laut Wikipedia kann der Entitätentyp "Person" (Kürzel: "p") weiter unterteilt werden, wobei literarische Figuren als "pxl" codiert werden (s. https://de.wikipedia.org/wiki/Gemeinsame_Normdatei#Entit%C3%A4tencodierung")
      - wie dies als Filter eingesetzt wird, habe ich aber noch nicht verstanden
</div>

# 6. Übertragbarkeit auf andere Forschungsinteressen


<div class="todo_must">
TODO:
- vor allem darauf hinweisen, dass die quantitativen Abfragen auch zu Beginn eines Vorhabens ausgeführt werden können, um Suchausdrücke zu identifizieren, die von Interesse für die Fragestellung sind (Baker's semantisch klassifizierte Wortformen, Lemma-Liste von Heidi)
- kurz zeigen, dass die Vorgehensweise immer angewendet werden kann, wenn es um Begriffsbestimmung im weitesten Sinn geht
- auf Annotationslehrpfad verweisen
- evtl. Bakers Fuchsjagd kurz als Beispiel dafür zeigen, dass auch hier Ko-Text-Analysen (gepaart mit Metadaten) die Grundlage der Vorgehensweise bilden 
</div>