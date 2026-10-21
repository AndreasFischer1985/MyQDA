# MyQDA - Text-Annotation-Tool

[MyQDA](https://andreasfischer1985.github.io/MyQDA/src/MyQDA.html) ist ein Open-Source-Tool für die qualitative Datenauswertung (QDA), welches die Durchführung KI-basierter Inhaltsanalysen nach [Fischer (2025)](https://doi.org/10.25656/01:34405) auf eine strukturierte, transparente und digital souveräne Art und Weise ermöglicht. Das gesamte Tool ist vollständig in einer einzigen HTML-Datei beschrieben und offen einsehbar – ein entscheidender Vorteil für nachvollziehbare und replizierbare wissenschaftliche Analysen.

---

## 💡 Grundgedanke & Philosophie

Im Mittelpunkt steht die Prämisse, dass KI-basierte Analysen stets unter **menschlicher Verantwortung** erfolgen müssen („Human-in-the-Loop“). MyQDA unterstützt gezielt die Nachvollziehbarkeit und Validität KI-generierter Ergebnisse durch folgende Kernmerkmale:

* **Verpflichtende Belege:** Standardmäßig werden Textstellen als wörtliche Zitate von der KI eingefordert.


* **Manuelle Editierbarkeit:** Alle KI-generierten Ergebnisse, Dokumente und Kodierungen sind jederzeit manuell editierbar.


* **Transparente Validierung:** Bei automatisierter Annotation wird transparent darauf hingewiesen, falls eine Textstelle im Korpus nicht oder nur über Fuzzy-Matching gefunden werden konnte.


* **Digitale Souveränität:** Durch die Unterstützung lokaler Open-Weights-Modelle (z. B. via LMStudio, Ollama oder Jan.ai) ist eine datenschutzkonforme und kostenfreie Analyse auf eigener Infrastruktur möglich.



---

## 🚀 Erste Schritte & Installation

Da MyQDA als eigenständige HTML-Datei vorliegt, ist keine komplexe Installation oder Einrichtung von Servern und Datenbanken erforderlich:

1. Öffnen Sie die aktuelle Version online ([https://andreasfischer1985.github.io/MyQDA/src/MyQDA.html](https://andreasfischer1985.github.io/MyQDA/src/MyQDA.html)) oder speichern Sie die HTML-Datei lokal.
2. Öffnen Sie die Datei z.B. per Doppelklick in einem modernen Webbrowser (z. B. Chrome, Firefox, Edge).
3. Verbinden Sie das Tool optional mit einem lokalen oder externen KI-Server (z.B. über LMStudio), um KI-gestützte Inhaltsanalysen durchzuführen.

### KI-Server (am Beispiel Jan.ai)
Wenn man MyQDA beispielsweise mit einem lokalen KI-Server per Jan.ai nutzen möchte, muss Jan.ai unter [https://www.jan.ai/](https://www.jan.ai/) herunterladen, installieren und einrichten (für Fragen in diesem Zusammenhang sei auf die Dokumentation von Jan.ai verwiesen). Anschließend muss man in Jan.ai unter „local API Server“ neben CORS enabled (true) unter „Configuration“ noch ein Sternchen (*) bei den trusted hosts eintragen. Außerdem legt Jan.ai Wert darauf, dass das Modell in MyQDA exakt benannt wird (z.B. gemma-3-1b-it-Q4_K_M.gguf) und auch der Endpunkt muss in MyQDA natürlich adäquat angegeben werden (http://127.0.0.1:1337/v1/chat/completions). 

Mit diesen Einstellungen lässt sich ein local API Server per Jan.ai starten (Button „Start Server“), der sich für KI-basierte Inhaltsanalysen in MyQDA nutzen lässt. 

Verbreitete Alternativen zu Jan.ai stellen z.B. LMStudio (wo man in den Settings zu Model Server *Enable CORS* aktivieren muss), Ollama (wo man *set "OLLAMA_ORIGINS=*"* setzen muss), oder - im Rahmen von Command-Line-Interfaces - llama.cpp dar.


---

Hier ist der ergänzte Abschnitt für die Anleitung, der die Kernfunktionen von MyQDA übersichtlich beschreibt:

---

### 🛠️ Grundfunktionen von MyQDA im Überblick

Die Benutzeroberfläche von MyQDA ist intuitiv aufgebaut und gliedert sich in eine linke Seitenleiste (für Dokumente und Codes) sowie das Hauptfenster (zur Textanzeige und Bearbeitung).

* **Einlesen von Dokumenten:**
Über den Button „➕ Hinzufügen“ in der Dokumenten-Leiste können Sie neue Dokumente manuell anlegen, einzelne TXT- oder PDF-Dateien importieren sowie ganze Ordnerstrukturen einlesen. Anschließend lassen sich Dokumente per Checkbox gezielt für die KI-Analyse anwählen oder ausschließen.


* **Anlegen & Verändern von Codes:**
Codes werden über die Code-Leiste („➕ Hinzufügen“) erstellt. Per Drag-and-Drop können Codes hierarchisch verschachtelt werden (um Untercodes darzustellen). Über die Bearbeitungsoptionen (✏️) lassen sich Code-Namen und zugehörige Markierungsfarben individuell anpassen.


* **Annotieren:**
Wählen Sie einen Code in der Liste aus, markieren Sie eine relevante Textstelle im Hauptfenster und klicken Sie auf **✅ Annotieren**. Alternativ können Sie Textstellen auch direkt per Drag-and-Drop auf einen Code ziehen. Die Annotationen werden direkt im Text farblich hinterlegt.


* **Deannotieren:**
Um eine bestehende Kodierung zu entfernen, markieren Sie den entsprechenden annotierten Textabschnitt und klicken Sie auf **🚫 Deannotieren**.


* **Textstellen, Statistiken und KI-basierte Inhaltsanalyse**
* Über **🔍 Textstellen** öffnen Sie eine strukturierte Übersicht aller Fundstellen und Zitate im Korpus, sortiert nach Codes.


* Der Button **📈 Statistik** liefert eine quantitative Auswertung der Nennungs- und Kodiereihäufigkeiten im Korpus.

* Der Button **🤖 KI** öffnet Einstellungen für eine KI-basierte Inhaltsanalayse nach Fischer (2025), auf die im Folgenden noch genauer eingegangen wird.
  
---

### 📖 KI-basierte Inhaltsanalyse 


Das von Fischer (2025) vorgeschlagene Ablaufmodell für die KI-gestützte qualitative Inhaltsanalyse gliedert sich in sechs systematische Phasen, die direkt in MyQDA abgebildet werden:

### 1. Kontext & Vorbereitung

* **Forschungsfrage & Korpus:** Definieren Sie in den Analyse-Einstellungen Ihre Forschungsfrage/Ihren Kontext und markieren Sie die hierfür relevanten Dokumente im Korpus.


* **Modellwahl:** Wählen Sie ein geeignetes KI-Modell (z. B. aus der Gemma- oder Llama-Familie). Für eine möglichst hohe Replizierbarkeit und Reduktion stochastischer Effekte wird empfohlen, den Parameter *Temperature* auf `0.0` zu setzen.



### 2. Wahl der Analysetechnik

MyQDA unterstützt die vier zentralen Grundtechniken nach Fischer (2025), die in der Praxis auch kombiniert werden können (z.B. durch Analysen höherer Ordnung):

* **Zusammenfassung:** Verdichtung des Materials auf das Wesentliche durch Reduktion redundanter Aussagen.


* **Explikation:** Hinzufügen von Kontext, Erklärungen, Übersetzungen oder Zusatzmaterialien zu spezifischen Textteilen.


* **Induktion von Kategorien:** Ableitung emergenter Kategorien und Konzepte direkt aus den Textdaten.


* **Deduktion zu Kategorien:** Anwendung bereits vorhandener, theoretischer Kategoriensysteme und Regeln auf das Textkorpus.

Weitere Informationen zur KI-basierten Inhaltsanalyse und wissenschaftliche Referenzen finden sich auf Github beispielsweise unter [https://github.com/AndreasFischer1985/AI-based-Content-Analysis](https://github.com/AndreasFischer1985/AI-based-Content-Analysis)

### 3. Festlegung der Einheiten

* **Kodiereinheit:** Bestimmung der Textteile, die separat kodiert oder besprochen werden sollen.


* **Kontexteinheit:** Zuordnung der Einheit zum übergeordneten Material oder Fall.


* **Verarbeitungseinheit:** Entscheidung, ob das Material im Rahmen einer Massenverarbeitung (Verarbeitungseinheit 'Korpus'), Dokument für Dokument (Verarbeitungseinheit 'Dokument') oder separat für bereits annotierte Textstellen (Verarbeitungseinheit 'Segment') analysiert werden soll.



### 4. Prozess (Prompting & Verarbeitungsspezifikation)

* **Vorverarbeitung:** Aufbereitungs und Einbettung der Daten in vordefinierte Prompt-Templates (die Sie in MyQDA bedarfsgemäß anpassen können).


* **Verarbeitung:** Ausführung der Analyse über den KI-Dialog in MyQDA (wahlweise mit Live-Streaming via SSE).


* **Nachverarbeitung:** Extrahieren der Ergebnisse (standardmäßig im JSON-Format und aufbereitet für das optionale Übernehmen oder Annotieren der KI-generierten Ergebnisse als Codes).



### 5. Implementierung & Monitoring

* Fortlaufende Protokollierung und Überwachung der Prozesse.


* Bei Bedarf sollten die vorangegangenen Schritte wiederholt werden um zielführend Prompts, Parameter oder sonstige Optionen anzupassen.



### 6. Evaluation & Export

* **Validierung:** Kritische Überprüfung der KI-generierten Ergebnisse und Zitate (manuelle vollständige oder stichprobenhafte Prüfung der KI-generierten Antworten - in MyQDA unterstützt durch automatische Überprüfung im Zuge der automatisierten Annotation KI-generierter Codes).


* **Report und/oder QDPX-Export:** KI-basierte Analysen werden in MyQDA direkt als Dokumente angelegt, die für die Berichtslegung oder für Analysen zweiter Ordnung verwendet werden können. Exportieren Sie Ihr abgeschlossenes Projekt optional auch inklusive aller Dokumente, Codes und Annotationen im standardisierten REFI-QDA-Format (`.qdpx`), um die Daten nahtlos in andere QDA-Programme (wie ATLAS.ti oder MAXQDA) zu übertragen.



---

## 📜 Lizenz & Zitiervorschlag

* **Lizenz:** Open Source (tba...)


* **Methodische Grundlagen:** Bitte zitieren Sie bei der Verwendung des Ansatzes die zugrundeliegende Methodik nach Fischer (2025):
> Fischer, A. (2025). *Die Zukunft der Qualitativen Inhaltsanalyse im Zeitalter Künstlicher Intelligenz. Ein Ablaufmodell KI-basierter Inhaltsanalyse*. f-bb-online, 03/25. DOI: [10.25656/01:34405](https://doi.org/10.25656/01:34405)
> 
>
