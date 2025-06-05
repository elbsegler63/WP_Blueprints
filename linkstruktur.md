# Welche Struktur muss der Link haben, um eine eigene WordPress Playground JSON auszuführen?

<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" class="logo" width="120"/>

## Der Access-Control-Allow-Origin
Im Header muss der`Access-Control-Allow-Origin: *`lauten.

**Direkt auf GitHub (z.B. für die URL**
`https://github.com/elbsegler63/WP_Blueprints/blob/main/TT5%20Child/blueprint.json`
**kannst du den Header `Access-Control-Allow-Origin: *` nicht selbst setzen.** GitHub erlaubt keine eigenen Server-Konfigurationen wie `.htaccess` oder eigene Header für Dateien im Repository[^3].

### Was funktioniert bei GitHub?

- **GitHub API:**
Die GitHub REST-API unterstützt CORS und sendet standardmäßig den Header `Access-Control-Allow-Origin: *` zurück. Das gilt aber nur für API-Endpunkte wie `https://api.github.com`, nicht für Rohdateien oder Repository-URLs[^2][^5].
- **GitHub Pages:**
Bei GitHub Pages (also statischen Webseiten unter `username.github.io`) wird für öffentlich zugängliche Seiten CORS mit `Access-Control-Allow-Origin: *` gesetzt. Das gilt aber nur für GitHub Pages, nicht für die normale Repository-Ansicht oder Rohdateien[^3].


### Problem bei deiner URL

Die von dir genannte URL verweist auf eine Datei im Repository (nicht auf GitHub Pages und nicht auf die API):

```
https://github.com/elbsegler63/WP_Blueprints/blob/main/TT5%20Child/blueprint.json
```

- **Diese URL gibt HTML zurück (die GitHub-Oberfläche), nicht die Rohdaten.**
- **CORS-Header werden von GitHub hier nicht gesetzt und können auch nicht beeinflusst werden.**


### Lösungsmöglichkeiten

**1. Verwende den Raw-Link (raw.githubusercontent.com):**
Für den direkten Zugriff auf die Datei solltest du den Raw-Link verwenden, z.B.:

```
https://raw.githubusercontent.com/elbsegler63/WP_Blueprints/main/TT5%20Child/blueprint.json
```

- **GitHub setzt hier aber normalerweise keinen `Access-Control-Allow-Origin: *`-Header.**
Das bedeutet: Browser blockieren AJAX-Requests auf diese URL wegen fehlender CORS-Header.

**2. Datei auf GitHub Pages hosten:**
Wenn du die Datei auf GitHub Pages bereitstellst (z.B. im `docs`-Ordner oder im `gh-pages`-Branch), wird CORS mit `Access-Control-Allow-Origin: *` unterstützt[^3].

**3. Proxy verwenden:**
Du kannst einen eigenen Proxy-Server nutzen, der die Datei abruft und den gewünschten Header setzt.

### Fazit

- **Du kannst bei GitHub selbst keinen `Access-Control-Allow-Origin: *`-Header für Repository-Dateien setzen.**
- **Nur die GitHub API und GitHub Pages setzen diesen Header standardmäßig.**
- **Für statische Dateien in Repos (raw.githubusercontent.com) gibt es keinen CORS-Header.**

**Empfehlung:**
Lege die Datei in ein GitHub Pages-Verzeichnis und greife über die Pages-URL darauf zu, oder nutze einen eigenen Proxy, falls du CORS benötigst[^3][^5].

> GitHub Pages now supports CORS ... returns an Access-Control-Allow-Origin: * header. ... There's no way to support CORS on GitHub [raw files], though I'd love to see this feature.[^3]

<div style="text-align: center">⁂</div>

[^1]: blueprint.json

[^2]: https://docs.github.com/de/rest/using-the-rest-api/using-cors-and-jsonp-to-make-cross-origin-requests

[^3]: https://stackoverflow.com/questions/26416727/cross-origin-resource-sharing-on-github-pages

[^4]: https://github.com/OpenLiberty/guide-cors

[^5]: https://docs.github.com/en/rest/using-the-rest-api/using-cors-and-jsonp-to-make-cross-origin-requests

[^6]: https://github.com/orgs/community/discussions/12209

[^7]: https://github.com/homematic-community/XML-API/issues/72

[^8]: https://github.com/AUTOMATIC1111/stable-diffusion-webui/discussions/13776

[^9]: https://learn.microsoft.com/de-de/aspnet/core/security/cors?view=aspnetcore-9.0

[^10]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Access-Control-Allow-Origin

[^11]: https://github.com/requarks/wiki/discussions/3056


https://playground.wordpress.net/?blueprint-url=https://github.com/elbsegler63/WP_Blueprints/main/TT5%20Child/blueprint.json
