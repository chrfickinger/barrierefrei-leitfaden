# Seiteaufbau

## 1. Grundgerüst und Landmarken

- **Skip-Link**
  ```html
  <a href="#main" class="skip-link">Zum Hauptinhalt springen</a>
  ```
  *Erklärung:* Erlaubt Tastaturnutzer:innen, direkt zum `<main>` zu springen.

- **`<header>`**
  ```html
  <header role="banner">…</header>
  ```
  *Erklärung:* Oberster Bereich, enthält Logo, Hauptnavigation, Überschrift.

- **`<nav>`**
  ```html
  <nav role="navigation" aria-label="Hauptnavigation">…</nav>
  ```
  *Erklärung:* Markiert Navigationsbereiche, `aria-label` differenziert mehrere Navs.

- **`<main>`**
  ```html
  <main id="main" role="main">…</main>
  ```
  *Erklärung:* Hauptinhalt der Seite; nur einmal pro Seite verwenden.

- **`<aside>`**
  ```html
  <aside role="complementary" aria-label="Seitenleiste">…</aside>
  ```
  *Erklärung:* Sekundäre Inhalte wie Widgets, Links, Werbung.

- **`<footer>`**
  ```html
  <footer role="contentinfo">…</footer>
  ```
  *Erklärung:* Fußbereich mit Copyright, Impressum.

---

## 2. Überschriftenstruktur

- Überschriften-Reihenfolge: `<h1>` bis `<h6>`
  - Jede Seite nur eine `<h1>`
  - Logische Gliederung: keine Sprünge von `<h2>` zu `<h4>`.

---

## 3. ARIA-Regionen & Labels

- **`aria-label`**
  Beschriftet Landmarken oder interaktive Regionen:
  ```html
  <nav aria-label="Footer-Navigation">…</nav>
  ```

- **`aria-labelledby`**
  Verweist auf vorhandene Überschrift:
  ```html
  <section aria-labelledby="sec-hero-title">
    <h2 id="sec-hero-title">Unsere Mission</h2>
    …
  </section>
  ```

- **`role="region"`**
  Für benannte Bereiche:
  ```html
  <div role="region" aria-label="Aktuelles">…</div>
  ```

---

## 4. Zugängliche Formulare (Kurzüberblick)

- `<form role="form">` nicht nötig (Formular hat schon Bedeutung), stattdessen:
  - `<fieldset>` + `<legend>` für Gruppen
  - `<label for="id">…</label>` nie weglassen
  - `aria-required="true"` für Pflichtfelder

---

## 5. Modale Dialoge und Popups

- **Modal**
  ```html
  <div role="dialog" aria-modal="true" aria-labelledby="dialog-title">
    <h2 id="dialog-title">…</h2>
    …
  </div>
  ```
  *Erklärung:* `aria-modal="true"` sperrt Hintergrund-Inhalte.

---


# Bilder

## 1. Alt-Text („alt"-Attribut)

- **Immer setzen**
  - Jedes `<img>` muss ein `alt`-Attribut haben, auch wenn es leer ist.
- **Inhalt beschreiben**
  - Alt-Text soll den Informationsgehalt knapp und präzise wiedergeben.
  ```html
  <!-- informatives Bild -->
  <img src="tour.jpg" alt="Radfahrer auf Waldweg bei Sonnenaufgang">
  ```
- **Leerer Alt-Text für Dekoration**
  - Für rein dekorative Bilder: `alt=""`
  ```html
  <img src="ornament.svg" alt="">  <!-- Screenreader überspringen -->
  ```

---

## 2. Semantik: `<figure>` & `<figcaption>`

- **Komplexe Grafiken**
  - Umfasse das Bild und seine Beschreibung mit `<figure>`.
- **Beschriftung**
  - Nutze `<figcaption>` für detaillierte Bildtexte.
  ```html
  <figure>
    <img src="chart.png"
         alt="Mitgliederzahlen 2019 bis 2024"
         aria-describedby="desc-chart">
    <figcaption id="desc-chart">
      Balkendiagramm: Zunahme von 120 auf 250 Mitglieder innerhalb von fünf Jahren.
    </figcaption>
  </figure>
  ```

