La _Same-Origin Policy (SOP)_ és una mesura de seguretat implementada pels navegadors per protegir els usuaris d’atacs maliciosos i filtracions de dades. Aquesta política restringeix l’accés d’un lloc web a la informació d’un altre domini, tret que ambdós comparteixin el mateix origen. D’aquesta manera, s’eviten accions no autoritzades com el robatori de dades o l’execució de codi maliciós.

🔍 **En resum**: Un lloc web només pot interactuar amb recursos que provinguin del mateix origen, llevat que hi hagi una configuració especial per permetre-ho.

---
## 🌍 Definició d'Origen

L'origen d'una pàgina web es determina per tres elements fonamentals:

- **Protocol** → (http, https, ftp...)
- **Domini** → (exemple.com, google.com...)
- **Port** → (80, 443, 8080...)

🔹 Si qualsevol d'aquests elements és diferent entre dues URLs, es considera que tenen **orígens diferents** i, per tant, estan subjectes a les restriccions de SOP.

### 📋 Exemples de comparació d'origen

|🌐 URL d’origen → Destí|Mateix Origen?|🔎 Motiu|
|---|---|---|
|`http://store.company.com/dir/page.html` → `http://store.company.com/dir2/other.html`|✅|Només canvia la ruta (mateix protocol, domini i port).|
|`http://store.company.com/dir/page.html` → `https://store.company.com/page.html`|❌|El protocol és diferent (`http` vs `https`).|
|`http://company.com/dir/page.html` → `http://news.company.com/dir/page.html`|❌|Els dominis són diferents (`company.com` vs `news.company.com`).|
|`http://store.company.com:80/dir/page.html` → `http://store.company.com:81/dir/page.html`|❌|Els ports són diferents (`80` vs `81`).|

## 📊 Resum de la SOP

|🔹 Característica|ℹ️ Descripció|
|---|---|
|🖥️ **Qui la imposa?**|Els navegadors.|
|🔐 **Què protegeix?**|Evita que llocs web accedeixin a dades sensibles d'altres dominis sense permís.|
|🚫 **Què bloqueja?**|Peticions AJAX, accés a cookies i altres dades entre diferents orígens.|
|🔄 **Com permetre l’accés?**|Mitjançant mecanismes com **CORS**, **postMessage**, o si el servidor destí ho permet.|

---

🔒 **La SOP és una barrera fonamental per a la seguretat web**, ajudant a prevenir atacs com el _Cross-Site Scripting (XSS)_ o el _Cross-Site Request Forgery (CSRF)_. Per això, és clau entendre-la i saber com gestionar-la correctament. 🚀✨