
Les **cookies** són fragments d'informació que els servidors envien als navegadors per ser guardats i enviats en futures sol·licituds. S'utilitzen per gestionar sessions i guardar preferències de l'usuari, com per exemple el color de la web. Els navegadors permeten controlar el comportament de les cookies mitjançant els següents atributs:

---

## 🏷️ 1. **Name (Nom)** 
### Descripció:  
És el **nom únic** de la cookie, que serveix per identificar-la. El nom és essencial perquè el servidor pugui identificar la cookie i gestionar la sessió de l'usuari.

### Exemple:  
`sessionid`, `php_session`...

### Normes:  
- El nom ha de ser **únic** per cada domini.  
- No poden haver dues cookies amb el mateix nom per al mateix domini.

---

## 💡2. **Value (Valor)** 
### Descripció:  
És el **valor associat al nom de la cookie**. Es guarda al navegador i s'envia en cada sol·licitud HTTP per identificar la sessió o preferències d'un usuari.

### Normes:  
- Pot ser qualsevol **cadena de text**, excepte el punt i coma (`;`) i l'espai en blanc (` `).

---

## 🌍3. **Domain (Dominio)** 
### Descripció:  
Especifica el **domini i el subdomini** al qual pertany la cookie. Indica quines webs poden accedir a la cookie.

### Exemple:  
`.exemple.com`, accessible des de `www.exemple.com`, `vpn.exemple.com`, etc.

### Normes:  
- Si no es defineix el domini, es pren per defecte el domini del servidor.

---

## 🛤️4. **Path (Ruta)** 
### Descripció:  
Defineix **quins directoris de la web** poden enviar la cookie. La cookie no s'enviarà a altres directoris fora del **path** definit.

### Normes:  
- Si no es defineix un **path**, s'assignarà el **path** actual de la URL.

---

## 📅5. **Expires (Caducitat)** 
### Descripció:  
Defineix la **data i hora** en què la cookie caducarà. Si no s'especifica, la cookie serà de sessió, és a dir, s'eliminarà al tancar el navegador.

### Format:  
La data ha de ser especificada en format **GMT**.

### Normes:  
- Si no es defineix una data d'expiració, la cookie serà **temporal** i es destruirà al tancar el navegador.

---

## ⏳6. **Max-Age (Màxima Vida)** 
### Descripció:  
Similar a **Expires**, però defineix el temps (en **segons**) durant el qual la cookie serà vàlida. Aquest temps es calcula a partir de la creació de la cookie.

### Exemple:  
`Max-Age=3600` (La cookie caducarà en **1 hora**).

### Normes:  
- **Max-Age** té **prioritat sobre Expires**. Si es defineixen ambdós, s'utilitzarà **Max-Age**.

---

## 🔐7. **Secure (Seguretat)** 
### Descripció:  
L'atribut **`Secure`** indica que la cookie només es transmetrà a través de **connexions HTTPS segures**. Això protegeix les cookies de ser interceptades en connexions HTTP no segures, com en atacs **MITM (Man In The Middle)**.

### Normes:  
- Si la pàgina utilitza **HTTP** i una cookie té l'atribut **`Secure`**, aquesta **no serà enviada**.  
- Ha de ser utilitzat exclusivament amb connexions **HTTPS**.

---

## 🚫💻8. **HttpOnly** 
### Descripció:  
L'atribut **`HttpOnly`** fa que la cookie només sigui accessible pel servidor web, **no per JavaScript**. Això ajuda a prevenir atacs de **XSS (Cross-Site Scripting)**.

### Normes:  
- **Impossible accedir des de JavaScript**: Les cookies amb aquest atribut no poden ser llegides per JavaScript, ajudant a prevenir que scripts maliciosos obtinguin les cookies.

- **Protegeix cookies sensibles**: Especialment útil per a cookies de **sessió** o **autenticació**.

---

## 🔒9. **SameSite** 
### Descripció:  
L'atribut **`SameSite`** controla com s'envien les cookies en sol·licituds que provenen de **diferents llocs** (cross-site). Aquest atribut s'utilitza principalment per protegir contra atacs de **CSRF (Cross-Site Request Forgery)**.

**SameSite** ajuda a prevenir aquests atacs al no enviar les cookies quan la petició prové d'un altre domini.

### Tipus:
1. **SameSite=Strict**: Les cookies **només s'enviaran** si la petició prové del mateix domini.
   
2. **SameSite=Lax**: Les cookies es poden enviar en algunes sol·licituds creuades (per exemple, en un enllaç, però no en formularis).

3. **SameSite=None**: Equival a no tenir **`SameSite`** configurat. Les cookies s'envien en sol·licituds creuades, **però només si també es defineix `Secure`** per garantir que es transmetin a través de connexions segures (HTTPS).

---