---

## 3. Responsive Bilder: `<picture>` & `srcset`

- **Mehrere Auflösungen anbieten**
  ```html
  <picture>
    <source media="(min-width: 800px)" srcset="large.jpg">
    <img src="small.jpg" alt="Vereinsheim vor Bergkulisse">
  </picture>
  ```
- **Alt-Text behalten**
  - Alle `<img>`-Instanzen benötigen dasselbe aussagekräftige `alt`.

---

## 4. ARIA-Ergänzungen

- **`aria-describedby`**
  - Verknüpft das Bild mit einer ausführlichen Beschreibung:
  ```html
  <img src="map.png"
       alt="Stadtplan von St. Ingbert"
       aria-describedby="map-desc">
  <p id="map-desc">Die Karte zeigt Hauptstraßen, Radwege und Parkplätze rund um das Vereinsgelände.</p>
  ```
- **`role="presentation"`**
  - Bei komplexen SVGs ohne Informationswert:
  ```html
  <img src="icon.svg" alt="" role="presentation">
  ```
- **`aria-hidden="true"`**
  - Für dekorative Icons in `<span>`-Elementen:
  ```html
  <span class="icon-dekor" aria-hidden="true"></span>
  ```

---

## 5. Kein Bildtext allein

- **Vermeide wichtigen Text als Grafik**
  - Screenreader und Vergrößerungsprogramme können Textgrafiken nicht erfassen.
  - Nutze stattdessen echten HTML-Text oder CSS.

---

# Linktexte

## 1. Aussagekräftiger Linktext

- **Vermeide generische Phrasen**
  - **Schlecht:** `<a href="/download">Hier klicken</a>`
  - **Gut:** `<a href="/download">Vereinsbroschüre als PDF herunterladen</a>`

- **Zusammenhang verstehen**
  - Linktexte sollten auch ohne umgebenden Kontext Sinn ergeben.

---

## 2. Kontext und Redundanz

- **Keine doppelten Linktexte auf einer Seite**
  - Verwende unterschiedliche Texte, z. B. „Mehr erfahren zu Training“ und „Mehr erfahren zu Events“ statt zweimal „Mehr erfahren“.

- **Vermeidung von Ellipsen**
  - Statt `<a href="/events">Events …</a>` lieber `<a href="/events">Zu unseren Events</a>`.

---

## 3. Icon-only Links

- **Icon mit `aria-label` oder `.sr-only`**
  ```html
  <a href="/home" aria-label="Zur Startseite">
    <svg><!-- ... --></svg>
  </a>
  ```
  oder
  ```html
  <a href="/home">
    <svg><!-- ... --></svg>
    <span class="sr-only">Zur Startseite</span>
  </a>
  ```

---

## 4. Kein `title` für Accessibility

- **`title`-Attribute sind kein Ersatz**
  - Screenreader lesen `title` oft nicht vor. Nutze stattdessen klaren Linktext oder `aria-label`.

---

## 5. Verwendung von `.sr-only`

- **Zusätzliche Informationen nur für Screenreader**
  ```html
  <a href="/terms">
    Nutzungsbedingungen
    <span class="sr-only"> (öffnet Seite mit rechtlichen Hinweisen)</span>
  </a>
  ```

---

## 6. ARIA-Ergänzungen (wenn nötig)

- **`aria-label`**
  - Nur bei rein ikonischen Links ohne sichtbaren Text.

- **`aria-describedby`**
  - Für längere Hinweise außerhalb des Linktextes.

---

# Prüfung & Testing

- **Screenreader-Test**
  - Teste mit NVDA, VoiceOver oder JAWS.

- **Keyboard-Navigation**
  - Überprüfe, dass Links per Tab erreichbar und eindeutig fokussiert sind.

- **Automatisierte Tools**
  - aXe, WAVE oder Lighthouse auf fehlende Linktexte prüfen.

---

Mit diesem Leitfaden stellst du sicher, dass deine Links klar, verständlich und für alle Nutzer:innen zugänglich sind.
