
Segurament, al fer una auditoria, el que ens trobem més sovint és una **Blind SQL Injection (SQLi)**. A continuació, es detallen els passos a seguir per explotar aquest tipus de vulnerabilitat.

---

## **1. Trobar el SQLi 🔑**

Abans de fer qualsevol altra cosa, el primer que hem de fer és identificar el **payload** que fa vulnerable la web. Per fer-ho de manera automàtica, el millor és realitzar un atac de força bruta amb payloads de SQLi.

Per exemple, podem utilitzar un fitxer de payloads com el següent:

- [Huge SQL Payload List](https://github.com/PenTestical/sqli/blob/main/hugeSQL.txt)

Un cop tinguem aquest fitxer, podem utilitzar una eina com **Burp Suite** per fer força bruta amb aquests payloads i veure com es comporta la web, identificant així quin payload és vulnerable.

---

## **2. Provar l'Atac ⚡**

Un cop trobat el payload vulnerable, el següent pas és executar les **queries** per obtenir informació de la base de dades. La query que utilitzarem és la següent:

```sql
'+OR+(SELECT+IF(SUBSTRING((SELECT+table_name+FROM+information_schema.tables+LIMIT+0,1),1,1)='a',+SLEEP(3),+0));+--+-
```

En aquesta query, hem de realitzar força bruta als següents valors, que estaran marcats en **roig** per fer-los més evidents:

---

##### **Query amb parts a modificar (marcades en roig):**

+OR+(SELECT+IF(SUBSTRING((SELECT+table_name+FROM+information_schema.tables+LIMIT+<span style="color:red">[X]</span>,1),<span style="color:red">[X]</span>,1)='<span style="color:red">[X]</span>',+SLEEP(3),+0));+--+-

---
Els valors marcats en roig representen els següents llocs on farem força bruta:

1. **[X]**: Valors **numèrics** per al límit de la taula (per exemple, el nombre de taules).
2. **[X]**: **Posició** dins de la taula (per exemple, el nombre de columnes).
3. **[X]**: **Caràcters** a comparar amb les dades de la taula (per exemple, la primera lletra d'un nom de taula).

---
## **3. Obtenir Resultats 📊**

Un cop realitzada la força bruta, hem de revisar els resultats. Com que és un atac **time-based**, la diferència es notarà en el **temps de resposta** de la web. Si el temps de resposta és més llarg per a determinats payloads, això indica que el payload és correcte.

Amb aquesta informació, serà útil crear un **script en Python** que, a partir de les respostes obtingudes, pugui generar els noms de les bases de dades, taules, etc.

> **Nota:** Encara cal fer el script! 📝