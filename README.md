# Assistent-SHK
# 🛠️ Lokale KI-Pipeline für automatisierte SHK-Anfrageassistenz

![Status](https://img.shields.io/badge/Status-In_Development-orange)
![Tech Stack](https://img.shields.io/badge/Tech-Python_|_Ollama_|_Qwen_|_Gemma-blue)
![Focus](https://img.shields.io/badge/Domain-SHK_|_Gebäudetechnik-green)

> **Projektfokus:** Entwicklung einer sicheren, datenschutzkonformen Multi-Agenten-Architektur zur Vorqualifizierung und Beantwortung technischer Kunden- und B2B-Anfragen im SHK-Handwerk.

![Architektur: Soll & Ist](Pipeline-Soll-Ist-fuer-Winter.png)

## 📌 Ausgangslage & Business Value
Fachbetriebe im Bereich SHK (Sanitär, Heizung, Klima) und Stalltechnik binden massive Ressourcen in der manuellen Sichtung unklarer Kundenanfragen, dem Abgleich von B2B-Produktdaten und der Beantwortung wiederkehrender technischer Fragen. Standard-Cloud-KIs scheiden aufgrund fehlenden Fachwissens, mangelnder Mandantentrennung und Datenschutzbedenken aus. 

Dieses Projekt löst das Problem durch eine **vollständig lokal gehostete Multi-Agenten-Pipeline**, die technisches Domänenwissen direkt in den Ausführungsworkflow integriert.

## 🎯 Zielbild (SOLL-Zustand: SHK-Anfrageassistent)
Ein prozesssicherer Assistent, der in drei Stufen arbeitet:
1. **Anfrage vorbereiten:** Synthetische Einordnung der Anfragen und Erkennung fehlender technischer Angaben für gezielte Rückfragen.
2. **Freigegebene FAQ:** Automatisierter Abgleich mit validierten Inhalten und Erstellung eines Antwortentwurfs inkl. Quellenbelegen.
3. **Menschliche Freigabe (Human-in-the-Loop):** Kein automatischer Versand ohne menschliche Endabnahme durch den Fachbetrieb, um Haftungsrisiken auszuschließen.

## ⚙️ Systemarchitektur & Infrastruktur (IST-Stand)
Um volle Datenhoheit zu gewährleisten, ist das System strikt lokal und netzwerkisoliert aufgebaut:
* **Dezentrale Inferenz & Runner:** Trennung der Modellanfragen (Windows-PC via Ollama, z.B. `qwen3.5:4b`) vom Ausführungsserver (CachyOS-Server mit Python-Runner).
* **Sichere Kommunikation:** Verbindung über einen SSH-Rücktunnel.
* **Bubblewrap Sandbox:** Getrennte Probeläufe und Ausführung von Code finden in einer strikt isolierten Umgebung mit harten Ressourcenlimits statt.

## 🤖 Multi-Agenten-Logik & SHK-Fachprüfung
Ein Auftrag durchläuft sequenziell **7 spezialisierte Beratungsrollen**, um höchste Qualität zu sichern:
`Manager` ➔ `Business` ➔ `Architekt` ➔ `Entwickler` ➔ **`SHK-Fachprüfung`** ➔ `Security` ➔ `QA`

*Highlight:* Durch die dedizierte **SHK-Fachprüfung** wird sichergestellt, dass branchenspezifische Parameter (z.B. Heizlasten, Lüftungsquerschnitte) nicht von generischen IT-Entscheidungen des LLMs überschrieben werden.

## 🛡️ Strikte Qualitätssicherung (QA)
Das System verlässt sich nicht auf einfache Textgenerierung, sondern evaluiert die KI-Outputs algorithmisch:
* Ein separates Skript (`qa_review.py`) prüft die Einhaltung der JSON-Schemata und die Belege der Zeilen.
* Unzureichende Ausgaben kleiner Modelle (Qwen/Gemma) werden konsequent als `NOT_QUALIFIED` eingestuft.
* Alle Laufzeiten, Auftragstexte und Rollenentscheidungen werden transparent in einem dedizierten Laufordner dokumentiert.

---

### 👨‍💻 Über den Entwickler
Ich vereine tiefe Branchenkenntnis (Domain Expertise als SHK-Experte & Techniker) mit modernem AI-Engineering, Systemadministration und Vibecoding. Mein Fokus liegt darauf, die Lücke zwischen theoretischen KI-Modellen und dem echten, physischen Handwerks- und B2B-Alltag zu schließen. 

📫 **Kontakt:** [Dein LinkedIn Link] | [Deine E-Mail Adresse]
