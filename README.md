# imailsecure-site

Website für **iMail Secure** — statisches HTML, keine Build-Kette, keine
externen Ressourcen (keine Fonts, keine Skripte, keine Analytics). Das ist
Absicht: Die Seite soll dieselbe Haltung zeigen wie die App.

```
index.html      Startseite
privacy.html    Datenschutzerklärung + Impressum
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

| Platzhalter | Wofür |
|---|---|
| `[Vor- und Nachname]` | Betreiber, Impressum (§ 5 DDG), Verantwortlicher nach DSGVO |
| `[Straße und Hausnummer]` | Anschrift (eine ladungsfähige Anschrift ist Pflicht) |
| `[PLZ und Ort]` | Anschrift |
| `[kontakt@deine-domain.example]` | Kontaktadresse in Datenschutz, Impressum und Support |
| `[TT. Monat JJJJ]` | Stand der Datenschutzerklärung |

Die Kontaktadresse muss ein **funktionierendes Postfach** sein. Apple prüft
Support- und Datenschutz-URL vor der Freigabe.

## Veröffentlichen über GitHub Pages

GitHub Pages ist bei GitHub Free nur für **öffentliche** Repositories
kostenlos. Deshalb liegt die Website in einem eigenen, kleinen Repo — der
App-Quellcode bleibt davon unberührt.

1. Auf GitHub ein **öffentliches** Repository `imailsecure-site` anlegen
   (ohne README, ohne .gitignore).
2. Dieses Verzeichnis pushen:

   ```bash
   cd ~/XCODE/imailsecure-site
   git remote add origin git@github.com:christiandrenner-web/imailsecure-site.git
   git branch -M main
   git push -u origin main
   ```

3. Im Repo: **Settings → Pages**
   - Source: *Deploy from a branch*
   - Branch: `main`, Ordner: `/ (root)`
   - Save

4. Nach ein bis zwei Minuten ist die Seite erreichbar unter:

   ```
   https://christiandrenner-web.github.io/imailsecure-site/
   https://christiandrenner-web.github.io/imailsecure-site/privacy.html
   https://christiandrenner-web.github.io/imailsecure-site/support.html
   ```

5. Diese URLs sind bereits in der App eingetragen —
   `Sources/iMailSecure/Utilities/Constants.swift`:

   ```swift
   static let privacyPolicyURL = "https://christiandrenner-web.github.io/imailsecure-site/privacy.html"
   ```

## Eigene Domain (optional, später)

Eine eigene Domain ist für den App Store nicht nötig. Wenn sie kommt:
`imailsecure.de` ist derzeit frei und kostet etwa 10 €/Jahr (`.io` kostet
deutlich mehr und bringt keinen inhaltlichen Vorteil).

Bei eigener Domain: Datei `CNAME` mit der Domain anlegen, beim DNS-Anbieter
die GitHub-Pages-Records setzen, danach **HTTPS erzwingen** (Settings → Pages).
Erst wenn HTTPS aktiv ist, ist die URL für die App-Store-Einreichung geeignet.

## Prüfen

```bash
# keine externen Ressourcen (muss leer bleiben)
grep -nE '(src|href)="https?://' *.html

# Platzhalter (muss leer bleiben)
grep -n "placeholder" *.html

# lokal ansehen
python3 -m http.server 8080
```

## Lizenz

Die Texte dieser Website stehen unter CC BY 4.0 — außer Logo und Name
„iMail Secure", die nicht als eigene Marke verwendet werden dürfen.
