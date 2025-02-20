
## 🔍 **Què és URL Encoding & Decoding?**

L'**URL Encoding** i **Decoding** són processos per convertir caràcters especials en una URL per garantir que es transmetin correctament sense errors.

Quan una URL conté espais, accents o símbols especials (`á, é, ñ, #, /`), aquests s’han de substituir per una representació segura per evitar problemes de lectura.

---

## 🌍 **Per què cal codificar (encode) i descodificar (decode) les URL?**

🔹 **Raons principals:**

1. **Evitar errors en la transmissió** → Alguns caràcters tenen significats especials en les URL (`?`, `&`, `=`). Si no es codifiquen, podrien alterar la interpretació de la URL.
2. **Permetre l’ús de caràcters especials** → Algunes lletres com `á`, `ñ`, `ç` o espais no estan permesos directament en les URL.
3. **Millorar la compatibilitat entre navegadors i servidors** → El format estàndard evita errors en diferents sistemes.

📌 **Exemple pràctic:**

```
Text original:  café con azúcar
URL encoded:    caf%C3%A9%20con%20az%C3%BAcar
```

- La `é` es converteix en `%C3%A9`
- L'espai es converteix en `%20`
- La `ú` es converteix en `%C3%BA`

---

## 📚 **Com es fa l’URL Encoding?**

L’URL Encoding substitueix caràcters especials pel seu codi hexadecimal prefixat per `%`.

### 🔹 **Caràcters més comuns en URL encoding**

|Caràcter|Codificat (URL encoded)|
|---|---|
|Espai ( )|`%20` o `+`|
|`!`|`%21`|
|`#`|`%23`|
|`$`|`%24`|
|`&`|`%26`|
|`/`|`%2F`|
|`=`|`%3D`|
|`?`|`%3F`|
|`á`|`%C3%A1`|
|`é`|`%C3%A9`|
|`í`|`%C3%AD`|
|`ó`|`%C3%B3`|
|`ú`|`%C3%BA`|
|`ñ`|`%C3%B1`|
|`ü`|`%C3%BC`|

📌 **Exemple pràctic:**

```
Original:  hola qué tal?
Codificat: hola%20qu%C3%A9%20tal%3F
```

---

## 📜 **Com codificar i descodificar en JavaScript**

✅ **Codificar (encode)**

```javascript
const text = "café con azúcar";
const encoded = encodeURIComponent(text);
console.log(encoded);  // caf%C3%A9%20con%20az%C3%BAcar
```

✅ **Descodificar (decode)**

```javascript
const decoded = decodeURIComponent(encoded);
console.log(decoded);  // café con azúcar
```

🔸 **Diferències entre `encodeURI()` i `encodeURIComponent()`**

- `encodeURI()` → Manté caràcters especials com `/`, `:`, `?`, `#`, `&`, `=`
- `encodeURIComponent()` → Codifica **tot**, ideal per a paràmetres d’URL

📌 **Exemple comparatiu:**

```javascript
console.log(encodeURI("https://exemple.com/hola qué tal?"));
// https://exemple.com/hola%20qu%C3%A9%20tal?

console.log(encodeURIComponent("hola qué tal?"));
// hola%20qu%C3%A9%20tal%3F
```

---

## 🔥 **Resum Final**

✅ **Les URL han de codificar caràcters especials per evitar errors.** ✅ **L’encoding substitueix caràcters per codis `%XX`.** ✅ **Es pot fer fàcilment en JavaScript amb `encodeURIComponent()` i `decodeURIComponent()`.** ✅ **Sempre hem de descodificar les URL quan rebem informació del servidor.**

🔒 **Controlar correctament l'encoding i decoding de les URL és essencial per evitar problemes de compatibilitat i seguretat!** 🚀