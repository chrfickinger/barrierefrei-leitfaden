# Barrierefrei Leitfaden
Mit diesem Leitfaden stellst du sicher, dass deine Seiten klar, verständlich und für alle Nutzer zugänglich sind.

- [Barrierefrei Leitfaden](#barrierefrei-leitfaden)
	- [Grundgerüst](#grundgerüst)
		- [Landmarken](#landmarken)
		- [ARIA-Attribute](#aria-attribute)
		- [Skip Link](#skip-link)
	- [Focus Order](#focus-order)
	- [Überschriften](#überschriften)
	- [Bilder und Grafiken](#bilder-und-grafiken)
		- [Bildbeschreibungen](#bildbeschreibungen)
		- [ARIA-Attribute bei Bilden](#aria-attribute-bei-bilden)
		- [Responsive Bilder](#responsive-bilder)
		- [(Komplexe) Grafiken](#komplexe-grafiken)
		- [Bilder mit Text](#bilder-mit-text)
	- [Links](#links)
		- [Aussagekräftige Linktexte](#aussagekräftige-linktexte)
		- [Kontext und Redundanz](#kontext-und-redundanz)
		- [Icon-only Links](#icon-only-links)
		- [Kein title für Accessibility](#kein-title-für-accessibility)
		- [Verwendung von .sr-only](#verwendung-von-sr-only)
		- [Zusätzliches ARIA-Attribut](#zusätzliches-aria-attribut)
	- [Modale Dialoge und Popups](#modale-dialoge-und-popups)
	- [Formulare](#formulare)
	- [Farbkontrast](#farbkontrast)
	- [Sehbeeinträchtigung](#sehbeeinträchtigung)
	- [Farbenblindheit](#farbenblindheit)
	- [Legasthenie](#legasthenie)
	- [Transkript für Videos](#transkript-für-videos)
	- [Barrierefreie Dokumente](#barrierefreie-dokumente)
	- [Tests](#tests)
		- [Screenreader-Test](#screenreader-test)
		- [Keyboard-Navigation](#keyboard-navigation)
		- [Automatisierte Tools](#automatisierte-tools)

## Grundgerüst
### Landmarken
**Semantische Regionen definieren.** Nutze die nativen HTML5-Elemente als Landmarken, wann immer möglich. Screenreader erkennen sie automatisch und Nutzer können per Shortcut schnell zwischen Landmarks springen und gezielt Bereiche wie Navigation oder Hauptinhalt erreichen.
- **Banner**

	Oberster Bereich der Seite enthält Logo und Hauptnavigation.
	```html
	<!-- Landmark wird automatisch erkannt-->

	<header>...</header>

	<!-- oder Landmark wird in <div> nicht erkannt um muss ergänzt werden.-->

	<div class="header" role="banner">...</div>
	```
- **Navigation**

	Markiert Navigationsbereiche, `aria-label` differenziert mehrere Navs.
	```html
	<nav>...</nav>

	<!-- oder-->

	<div role="navigation">...</div>
	```
- **Main**

	Beinhaltet den zentralen Inhalt und darf nur einmal pro Seite benutzt werden.
	```html
	<main>...</main>

	<!-- oder-->

	<div role="main">...</div>
	```
- **Footer**

	Fußbereich mit Copyright, Impressum.
	```html
	<footer>...</footer>

	<!-- oder-->

	<div role="contentinfo">...</div>
	```
- **Aside**

	Ergänzende Inhalte, die den Hauptinhalt unterstützen (z. B. Sidebar)
	```html
	<aside>...</aside>

	<!-- oder-->

	<div role="complementary">...</div>
	````
- **Section**
	```html
	<section>...</section>

	<!-- oder-->

	<div role="region">...</div>
	````
- **Search**

	Bereich für die Seitensuche
	```html
	<search>...</search>

	<!-- oder-->

	<form role="search">...</form>
	```

### ARIA-Attribute
**Inhalte mit zusätlichen Erklärungen versehen wenn notwendig.**
Wenn die Semantik von HTML nicht ausreicht (z. B. bei mehreren Navigationsbereichen), helfen ARIA-Labels Screenreader-Nutzern, den Zweck zu verstehen.

**Best Practice**
1. Zuerst HTML-Semantik nutzen (Label, Überschrift, `<legend>`, `<caption>`, etc).
2. ARIA nur ergänzen, wenn es keine native Möglichkeit gibt.
3. „No ARIA is better than bad ARIA“.

**Beispiele**
- **aria-label**

	Vergibt eine direkte, unsichtbare Beschriftung für ein Element ohne sichtbaren Text.
	```html
	<!-- Icon-Button ohne sichtbaren Text -->

  <button aria-label="Navigation öffnen">
		<svg aria-hidden="true" ...>…</svg>
  </button>

	<!-- Screenreader liest: „Navigation öffnen, Schalter -->
	```

	```html
	<!-- Mehrere Navigationsbereiche -->

	<nav aria-label="Hauptnavigation">...</nav>
	<nav aria-label="Fußnavigation">...</nav>
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









### Skip Link
**Sprungmarke zum Hauptinhalt einbauen.**
Erlaubt dem Nutzer direkt zum Hauptinhalt zu springen.
```html
<a href="#main" class="skip-link">Zum Hauptinhalt springen</a>
```

---

## Focus Order
**Logische Reihenfolge für Tastaturnavigation einhalten.** Viele Nutzer bedienen Webseiten ausschließlich mit Tastatur. Wenn der Fokus nicht sinnvoll gesetzt ist, können Inhalte unzugänglich oder verwirrend sein.

---

## Überschriften
**Überschriften-Hierarchie einhalten.** Screenreader erlauben Navigation per Überschriften. Eine saubere, logische Struktur erleichtert Orientierung und Verständnis.
  - Überschriften-Reihenfolge einhalten: `<h1>` bis `<h6>`
  - Jede Seite nur eine `<h1>`
  - Logische Gliederung: keine Sprünge von `<h2>` zu `<h4>`.

---

## Bilder und Grafiken

### Bildbeschreibungen
**Textalternativen [alt-Attribute] für Bilder erstellen.** Screenreader lesen Alt-Texte bei Bildern vor, sodass blinde oder sehbehinderte Nutzer:innen verstehen, was ein Bild aussagt.
- Ein alt-Attribut muss bei Bildern immer gesetzt werden, auch wenn es leer ist.

- Der Alt-Text soll den Informationsgehalt knapp und präzise wiedergeben.
	```html
	<!-- Informatives Bild -->

	<img src="tour.jpg" alt="Radfahrer auf Waldweg bei Sonnenaufgang">
	```
- Leerer Alt-Text für dekorative Bilder
	```html
	<!-- Dekoratives Bild (wird vom Screenreader übersprungen) -->

	<img src="ornament.svg" alt="" />
	```
### ARIA-Attribute bei Bilden
**Zusätzlich erklärender Inhalt für Grafiken erstellen.** Mit ARIA-Attributen lassen sich Bilder um zusätzliche erklärende Inhalte ergänzen.
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
**Bilder flexibel an unterschiedliche Bildschirmgrößen anpassen.** Durch Techniken wie `picture` und `srcset` wird dem Browser die passende Bildvariante geliefert – optimiert für Smartphones, Tablets und Desktops.
```html
<picture>
  <source media="(min-width: 800px)" srcset="large.jpg">
  <img src="small.jpg" alt="Vereinsheim vor Bergkulisse">
</picture>
```

### (Komplexe) Grafiken
**Grafiken und Diagramme semantisch korrekt mit Beschriftung versehen.** Umfasse das Bild und seine Beschreibung mit `<figure>` und nutze `<figcaption>` für detaillierte Bildtexte.
```html
<figure>
  <img src="chart.png" alt="Mitgliederzahlen 2019 bis 2024" aria-describedby="desc-chart">
  <figcaption id="desc-chart">Balkendiagramm: Zunahme von 120 auf 250 Mitglieder innerhalb von fünf Jahren.</figcaption>
</figure>
```

### Bilder mit Text
**Wichtigen Text als Grafik vermeiden.** Screenreader und Vergrößerungsprogramme können Textgrafiken nicht erfassen. Nutze stattdessen HTML-Text oder CSS.

---

## Links
**Sinnvolle, aussagekräftige Linktexte verwenden**
Screenreader-Nutzer hören oft nur eine Liste von Links.

### Aussagekräftige Linktexte
- Vermeide generische Phrasen
	```html
	<!-- Falsch: -->
	<a href="/download">Hier klicken</a>

	<!-- Richtig: -->
	<a href="/download">Vereinsbroschüre als PDF herunterladen</a>
	```
- Zusammenhang verstehen. Linktexte sollten auch ohne umgebenden Kontext Sinn ergeben.

### Kontext und Redundanz
- Keine doppelten Linktexte auf einer Seite. Verwende unterschiedliche Texte, z. B. „Mehr erfahren zu Training“ und „Mehr erfahren zu Events“ statt zweimal „Mehr erfahren“.
- Linktext nicht abschneiden. Ohne den sichtbaren Kontext ist nicht klar, was genau passiert („Events anzeigen? erstellen? Infos?“).
```html
<!-- Falsch: -->
<a href="/events">Events …</a>

<!-- Richtig: -->
<a href="/events">Zu unseren Events</a>.
```
### Icon-only Links
Icons mit `aria-label` oder `.sr-only` beschreiben.
```html
<a href="/home" aria-label="Zur Startseite">
	<svg>...</svg>
</a>

<!-- oder -->

<a href="/home">
	<svg>...</svg>
	<span class="sr-only">Zur Startseite</span>
</a>
```
### Kein title für Accessibility
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

## Modale Dialoge und Popups
`aria-modal="true"` sperrt Hintergrund-Inhalte.
```html
<div role="dialog" aria-modal="true" aria-labelledby="dialog-title">
  <h2 id="dialog-title">…</h2>
  …
</div>
```

---

## Formulare
**Formulare so gestaltet, dass sie für Screenreader- und Tastaturnutzer:innen vollständig nutzbar sind.**
Barrierefreie Formulare verwenden eindeutige Labels, logische Fokus-Reihenfolge, klare Fehlermeldungen, Pflichtfeld-Kennzeichnungen und ggf. Hilfetexte oder Live-Regionen. So wird sichergestellt, dass alle Nutzer:innen Daten korrekt und selbstständig eingeben können.

- **Labels**
  Eindeutige `<label>`-Elemente für jedes Feld. Screenreader lesen Labels vor, Nutzer:innen verstehen sofort, wofür ein Feld gedacht ist.

- **Hilfetexte**
  Hinweise mit `aria-describedby` oder unterhalb der Felder. Zusätzliche Infos (z. B. „Mindestens 8 Zeichen“) werden vorgelesen und erleichtern die Eingabe.

- **Fehlermeldungen**
  Klar sichtbar, mit `role="alert"`. Fehler werden sofort erkennbar und auch von Screenreadern angesagt.

- **Pflichtfelder**
  Kennzeichnung mit `required` + visuelle Markierung. Hilft Nutzer:innen zu erkennen, welche Felder notwendig sind – Screenreader geben das ebenfalls aus.

- **Tastaturbedienung**
  Tab-Reihenfolge, logische Navigation. Alle Felder und Buttons müssen in logischer Reihenfolge mit <kbd>Tab</kbd> erreichbar sein.

- **Eindeutige IDs**
  Verknüpfung von `<label>` mit `for` und Feld-ID. Stellt sicher, dass Screenreader die richtige Verbindung zwischen Feld und Label herstellen.

- **Autocomplete**
  Attribute wie `autocomplete="email"` oder `tel`. Unterstützt Assistive Technologien und erleichtert Eingaben durch automatische Vorschläge.

- **Live-Regionen**
  Statusmeldungen mit `aria-live`. Z. B. „Formular erfolgreich gesendet“ wird automatisch angesagt, ohne dass der Fokus springt.

---

## Farbkontrast
**Ausreichender Unterschied zwischen Text und Hintergrund schaffen.**
Menschen mit eingeschränktem Sehvermögen oder Farbfehlsichtigkeit können Inhalte nur lesen, wenn der Kontrast hoch genug ist (z. B. WCAG AA: 4,5:1).

---

## Sehbeeinträchtigung
Inhalte für Nutzer mit eingeschränktem Sehvermögen (z. B. geringe Sehschärfe, Tunnelblick) zugänglich machen.
Barrierefreie Seiten nutzen klare Kontraste, flexible Schriftgrößen und gute Strukturen, um auch bei reduzierter Sehkraft bedienbar zu bleiben.

---

## Farbenblindheit
**Einschränkungen beim Unterscheiden von Farben (z. B. Rot-Grün-Schwäche).**
Informationen dürfen nicht nur durch Farbe vermittelt werden. Zusätzliche Symbole, Muster oder Texte verhindern, dass Inhalte verloren gehen.

---

## Legasthenie
*Schwierigkeiten beim Lesen und Verstehen von Texten.*
Gut lesbare Schriftarten, einfache Sprache, klare Gliederung und Vermeidung langer Textblöcke helfen, Inhalte zugänglicher zu machen.

---

## Transkript für Videos
**Textfassung des gesprochenen Inhalts und relevanter Geräusche erstellen.**
Transkripte machen audiovisuelle Inhalte für Gehörlose, Schwerhörige oder Personen mit eingeschränktem Zugriff auf Ton verständlich und durchsuchbar.

---

## Barrierefreie Dokumente
**Dokumente (PDF, Word, Präsentationen) mit zugänglicher Struktur versehen**
Damit auch außerhalb von Webseiten Inhalte von Screenreadern lesbar sind – z. B. durch richtige Überschriften-Hierarchie, Alt-Texte, Tags und Lese-Reihenfolge.

---

## Tests
Mit folgenden Möglichkeiten können Webseiten auf Barrierefreiheit überprüft werden.

### Screenreader-Test
Teste mit NVDA, VoiceOver oder JAWS.

### Keyboard-Navigation
Überprüfe, dass Links per <kbd>Tab</kbd> erreichbar und eindeutig fokussiert sind.

### Automatisierte Tools
aXe, WAVE oder Lighthouse auf fehlende Linktexte prüfen.
