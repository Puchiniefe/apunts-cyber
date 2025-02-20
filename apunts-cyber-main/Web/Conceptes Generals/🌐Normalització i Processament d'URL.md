
La normalització d’URL consisteix a transformar una URL en un format estàndard per facilitar la comparació, l'emmagatzematge i la seguretat.

---

## 🔍 **Passos per normalitzar una URL**

### 1️⃣ **Convertir a minúscules**  
El **protocol** i el **host** són insensibles a majúscules i minúscules, però el **path** pot ser sensible.  

✅ **Exemple:**  HTTPS://ExEmPlE.CoM/Home → https://example.com/Home


---

### 2️⃣ **Afegir o eliminar el `www.` segons convingui**  
Depenent de la política del sistema, es pot mantenir o eliminar `www.` per coherència.  

✅ **Exemple:**  [www.example.com](http://www.example.com) → example.com (o viceversa)


---

### 3️⃣ **Eliminar el port si és el predeterminat**  
- `80` per HTTP  
- `443` per HTTPS  

✅ **Exemple:**  https://example.com:443/home → https://example.com/home

---

### 4️⃣ **Eliminar barres `/` innecessàries**  
Les URL no han d’acabar amb `/` si no és necessari.  

✅ **Exemple:**  https://example.com/home/ → https://example.com/home

---

### 5️⃣ **Codificar i descodificar caràcters**  
Les URL han de contenir només caràcters segurs (`A-Z`, `a-z`, `0-9`, `-`, `_`, `.`, `~`) i codificar els caràcters especials.  

✅ **Exemple:**  https://example.com/café → https://example.com/caf%C3%A9

---

### 6️⃣ **Ordenar els paràmetres de la query**  
Per assegurar que dues URL amb els mateixos paràmetres es considerin iguals, s'han d’ordenar alfabèticament.  

✅ **Exemple:**  https://example.com/page?z=3&b=2&a=1 → https://example.com/page?a=1&b=2&z=3

---

### 7️⃣ **Eliminar fragments (`#`)**  
Els fragments (`#section`) només són útils per a la navegació dins la pàgina i **no afecten la sol·licitud al servidor**, per tant, sovint es poden eliminar.  

✅ **Exemple:**  https://example.com/page#section → https://example.com/page


---

### 8️⃣ **Eliminar valors per defecte en els paràmetres**  
Si un paràmetre té un valor per defecte en el servidor, es pot ometre.  

✅ **Exemple:**  https://example.com/page?lang=en → https://example.com/page (si 'en' és el valor per defecte)


---

## 🔥 **Resum Final**  

✅ Convertir **protocol i domini** a minúscules.  
✅ Eliminar **ports predeterminats**.  
✅ Normalitzar **barra final `/`**.  
✅ Codificar correctament **caràcters especials**.  
✅ Ordenar **paràmetres** i eliminar-ne els innecessaris.  
✅ Eliminar **fragments `#`** i valors per defecte.  

Aquest procés assegura que diferents representacions d’una mateixa URL siguin consistents! 🚀

