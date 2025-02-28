## *🔍 1. Definició*

SQL Injection (SQLi) és una vulnerabilitat de seguretat que permet a un atacant interferir en les consultes que una aplicació fa a la seva base de dades. Succeeix quan una aplicació no valida adequadament l'entrada de l'usuari i permet l'execució de comandes SQL maliciosos.

---

## *⚠️ 2. Tipus de SQL Injection*

### 🔹 2.1 SQLi Clàssic o In-band

- *Basat en errors (Error-based):* L'atacant provoca errors en la base de dades per obtenir informació.
    
- *Basat en la unió (UNION-based):* S'usa la clàusula UNION per extreure dades addicionals de la base de dades.
    

### 🔹 2.2 Blind SQLi

- *Boolean-based:* Es fan consultes condicionals per determinar si una afirmació és verdadera o falsa.
    
- *Basat en el temps:* S'utilitzen funcions de retard (SLEEP(), WAITFOR DELAY()) per inferir dades segons el temps de resposta.
    

### 🔹 2.3 SQLi Fora de Banda (OOB)

- S'usa quan no hi ha retroalimentació directa de l'error i s'envien dades a un servidor extern controlat per l'atacant.
    

---

## *💻 3. Exemple de SQLi*

### 🔸 Consulta vulnerable


```
SELECT * FROM usuarios WHERE usuario = '" + usuario + "' AND password = '" + password + "';
```

Si un atacant ingressa admin' -- en el camp de usuari, la consulta es converteix en:

```
SELECT * FROM usuarios WHERE usuario = 'admin' --' AND password = '';
```

El -- comenta la resta de la consulta, permetent accés sense necessitat de contrasenya.

---

## *🚨 4. Conseqüències*

- 🕵️‍♂️ Robatori d'informació confidencial.
    
- ✍️ Manipulació de dades.
    
- 🚪 Accés no autoritzat.
    
- ❌ Eliminació de bases de dades.s de datos.