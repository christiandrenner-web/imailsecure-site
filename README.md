# imailsecure-site

Website für **iMail Secure** — statisches HTML, keine Build-Kette, keine
externen Ressourcen (keine Fonts, keine Skripte, keine Analytics). Das ist
Absicht: Die Seite soll dieselbe Haltung zeigen wie die App.

```
index.html      Startseite
privacy.html    Datenschutzerklärung + Impressum
terms.html      Nutzungsbedingungen (AGB) + Abo-Bedingungen
support.html    Hilfe und Kontakt
style.css       gemeinsames Stylesheet (lokal, kein CDN)
.nojekyll       GitHub Pages: kein Jekyll-Processing
```

## ⚠️ Vor dem Veröffentlichen: Platzhalter ersetzen

Die Seiten enthalten sichtbar markierte Platzhalter
(`<span class="placeholder">[…]</span>`). Alle müssen ersetzt werden, sonst
ist die Seite weder App-Store-tauglich noch rechtlich in Ordnung.

```bash
grep -rn "placeholder" *.html
```

Zu ersetzen:

| Platzhalter | Wofür | Status |
|---|---|---|
| `[Vor- und Nachname]` | Betreiber, Impressum (§ 5 DDG), Verantwortlicher nach DSGVO | ✅ Christian Renner |
| `[Straße und Hausnummer]` | Anschrift (eine ladungsfähige Anschrift ist Pflicht) | ✅ Steigerstr. 101b |
| `[PLZ und Ort]` | Anschrift | ✅ 06493 Harzgerode |
| `[TT. Monat JJJJ]` | Stand der Datenschutzerklärung | ✅ 11. November 2026 |
| `chr.renner@mein.gmx` | Kontaktadresse in Datenschutz, Impressum und Support | ✅ eingetragen |

Die Kontaktadresse muss ein **funktionierendes Postfach** sein. Apple prüft
Support- und Datenschutz-URL vor der Freigabe, und das Impressum verlangt eine
schnelle elektronische Kontaktaufnahme. Eine Adresse wie
`imailsecure.app@…` bei einem Freemailer reicht dafür aus.

## Veröffentlicht über GitHub Pages

Die Website liegt in einem eigenen, öffentlichen Repo; der App-Quellcode
bleibt davon unberührt. Stand 12. November 2026 ist sie live.

- Repo: <https://github.com/christiandrenner-web/imailsecure-site>
- Pages: *Deploy from a branch*, Branch `main`, Ordner `/ (root)`, HTTPS erzwungen
- Änderungen: committen und nach `main` pushen — Pages baut automatisch.

Die Seite ist erreichbar unter:

```
https://christiandrenner-web.github.io/imailsecure-site/
https://christiandrenner-web.github.io/imailsecure-site/privacy.html
https://christiandrenner-web.github.io/imailsecure-site/terms.html
https://christiandrenner-web.github.io/imailsecure-site/support.html
```

Diese URLs sind bereits in der App eingetragen —
`Sources/iMailSecure/Utilities/Constants.swift`:

```swift
static let privacyPolicyURL = "https://christiandrenner-web.github.io/imailsecure-site/privacy.html"
static let termsOfUseURL    = "https://christiandrenner-web.github.io/imailsecure-site/terms.html"
```

## `terms.html` ist ein Entwurf

Die Nutzungsbedingungen sind inhaltlich vollständig, aber **nicht anwaltlich
geprüft**. Auf der Seite stehen deshalb ein `Entwurf`-Badge und ein
Hinweiskasten. Nach der Prüfung:

1. Badge (`<span class="badge">Entwurf</span>`) und den Hinweiskasten entfernen,
2. Stand-Datum anpassen,
3. Preisangaben mit App Store Connect abgleichen (1,99 €/Monat, 17,99 €/Jahr).

Der Entwurf deckt ab: Geltungsbereich, Free/Pro, 7-Tage-Testphase über Apples
Introductory Offer, Preise, automatische Verlängerung, Kündigung über die
Apple-ID, Widerrufsrecht bei digitalen Inhalten (§ 356 Abs. 5 BGB), Lizenz des
Quellcodes (PolyForm Noncommercial, ausdrücklich kein Open Source), Pflichten,
Verfügbarkeit, Haftungsbegrenzung, Änderungsklausel und Streitbeilegung.

## Eigene Domain (optional, später)

Eine eigene Domain ist für den App Store nicht nötig. Wenn sie kommt:
`imailsecure.de` ist derzeit frei und kostet etwa 10 €/Jahr (`.io` kostet
deutlich mehr und bringt keinen inhaltlichen Vorteil).

Bei eigener Domain: Datei `CNAME` mit der Domain anlegen, beim DNS-Anbieter
die GitHub-Pages-Records setzen, danach **HTTPS erzwingen** (Settings → Pages).
Erst wenn HTTPS aktiv ist, ist die URL für die App-Store-Einreichung geeignet.

## Prüfen

```bash
# keine externen Ressourcen (muss leer bleiben; <a href="https://…"> ist erlaubt)
grep -nE '(<link[^>]+href|src)="https?://' *.html

# Platzhalter (muss leer bleiben)
grep -n "placeholder" *.html

# lokal ansehen
python3 -m http.server 8080
```

## Lizenz

Die Texte dieser Website stehen unter CC BY 4.0 — außer Logo und Name
„iMail Secure", die nicht als eigene Marke verwendet werden dürfen.

Die **App** steht unter der PolyForm Noncommercial 1.0.0 (Quellcode einsehbar,
keine kommerzielle Nutzung durch Dritte). Das ist kein Open Source; die
Bezeichnung darf auch auf dieser Website nicht verwendet werden. Details im
App-Repo unter `LICENSING.md`.
