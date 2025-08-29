# Barrierefrei Leitfaden
Mit diesem Leitfaden stellst du sicher, dass deine Seiten klar, verständlich und für alle Nutzer zugänglich sind.

- [Barrierefrei Leitfaden](#barrierefrei-leitfaden)
	- [Grundgerüst](#grundgerüst)
		- [Landmarken](#landmarken)
		- [ARIA-Attribute](#aria-attribute)
	- [Tastatursteuerung](#tastatursteuerung)
		- [Fokus-Reihenfolge](#fokus-reihenfolge)
		- [Skip Link](#skip-link)
	- [Überschriften](#überschriften)
	- [Links](#links)
		- [Aussagekräftige Linktexte](#aussagekräftige-linktexte)
		- [Kontext und Redundanz](#kontext-und-redundanz)
		- [Icon-only Links](#icon-only-links)
		- [Kein Title-Tag verwenden](#kein-title-tag-verwenden)
		- [Verwendung von .sr-only](#verwendung-von-sr-only)
		- [Zusätzliches ARIA-Attribut](#zusätzliches-aria-attribut)
	- [Bilder und Grafiken](#bilder-und-grafiken)
		- [Bildbeschreibungen](#bildbeschreibungen)
		- [ARIA-Attribute bei Bilden](#aria-attribute-bei-bilden)
		- [Responsive Bilder](#responsive-bilder)
		- [(Komplexe) Grafiken](#komplexe-grafiken)
		- [Bilder mit Text](#bilder-mit-text)
	- [Videos](#videos)
	- [Modale Dialoge und Popups](#modale-dialoge-und-popups)
	- [Formulare](#formulare)
	- [Visuelle Barrieren](#visuelle-barrieren)
		- [Farbkontrast](#farbkontrast)
		- [Sehbeeinträchtigung](#sehbeeinträchtigung)
		- [Farbenblindheit](#farbenblindheit)
	- [Kognitive Barrieren](#kognitive-barrieren)
		- [Legasthenie](#legasthenie)
		- [Leichte Sprache](#leichte-sprache)
	- [Barrierefreie Dokumente](#barrierefreie-dokumente)
	- [Rechtliche Vorgaben](#rechtliche-vorgaben)
		- [Barrierefreierklärung](#barrierefreierklärung)
		- [Navigationshinweise](#navigationshinweise)
		- [Barriere melden](#barriere-melden)
	- [Tests](#tests)
		- [Screenreader-Test](#screenreader-test)
		- [Keyboard-Navigation](#keyboard-navigation)
		- [Automatisierte Tools](#automatisierte-tools)
	- [Checkliste](#checkliste)

## Grundgerüst
### Landmarken
Nutze die nativen HTML5-Elemente als Landmarken um semantische Regionen zu definieren, wann immer möglich. Screenreader erkennen sie automatisch und Nutzer können per Shortcut schnell zwischen Landmarks springen und gezielt Bereiche wie Navigation oder Hauptinhalt erreichen.
- **Banner**

	Oberster Bereich der Seite enthält Logo und Hauptnavigation.
	```html
	<!-- Landmark wird automatisch erkannt-->
	<header>…</header>

	<!-- oder Landmark wird in <div> nicht erkannt um muss ergänzt werden.-->
	<div class="header" role="banner">…</div>
	```
- **Navigation**

	Bereich für die Haupt- oder Seitennavigation. Ermöglicht das gezielte Ansteuern verschiedener Seitenbereiche oder Inhalte.
	```html
	<nav>…</nav> <!-- oder --> <div role="navigation">…</div>
	```

	`aria-label` differenziert mehrere Navigationen.
	```html
	<nav aria-label="Hauptnavigation">…</nav>
	<nav aria-label="Fußnavigation">…</nav>
	```



- **Main**

	Beinhaltet den zentralen Inhalt und darf nur einmal pro Seite benutzt werden.
	```html
	<main>…</main>  <!-- oder -->  <div role="main">…</div>
	```
- **Footer**

	Fußbereich der Seite mit ergänzenden Informationen wie Impressum, Kontakt oder Copyright.
	```html
	<footer>…</footer>  <!-- oder -->  <div role="contentinfo">…</div>
	```
- **Aside**

	Ergänzende Inhalte, die den Hauptinhalt unterstützen (z. B. Sidebar)
	```html
	<aside>…</aside>  <!-- oder -->  <div role="complementary">…</div>
	```
- **Section**

	Abschnitt für thematisch zusammengehörige Inhalte, meist mit Überschrift. Hilft, die Seite logisch zu gliedern und die Orientierung für alle Nutzer zu verbessern.
	```html
	<section>…</section>  <!-- oder -->  <div role="region">…</div>
	````
- **Search**

	Bereich für die Seitensuche
	```html
	<search>…</search>  <!-- oder -->  <form role="search">…</form>
	```

### ARIA-Attribute
Versehe Inhalte mit zusätzlichen Erklärungen wenn notwendig. Wenn die Semantik von HTML nicht ausreicht (z. B. bei mehreren Navigationsbereichen), helfen ARIA-Labels Screenreader-Nutzern, den Zweck zu verstehen.

**Best Practice**
- Zuerst HTML-Semantik nutzen (Label, Überschrift, `<legend>`, `<caption>`, etc).
- ARIA nur ergänzen, wenn es keine native Möglichkeit gibt.
- „No ARIA is better than bad ARIA“.

**Beispiele**
- **aria-label**

	Vergibt eine direkte, unsichtbare Beschriftung für ein Element ohne sichtbaren Text.
	```html
	<!-- Icon-Button ohne sichtbaren Text -->
  <button aria-label="Navigation öffnen">
		<svg aria-hidden="true" …>…</svg>
  </button>

	<!-- Screenreader liest: „Navigation öffnen, Schalter“ -->
	```

	```html
	<!-- Mehrere Navigationsbereiche -->
	<nav aria-label="Hauptnavigation">…</nav>
	<nav aria-label="Fußnavigation">…</nav>
	```
- **aria-labelledby**

	Verknüpft ein Element mit einer bestehenden Beschriftung im Dokument.
	```html
	<section aria-labelledby="kontakt-title">
  	<h2 id="kontakt-title">Kontakt aufnehmen</h2>
  	<p>Hier findest du unser Formular.</p>
	</section>

	<!-- Screenreader liest: „Kontakt aufnehmen, Bereich“ -->
	```
- **aria-describedby**

	Fügt zusätzliche erklärende Hinweise zu einem Element hinzu.
	```html
	<label for="email">E-Mail</label>
	<input id="email" type="email" aria-describedby="email-hint">
	<p id="email-hint">Wir verwenden deine E-Mail nur zur Rückmeldung.</p>

	<!-- Screenreader liest: „E-Mail, Eingabefeld, Wir verwenden deine E-Mail nur zur Rückmeldung“ -->
	```

- **Kombination**

	Manchmal werden mehrere ARIA-Attribute zusammen eingesetzt:
	```html
	<nav aria-label="Hauptnavigation">
		<ul>
			<li><a href="/leistungen">Leistungen</a></li>
			<li><a href="/kontakt">Kontakt</a></li>
		</ul>
	</nav>

	<!-- Screenreader liest: „Hauptnavigation, Liste mit 2 Einträgen …“ -->
	```
---

## Tastatursteuerung

### Fokus-Reihenfolge
Halte die logische Reihenfolge für Tastaturnavigation ein. Viele Nutzer bedienen Webseiten ausschließlich mit Tastatur. Wenn der Fokus nicht sinnvoll gesetzt ist, können Inhalte unzugänglich oder verwirrend sein.
- Links, Buttons, Formulare mit`tabindex` auszeichnen.
- Dekorative Bereiche aus Tastaturnavigation enfernen.

```html
<!-- Link nicht erreichbar-->
<a href="#" tabindex="0">

<!-- Link erreichbar (Reihenfolge automatisch) -->
<a href="#" tabindex="1">

<!-- Link erreichbar (Reihenfolge priorisiert) -->
<a href="#" tabindex="2, 3, 4, …">
```

### Skip Link
Baue eine Sprungmarke zum Hauptinhalt ein. Das erlaubt dem Nutzer direkt zum Inhaltsbereich zu springen.
```html
<a href="#main" class="skip-link">Zum Hauptinhalt springen</a>
```

---

## Überschriften
Halte die Überschriften-Hierarchie ein. Screenreader erlauben Navigation per Überschriften. Eine saubere, logische Struktur erleichtert Orientierung und Verständnis.
  - Überschriften-Reihenfolge einhalten: `<h1>` bis `<h6>`
  - Jede Seite nur eine `<h1>`
  - Logische Gliederung: keine Sprünge von `<h2>` zu `<h4>`.

---

## Links
Verwende sinnvolle, aussagekräftige Linktexte. Screenreader-Nutzer hören oft nur eine Liste von Links.

### Aussagekräftige Linktexte
- Vermeide generische Phrasen
- Linktexte sollten auch ohne umgebenden Kontext Sinn ergeben.
```html
<!-- Falsch: -->
<a href="/download">Hier klicken</a>

<!-- Richtig: -->
<a href="/download">Vereinsbroschüre als PDF herunterladen</a>
```

### Kontext und Redundanz
- Nutze keine doppelten Linktexte auf einer Seite. Verwende unterschiedliche Texte, z. B. „Mehr erfahren zu Training“ und „Mehr erfahren zu Events“ statt zweimal „Mehr erfahren“.
- Linktext dürfen nicht abgeschnitten werden. Ohne sichtbaren Kontext ist nicht klar, was genau passiert („Events anzeigen? erstellen? Infos?“).
```html
<!-- Falsch: -->
<a href="/events">Events …</a>

<!-- Richtig: -->
<a href="/events">Zu unseren Events</a>.
```
### Icon-only Links
Verlinkte Icons ohne sichtbaren Text müssen für Screenreader verständlich gemacht werden. Wenn ein Link oder Button nur aus einem Icon besteht (z. B. ein Haus-Symbol für die Startseite), können Screenreader-Nutzer ohne zusätzliche Maßnahmen nicht erkennen, wohin der Link führt.
```html
<a href="/home" aria-label="Zur Startseite">
	<svg>…</svg>
</a>

<!-- oder -->

<a href="/home">
	<svg>…</svg>
	<span class="sr-only">Zur Startseite</span>
</a>
```
### Kein Title-Tag verwenden
`title`-Attribute sind kein Ersatz. Screenreader lesen `title` oft nicht vor. Nutze stattdessen klaren Linktext oder `aria-label`.

### Verwendung von .sr-only
Zusätzliche Informationen nur für Screenreader
```html
<a href="/terms">
  Nutzungsbedingungen
  <span class="sr-only"> (öffnet Seite mit rechtlichen Hinweisen)</span>
</a>
```

### Zusätzliches ARIA-Attribut
Längere Hinweise außerhalb des Linktextes können über `aria-describedby` definiert werden.
```html
<a href="/mitgliedschaft" aria-describedby="mitgliedschaft-hinweis">
  Mehr zur Mitgliedschaft
</a>
<span id="mitgliedschaft-hinweis">
  Die Seite enthält Informationen zu Beiträgen, Vorteilen und Kündigungsfristen.
</span>
```

---

## Bilder und Grafiken

### Bildbeschreibungen
Erstelle Textalternativen [alt-Attribute] für Bilder. Screenreader lesen Alt-Texte bei Bildern vor, sodass blinde oder sehbehinderte Nutzer verstehen, was ein Bild aussagt.
- Der Alt-Text soll den Informationsgehalt knapp und präzise wiedergeben.
- Der Alt-Text muss bei Bildern immer gesetzt werden, auch wenn er leer ist.
	```html
	<!-- Informatives Bild -->
	<img src="tour.jpg" alt="Radfahrer auf Waldweg bei Sonnenaufgang">
	```
- Dekorative Bilder erhalten einen leeren Alt-Text.
	```html
	<!-- Dekoratives Bild (wird vom Screenreader übersprungen) -->
	<img src="ornament.svg" alt="" />
	```
### ARIA-Attribute bei Bilden
Erstelle zusätzlich erklärenden Inhalt für Grafiken. Mit ARIA-Attributen lassen sich Bilder um zusätzliche erklärende Inhalte ergänzen.
- **aria-describedby**
	```html
	<!-- Verknüpft das Bild mit einer ausführlichen Beschreibung -->
  <img src="map.png" alt="Stadtplan von Berlin" aria-describedby="map-desc">
	<p id="map-desc">Die Karte zeigt Hauptstraßen, Radwege und Parkplätze rund um das Vereinsgelände.</p>
	```
- **role="presentation"**
	```html
	<!-- Bei komplexen SVGs ohne Informationswert benutzen -->
  <img src="icon.svg" alt="" role="presentation" />
	```
- **aria-hidden="true"**
	```html
	<!-- Für dekorative Icons in <span>-Elementen -->
  <span class="icon-dekor" aria-hidden="true"></span>
	```

### Responsive Bilder
Passe Bilder flexibel an unterschiedliche Bildschirmgrößen an. Durch Techniken wie `picture` und `srcset` wird dem Browser die passende Bildvariante geliefert – optimiert für Smartphones, Tablets und Desktops.
```html
<picture>
  <source media="(min-width: 800px)" srcset="large.jpg">
  <img src="small.jpg" alt="Vereinsheim vor Bergkulisse">
</picture>
```

### (Komplexe) Grafiken
Versehe Grafiken und Diagramme semantisch korrekt mit Beschriftung. Umfasse das Bild und seine Beschreibung mit `<figure>` und nutze `<figcaption>` für detaillierte Bildtexte.
```html
<figure>
  <img src="chart.png" alt="Mitgliederzahlen 2019 bis 2024" aria-describedby="desc-chart">
  <figcaption id="desc-chart">Balkendiagramm: Zunahme von 120 auf 250 Mitglieder innerhalb von fünf Jahren.</figcaption>
</figure>
```

### Bilder mit Text
Vermeide wichtigen Text als Grafik. Screenreader und Vergrößerungsprogramme können Textgrafiken nicht erfassen. Nutze stattdessen HTML-Text oder CSS.

---

## Videos
Mache Inhalte für alle Nutzer zugänglich.
- Untertitel von gesprochenem Text in Videos erstellen
- Transkript (Textfassung) des gesprochenen Inhalts und relevanter Geräusche erstellen
- Videoinhalte in Gebärdensprache anbieten, um sie für Gehörlose vollständig zugänglich zu machen.

---

## Modale Dialoge und Popups
Überlagernde Fenster, die den Fokus auf sich ziehen müssen per Tastatur vollständig bedienbar und für Screenreader zugänglich sein.

- Tastatursteuerung ermöglichen
- Hintergrund-Inhalte mit `aria-modal="true"` sperren
```html
<div role="dialog" aria-modal="true" aria-labelledby="dialog-title">
  <h2 id="dialog-title">…</h2>
  …
</div>
```

---

## Formulare
Gestalte Formulare so, dass sie für Screenreader- und Tastaturnutzer vollständig nutzbar sind. Barrierefreie Formulare verwenden eindeutige Labels, logische Fokus-Reihenfolge, klare Fehlermeldungen, Pflichtfeld-Kennzeichnungen und ggf. Hilfetexte oder Live-Regionen. So wird sichergestellt, dass alle Nutzer Daten korrekt und selbstständig eingeben können.

- **Labels**
  Eindeutige `<label>`-Elemente für jedes Feld. Screenreader lesen Labels vor, Nutzer verstehen sofort, wofür ein Feld gedacht ist.

- **Hilfetexte**
  Hinweise mit `aria-describedby` oder unterhalb der Felder. Zusätzliche Infos (z. B. „Mindestens 8 Zeichen“) werden vorgelesen und erleichtern die Eingabe.

- **Fehlermeldungen**
  Klar sichtbar, mit `role="alert"`. Fehler werden sofort erkennbar und auch von Screenreadern angesagt.

- **Pflichtfelder**
  Kennzeichnung mit `required` + visuelle Markierung. Hilft Nutzer zu erkennen, welche Felder notwendig sind – Screenreader geben das ebenfalls aus.

- **Tastaturbedienung**
  Tab-Reihenfolge, logische Navigation. Alle Felder und Buttons müssen in logischer Reihenfolge mit <kbd>Tab</kbd> erreichbar sein.

- **Eindeutige IDs**
  Verknüpfung von `<label>` mit `for` und Feld-ID. Stellt sicher, dass Screenreader die richtige Verbindung zwischen Feld und Label herstellen.

- **Autocomplete**
  Attribute wie `autocomplete="email"` oder `tel`. Unterstützt Assistive Technologien und erleichtert Eingaben durch automatische Vorschläge.

- **Live-Regionen**
  Statusmeldungen mit `aria-live`. Z. B. „Formular erfolgreich gesendet“ wird automatisch angesagt, ohne dass der Fokus springt.

---

## Visuelle Barrieren
### Farbkontrast
Ein ausreichender Farbkontrast zwischen Text und Hintergrund ist notwendig, damit Inhalte auch bei Sehbeeinträchtigungen gut lesbar sind.
- Stelle einen Kontrast von mindestens 4,5:1 (WCAG AA) zwischen Text und Hintergrund sicher.
- Prüfe alle Farben mit einem Kontrast-Checker.
- Vermeide Farbkombinationen mit geringem Kontrast.
- Nutze keine rein farbigen Hinweise ohne ausreichenden Kontrast.

### Sehbeeinträchtigung
Sehbeeinträchtigungen wie geringe Sehschärfe oder Tunnelblick erschweren das Erfassen von Inhalten. Klare Kontraste, flexible Schriftgrößen und eine übersichtliche Struktur helfen, Webseiten für Betroffene zugänglich zu machen.
- Verwende klare Kontraste.
- Erlaube flexible Anpassung der Schriftgröße.
- Strukturiere Seiten übersichtlich.
- Vermeide zu kleine Schriftgrößen.
- Halte ausreichend Abstand zwischen Elementen ein.

### Farbenblindheit
Farbenblindheit erschwert es vielen Menschen, farbliche Unterschiede zu erkennen. Damit alle Inhalte verständlich bleiben, dürfen wichtige Informationen nicht ausschließlich durch Farben vermittelt werden.
- Vermittle Informationen nicht nur durch Farbe.
- Stelle sicher, dass alle Inhalte auch ohne Farberkennung verständlich sind.
- Ergänze Farben immer durch Symbole, Muster oder Texte.
```html
<!-- Beispiel für Ergänzung durch Symbole und Text -->
<div style="color: green;">●</span> <span>Erledigt</div>
<div style="color: red;">✖</span> <span>Nicht erledigt</div>
```

---

## Kognitive Barrieren

### Legasthenie
Menschen mit Legasthenie haben Schwierigkeiten beim Lesen und Verarbeiten von geschriebenem Text. Für sie ist es besonders wichtig, dass Texte gut lesbar gestaltet sind. Folgende Maßnahmen erleichtern Zugang zum Inhalt.
- Verwende klare, gut lesbare Schriftarten.
- Sorge für ausreichend Zeilenabstand.
- Schreibe kurze Absätze.
- Gliedere Texte übersichtlich.

### Leichte Sprache
Leichte Sprache ist ein spezielles Angebot, das komplexe Inhalte vereinfacht und so für viele Menschen mit kognitiven Einschränkungen, Lernschwierigkeiten oder geringen Deutschkenntnissen zugänglich macht.
- Vermeide komplexe Sätze.
- Erkläre oder vermeide Fachbegriffe und Fremdwörter.
- Verwende kurze Absätze und eine klare Gliederung.
- Nenne wichtige Informationen zuerst.
- Schreibe aktiv statt passiv.
- Setze Bilder oder Symbole zur Unterstützung ein.
- Verwende einfache und bekannte Wörter.
- Gliedere lange Texte in überschaubare Abschnitte.
- Lasse Inhalte von Personen mit Lernschwierigkeiten testen.

---

## Barrierefreie Dokumente
**Dokumente (PDF, Word, Präsentationen) mit zugänglicher Struktur versehen**
Damit auch außerhalb von Webseiten Inhalte von Screenreadern lesbar sind – z. B. durch richtige Überschriften-Hierarchie, Alt-Texte, Tags und Lese-Reihenfolge.

---

## Rechtliche Vorgaben
### Barrierefreierklärung

### Navigationshinweise

### Barriere melden
Nicht rechtlich vorgeschrieben, aber sinnvoll: Gib Menschen mit Beeinträchtigungen die Möglichkeit, Barrieren bei der Bedienung der Webseite zu melden, anstatt sich ausschließlich auf automatisierte Tools zu verlassen.

---

## Tests
Mit folgenden Möglichkeiten können Webseiten auf Barrierefreiheit überprüft werden.

### Screenreader-Test
Teste mit NVDA, VoiceOver oder JAWS.

### Keyboard-Navigation
Überprüfe, dass Links per <kbd>Tab</kbd> erreichbar und eindeutig fokussiert sind.

### Automatisierte Tools
aXe, WAVE oder Lighthouse auf fehlende Linktexte prüfen.

---
---

## Checkliste
Die folgende Checkliste hilft dir einzuschätzen, wie zugänglich deine Webseite für Menschen mit Beeinträchtigungen ist.

**Grundgerüst**
- [ ] Semantische Regionen definieren [→ Erklärung](#landmarken)
- [ ] Zusätzliche ARIA-Attribute ergänzen [→ Erklärung](#aria-attribute)

**Tastatursteuerung**
- [ ] Links mit tabindex auszeichnen [→ Erklärung](#fokus-reihenfolge)
- [ ] Buttons mit tabindex auszeichnen [→ Erklärung](#fokus-reihenfolge)
- [ ] Formulare mit tabindex auszeichnen [→ Erklärung](#fokus-reihenfolge)
- [ ] Dekorative Bereiche enfernen [→ Erklärung](#fokus-reihenfolge)
- [ ] Sprungmarke zum Hauptinhalt einbauen [→ Erklärung](#skip-link)

**Überschriften**
- [ ] Überschriften-Reihenfolge einhalten [→ Erklärung](#überschriften)
- [ ] Jede Seite nur eine h1 [→ Erklärung](#überschriften)
- [ ] Logische Gliederung einhalten [→ Erklärung](#überschriften)

**Links**
- [ ] Aussagekräftige Linktexte verwenden ([→ Erklärung](#aussagekräftige-linktexte))
- [ ] Keine doppelten Linktexte [→ Erklärung](#kontext-und-redundanz)
- [ ] Linktexte nicht abschneiden [→ Erklärung](#kontext-und-redundanz)
- [ ] Verlinkte Icons ohne sichtbaren Text beschreiben [→ Erklärung](#icon-only-links)
- [ ] [aria-label] statt [title] benutzen [→ Erklärung](#kein-title-tag-verwenden)
- [ ] Zusätzliche Hinweise mit [.sr-only] beschreiben [→ Erklärung](#verwendung-von-sr-only)
- [ ] Längere Hinweise mit [aria-describedby] definieren [→ Erklärung](#zusätzliches-aria-attribut)

**Bilder und Grafiken**
- [ ] Alt-Text für Bilder erstellen [→ Erklärung](#bildbeschreibungen)
- [ ] Leerer Alt-Text für dekorative Bilder [→ Erklärung](#bildbeschreibungen)
- [ ] Zusätzliche ARIA-Attribute ergänzen [→ Erklärung](#aria-attribute-bei-bilden)
- [ ] Bilder an unterschiedliche Bildschirmgrößen anpassen [→ Erklärung](#responsive-bilder)
- [ ] Korrekte Semantik für Grafiken und Diagramme [→ Erklärung](#komplexe-grafiken)
- [ ] Wichtigen Text als Grafik vermeiden [→ Erklärung](#bilder-mit-text)

**Videos**
- [ ] Untertitel für gesprochenen Text erstellen [→ Erklärung](#videos)
- [ ] Transkript für gesprochenen Text und Geräusche erstellen [→ Erklärung](#videos)
- [ ] Videos mit Gebärdensprache versehen [→ Erklärung](#videos)

**Modale Dialoge und Popups**
- [ ] Tastaturnavigation ermöglichen [→ Erklärung](#modale-dialoge-und-popups)
- [ ] Hintergrund-Inhalte sperren [→ Erklärung](#modale-dialoge-und-popups)

**Formulare**
- [ ] adf

**Visuelle Barrieren**
- [ ] Farbkontrast auf WCAG AA: 4,5:1 überprüfen [→ Erklärung](#farbkontrast)
- [ ] Farbkombinationen mit geringem Kontrast vermeiden. [→ Erklärung](#farbkontrast)
- [ ] Keine farbigen Hinweise ohne ausreichenden Kontrast [→ Erklärung](#farbkontrast)
- [ ] Flexible Anpassung der Schriftgröße. [→ Erklärung](#sehbeeinträchtigung)
- [ ] Strukturiere Seiten übersichtlich. [→ Erklärung](#sehbeeinträchtigung)
- [ ] Kleine Schriftgrößen vermeiden. [→ Erklärung](#sehbeeinträchtigung)
- [ ] Ausreichend Abstand zwischen Elementen. [→ Erklärung](#sehbeeinträchtigung)
- [ ] Vermittle Informationen nicht nur durch Farbe. [→ Erklärung](#farbenblindheit)
- [ ] Stelle sicher, dass Inhalte ohne Farberkennung verständlich sind. [→ Erklärung](#farbenblindheit)
- [ ] Ergänze Farben durch Symbole oder Texte. [→ Erklärung](#farbenblindheit)

**Kognitive Barrieren**
- [ ] Verwende klare, gut lesbare Schriftarten. [→ Erklärung](#legasthenie)
- [ ] Sorge für ausreichend Zeilenabstand. [→ Erklärung](#legasthenie)
- [ ] Schreibe kurze Absätze. [→ Erklärung](#legasthenie)
- [ ] Gliedere Texte übersichtlich. [→ Erklärung](#legasthenie)
- [ ] Erstelle eine Version in leichter Sprache von inhaltlich komplexen Seiten [→ Erklärung](#leichte-sprache)

