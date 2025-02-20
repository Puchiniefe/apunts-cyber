# Origen en la Web: Protocol, Host i Port  

Quan accedim a una pàgina web, el navegador utilitza **tres elements clau** per determinar l’origen d’una sol·licitud:  

1️⃣ **Protocol** → Defineix com es transmeten les dades 🔒  
2️⃣ **Host** → És el domini o IP del servidor 🌐  
3️⃣ **Port** → És el canal de comunicació pel qual es fan les connexions 🔌  

💡 **Aquests tres elements junts formen l’"origen" d’una sol·licitud i determinen si dues URL pertanyen al mateix origen o no.**  

---

## 🔹 1. Protocol  

El **protocol** indica **com** es transmet la informació entre el client (navegador) i el servidor. Els més comuns són:  

- 🔓 `http://` → Protocol sense xifrat (no segur)  
- 🔒 `https://` → Protocol segur amb xifrat SSL/TLS  
- 📂 `ftp://` → Per a transferència de fitxers  
- 🔄 `ws://` i `wss://` → Per a WebSockets (comunicació en temps real)  

✅ **URLs amb el mateix host i port però diferent protocol tenen orígens diferents.**  

💡 **Exemple:**  [http://exemple.com](http://exemple.com) ❌ Diferent de [https://exemple.com](https://exemple.com)

---

## 🔹 2. Host (Domini o IP)  

El **host** és el nom de domini o la direcció IP del servidor.  

- **Domini**: `www.exemple.com`  
- **Adreça IP**: `192.168.1.1`  

❌ **Diferents dominis (incloent subdominis) es consideren orígens diferents.**  

💡 **Exemple:**  [https://exemple.com](https://exemple.com) ❌ Diferent de [https://sub.exemple.com](https://sub.exemple.com)
Encara que pertanyin a la mateixa empresa, **es consideren orígens diferents**.  

---

## 🔹 3. Port  

El **port** és un número que especifica el punt d'entrada per establir la connexió. Alguns ports comuns són:  

- 🌍 `80` → HTTP (per defecte)  
- 🔒 `443` → HTTPS (per defecte)  
- 🛠️ `3000`, `8080`, `5000` → Sovint usats per servidors locals o APIs  

✅ **URLs amb el mateix protocol i host però diferent port es consideren diferents orígens.**  

💡 **Exemple:**  [https://exemple.com:443](https://exemple.com:443) ❌ Diferent de [https://exemple.com:8443](https://exemple.com:8443)

---

## 🔥 Resum Final  

| 🏷️ **Element** | 🔍 **Exemple** | ⚠️ **Notes** |
|---------------|--------------|-------------|
| **Protocol** | `https://` | HTTP i HTTPS són diferents orígens |
| **Host** | `exemple.com` | `exemple.com` ≠ `sub.exemple.com` |
| **Port** | `:443` | `:443` ≠ `:8080` |

👉 **Perquè dues URLs siguin del mateix origen, han de tenir el mateix protocol, host i port!** 🚀  
