Les cookies són fragments de informació que els servidors envien als navegadors per a ser guardats i enviats futurament "de vuelta" en solicitus futures.(Es guarden en el navegador). Les cookies s'utilitzen per a tenir sessions i guardar preferències de la web d'un usuari (per exemple si vol la web en blanc o negre). Els navegadors permeten controlar el comportament de les cookies mitjançant els següents atributs:

## 1. Name (Nom)
#### Descripció 
És el nom únic de la cookie. El nom és important per a que el servidor identifiqui la cookie.
#### Exemple
"sessionid","php_session"...
#### Normes
El nom per a cada domini (pàgina web), ha de ser únic, no pot ser que hi hagi una web amb 2 cookies de diferenta informació amb el mateix nom.

## 2. Value (Valor)
#### Descripció
És el valor asociat al nom de la cookie, aquest està guardat al navegador i s'envia en cada solicitud HTTP , d'aquesta manera el servidor sap quina informació està relacionada amb un usuari.
#### Normes
El text pot ser qualsevol cadena de text, excepte el punt i coma ";" i el espai en blanc " ".
## 3. Domain (Dominio)
#### Descripció
Especifica el domini i el subdomini al que pertany la cookie, com a molt el subdomini pot ser un subcojunt del domini actual. Bàsicament diu quines webs poden accedir a la cookie.
#### Exemple
.exemple.com, vol dir que serà accessible desde www.exemple.com, vpn.exemple.com ...
#### Normes
Si no s'especifica un domini s'estableix per default el domini del servidor.
## 4. Path (Ruta)
#### Descripció
Defineix en quins directoris de la web s'enviarà la cookie. A la resta no s'enviarà
#### Normes
Si no es defineix un *path*, s'assignarà el *path* actual de la URL.
## 5. Expires (Caducitat)
#### Descripció
La data i hora en la que la cookie caducarà. SI no s'especifica, la cookie serà de sessió (osigui, s'eliminarà al tancar el navegador).
#### Format
La data ha d'estar especificada en format **GMT**.
#### Normes
Si no s'especifica data de caducitat, la cookie serà temporal i s'eliminarà al tancar el navegador.
## 6. Max-Age (Màxima vida)
#### Descripció
És similar a Expires però almenys de dir una data en que s'eliminarà la cookie

