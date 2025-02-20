## 🔍 **Què és CORS?**

**CORS (Cross-Origin Resource Sharing)** és un mecanisme que permet als navegadors concedir permisos perquè un lloc web pugui accedir a recursos d'un altre origen diferent. És una excepció a la **Same-Origin Policy (SOP)**, que per defecte restringeix aquest tipus d'accés per seguretat.

---
## 🌍 **Quan és necessari CORS?**

CORS és necessari quan un lloc web vol fer peticions **AJAX/Fetch** a un servidor d’un altre domini. Exemples:

- Una aplicació **React** (`http://localhost:3000`) fent una petició a una API en `https://api.exemple.com`.
- Un script JavaScript en un lloc `https://web1.com` intentant accedir a recursos de `https://web2.com`.

---
## ⚡ **Com funciona?**

Quan una web intenta fer una petició a un origen diferent, el navegador envia una petició prèvia (**preflight request**) amb el mètode **OPTIONS** per demanar permís.

- Si el servidor destí permet la petició, respon amb els **CORS Headers** necessaris.
- Si no, el navegador bloqueja la petició per seguretat.

---
## 📚 **Headers CORS importants**

|🔹 Header|📀 Funció|
|---|---|
|`Access-Control-Allow-Origin`|Especifica quins dominis poden accedir als recursos. Ex.: `*` (tots) o `https://exemple.com`.|
|`Access-Control-Allow-Methods`|Indica els mètodes HTTP permesos (`GET`, `POST`, `PUT`, `DELETE`...).|
|`Access-Control-Allow-Headers`|Defineix quins headers personalitzats es poden enviar a la petició.|
|`Access-Control-Allow-Credentials`|Permet enviar **cookies i autenticació** (`true` o `false`).|

---

##  🚨**Perills d'usar Access-Control-Allow-Origin: **

Si el servidor respon amb:

```http
Access-Control-Allow-Origin: *  
```

- **Es desactiven les restriccions de la SOP** i qualsevol lloc web pot fer peticions al teu servidor.
- Si les respostes contenen **informació sensible**, podrien ser accessibles per atacs _cross-site_.
- **No es poden enviar cookies o credencials**, ja que `Access-Control-Allow-Credentials: true` no funciona amb `*`.

👉 **Alternativa més segura:** Restringir a dominis de confiança.

```http
Access-Control-Allow-Origin: https://exemple.com  
```

## 🚀 **Resum Final**

✅ **CORS permet compartir recursos entre diferents orígens**.  
✅ **Els navegadors bloquegen peticions cross-origin per seguretat** (SOP).  
✅ **El servidor ha d’enviar els headers CORS correctes perquè funcioni**.  
✅ **Preflight Request** es fa en peticions complexes per confirmar permisos.

🔒 **Controlar correctament CORS és clau per evitar problemes de seguretat!** 🚀