---
title: Git für Nicht-Programmierer
theme: white
transition: 'fade'
---

# <span style="font-size: 7rem;">👋</span>

Note:
Hallo an alle
Vorstellungsrunde (bisherige Erfahrungen mit/Erwartungen an Git)
Erwartungsmanagement:
Git ist kompliziert
Kann nichts kaputtgehen - nur Mut

---

# <span style="font-size: 7rem;">2️⃣ Exkurse</span>

Note:
2 kleine Ausflüge zum Thema "Dateien" notwendig

---

# 2 Kategorien von Dateien

<br><br>
<div style="display: flex; justify-content: space-between;">
<h2 class="fragment">📝 Textdateien</h2>
<h2 class="fragment">🧮 Binärdateien</h2>
</div>

Note:
Dateien können in zwei Kategorien eingeteilt werden
Reinschauen: Text-Datei und SVG-Datei
Reinschauen: Pixelgrafik und Audiodatei
Unterschied: Textdateien können im Texteditor angeschaut werden und von Menschen gelesen werden. Binärdateien zeigen nur Quatsch an.

---

# Markdown

\# Überschriften (mehrere Ebenen)
**\*\*Fett\*\***
*\*Kursiv\**
\`Code\`
\> Zitat
Aufzählung (Nummeriert oder Bullets)
\[Links\]\(www.google.de\)
Bilder


Note:
Einfaches Textdateiformat (.md) um die STRUKTUR von Texten auszuzeichnen (NICHT das genaue Design/die Optik)
Unabhängig von einem physikalischen Medium (nicht wie Word)
Für Menschen gemacht (einfacher als HTML/XML weil kurze Steuerzeichen und kein Open/Close Tag notwendig)
Gut für Dokumente, wo der Inhalt zählt, nicht die Optik: Protokolle, Notizen, Verträge, Satzungen, Blogposts, Anleitungen, Präsentationen
Google: Markdown Cheatsheet

---

#### Finally...
# Git


Note:
Ausflug vorbei, back to Topic
Git ist eine verteilte Versionsverwaltung
Erfunden von Linus Torvalds (Linux-Erfinder) für die Linux-Entwicklung in 2005
Git ist ein Kommandozeilenprogramm
Git besteht aus einem Server und einem Client
Normalerweise: Server ist einer der großen Anbieter, Client ist der Entwickler mit seiner Kommandozeile
Git und GitHub/GitLab/Gitea/Bitbucket sind zwei unabhängige Dinge
94% aller Software-Entwickler verwenden Git als primäre Versionskontrolle (2022)
=> Git wird auch außerhalb von der Entwicklung eingesetzt


---

# Welche Probleme löst Git?

- Kollaboration
    - Mehrere Personen bearbeiten gleiche Datei (in unterschiedlichen Abschnitten)
    - Mehrere Personen bearbeiten gleiche Datei (im gleichen Abschnitt)
    - Mehrere Versionen/Stände des Projektordners parallel existieren lassen (Person A und Person B machen unabhängig jeweils Änderungen an einem Repo)
- Nachvollziehbarkeit (History) von Änderungen (+ Metadaten z.B. WARUM)


Note:
Graphen zeichnen?!

---

# Git Lingo Basics

- Repository (Repo)
- Commit
- Branch
- Fork


Note:
Repository: Top Level Einheit (Projekt)
Commit: Ein "Eintrag" im Zeitstrahl/History
Branch: Eine parallele, unabhängige Version aller Dateien (innerhalb eines Repos), die zu einem gewissen Zeitpunkt abgezweigt wird
Fork: Eine parallele, unabhängige Version eines kompletten Repos (inkl. aller Branches), die zu einem gewissen Zeitpunkt abgezweigt wird
Graphen zeichnen?!

---

# Plattformen

<div style="font-size: 0.7em">

| Name        |    GitHub    |     GitLab     |   Bitbucket  | Gitea/Forgejo |
|-------------|:------------:|:--------------:|:------------:|:-------------:|
| Firma       | 🇺🇸&nbsp;Microsoft | 🇺🇸&nbsp;GitLab Inc. | 🇦🇺&nbsp;Atlassian |  🏳️‍🌈&nbsp;Community |
| Self Hosted |       ❌      |        ✅       |       ❌      |       ✅       |
| SaaS        |       ✅      |        ✅       |       ✅      |  🏔️&nbsp;(Codeberg) |
| Gegründet   |     2008     |      2011      |     2012     |      2016     | 

</div>


Note:
Bisher alles Kommandozeile – nicht so schön
Fast alles was in Platformen passiert kann auch via Kommandozeile gemacht werden
Schauen wir uns GitHub an
Meta-Funktionen (nicht Teil von git):
- Issues/Tickets
- Diskussionen
- Actions
- Wiki

---