# 🤔 Què és un atac CSRF?

Un **CSRF (Cross-Site Request Forgery)** és un tipus d'atac en què s'aprofita que el navegador guarda les **cookies associades a un domini** i aquestes **s'envien automàticament** al domini corresponent. El domini es pensa que és **una sol·licitud legítima** i permet realitzar accions no desitjades, com si fossis l'usuari autenticat.

---

## ⚙️ Com funciona un atac CSRF?

El funcionament d'un atac CSRF es basa en l'enviament automàtic de cookies associades amb el domini del lloc web. Així és com es produeix un atac CSRF pas a pas:

1. **🖥️ L'usuari està autenticat en un lloc web**:
   - Suposem que l'usuari està **autenticat en google.com**. El seu navegador ha guardat les cookies associades a **google.com**, com per exemple una cookie de sessió (`sessionid=abc123`), que manté l'usuari connectat.

2. **👨‍💻 L'atacant crea una pàgina maliciosa**:
   - L'atacant crea una pàgina web maliciosa en el seu domini (**attacker.com**) que conté un **enllaç maliciós o formulari ocult** que realitza una sol·licitud HTTP al servidor de **google.com**.

3. **🧐 L'usuari visita la pàgina maliciosa**:
   - L'usuari, sense saber-ho, visita la pàgina de **attacker.com**. Això fa que el navegador de l'usuari carregui la pàgina maliciosa i es faci una **sol·licitud a google.com**.

4. **🔑 El navegador envia les cookies automàticament**:
   - Quan el navegador fa aquesta sol·licitud, **envia automàticament les cookies associades a google.com** amb la sol·licitud, ja que està autenticada en aquest lloc web. Això passa sense que l'usuari ho sàpiga.

5. **🔄 El servidor de google.com processa la sol·licitud**:
   - El servidor de **google.com** rep la sol·licitud, veu les cookies de sessió vàlides (com `sessionid=abc123`), i **processa la sol·licitud** com si fos una acció legítima realitzada per l'usuari autenticat. Això podria ser una acció no desitjada, com transferir diners al compte de l'atacant.

---

## 🔐 Què fa vulnerable un sistema a CSRF?

Els atacs CSRF són possibles perquè molts llocs web **no validen adequadament d'on provenen les sol·licituds**. Quan un lloc web només s'ha de confiar en la **cookie de sessió** per autenticar l'usuari i no utilitza altres mecanismes de seguretat, qualsevol sol·licitud HTTP legítima des del navegador de l'usuari es considerarà autèntica, incloent les malicioses.

---

## 🛡️ Protecció contra CSRF

6. **🔑 Tokens CSRF**:
   - Una de les mesures més comunes per evitar aquest tipus d'atac és l'ús de **tokens CSRF**. Els **tokens CSRF** són cadenes úniques que es generen i s'inclouen en les sol·licituds que es realitzen a un servidor web. Quan l'usuari envia una sol·licitud, el servidor verifica que el **token CSRF** que es rep coincideixi amb el token generat per la sessió de l'usuari. Si no coincideixen, la sol·licitud es rebutja.
   - Això assegura que la sol·licitud prové d'un formulari legítim en la pàgina del servidor i no d'un atacant.

7. **🍪 Cookies `SameSite`**:
   - El navegador pot aplicar l'atribut **`SameSite`** en les cookies, el qual ajuda a evitar que les cookies es facin servir en sol·licituds entre llocs (cross-site). Això significa que les cookies només s'enviaran en sol·licituds que provinguin del mateix lloc web que les ha establert.
   - **`SameSite=Strict`**: La cookie només es pot enviar en sol·licituds que provinguin del mateix domini. Si un atacant intenta forçar una sol·licitud maliciosa des de **attacker.com**, la cookie de **google.com** no es enviarà.
   - **`SameSite=Lax`**: Permet que les cookies es transmetin en sol·licituds de llocs creuats en certes condicions (per exemple, quan es fa clic en un enllaç).

8. **🔍 Verificació del referer i origin**:
   - Alguns llocs web també validen els encapçalaments **Referer** i **Origin** per assegurar-se que la sol·licitud prové d'un lloc de confiança.

9. **🛠️ Accions sensibles amb mètodes HTTP segurs**:
   - Algunes aplicacions opten per utilitzar **mètodes HTTP més segurs** per a sol·licituds sensibles (com **POST** en comptes de **GET**). Això ajuda a evitar que l'usuari realitzi accions importants amb només un enllaç.

---

## 🔚 Conclusió:
En l'atac **CSRF**, no s'accedeix a les cookies directament, sinó que s'aprofita que el navegador **envia les cookies automàticament** amb les sol·licituds HTTP. Així, l'atacant pot fer que la víctima enviï una sol·licitud maliciosa utilitzant les cookies vàlides, creant la sensació que la sol·licitud és legítima.

---

