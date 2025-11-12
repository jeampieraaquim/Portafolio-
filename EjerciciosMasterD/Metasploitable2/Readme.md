# Metasploitable 2 
```
Creador: Rapid7
Dirección IP: 192.168.56.101
Arquitectura: Linux
Dificultad: Media
```
# Objetivo
En el presente ejercicio, vamos a tratar de enumerar y explotar todas las vulnerabilidades posibles en el laboratorio virtual 'Metasploitable2'
 
# Escaneo y numeración
### Netdiscover ### 
Comando utilizado: netdiscover 

Resultados:

<img width="626" height="149" alt="image" src="https://github.com/user-attachments/assets/6267c948-c58e-43b9-ad36-fed26dcffbbe" />

Dirección IP: 192.168.56.101

### Ping
Comando utilizado: ping -c 5 [ip]

Resultados:

<img width="516" height="208" alt="image" src="https://github.com/user-attachments/assets/fe746c0c-c1b0-43e2-b9f6-c6e6fb5275c0" />

Interpretación: Responde correctamente a las peticiones ICMP por lo que asumimos que existe conexión.

### NMAP 
Comando utilizado: nmap -sC -sV [ip]

Resultados:

<img width="1213" height="839" alt="image" src="https://github.com/user-attachments/assets/6a946bd3-1222-4951-856c-5304d5f8396f" />

<img width="1331" height="828" alt="image" src="https://github.com/user-attachments/assets/4ed5da37-a5a4-41c1-a7d2-7d64c44943c2" />

<img width="792" height="317" alt="image" src="https://github.com/user-attachments/assets/62aa9955-f673-4b12-ab4c-e7a1d87eab27" />

Interpretación: Tenemos multiples puertos abiertos, por lo que tenemos muchas vias posibles para realizar un ataque.

### Nessus
Fuimos a la pagina web y realizamos el escaneo.

Resultados:

<img width="576" height="336" alt="image" src="https://github.com/user-attachments/assets/028f328f-c8d1-41bb-a036-072196f5eead" />

Interpretación: Hemos encontrado 116 vulnerabilidades, entre las cuales hay: criticas [8], altas [5], medias [18], bajas [8] e informativas [77]

# Explotación puerto por puerto 

### Puerto 21 FTP

<img width="441" height="225" alt="image" src="https://github.com/user-attachments/assets/45cc88a9-f32c-4898-9ab0-3ab33eb43f6b" />


- Login permitido sin credenciales

Vemos que permite logins 'Anonymous'

<img width="313" height="186" alt="image" src="https://github.com/user-attachments/assets/7cd896fa-3397-4969-be62-7dce303ed105" />

Hemos obtenido acceso, por lo que con comando sencillos podriamos extraer información sensible

<img width="476" height="164" alt="image" src="https://github.com/user-attachments/assets/12c032f7-b028-4e1f-ab5c-4d092e7730af" />

- Acceso con msfconsole

Como tenemos la versión en la que corre el puerto 21 (vsftpd 2.3.4), buscamos un exploit con ese mismo nombre.
Utilizaremos "search vsftpd 234" 

<img width="937" height="171" alt="image" src="https://github.com/user-attachments/assets/1b5872fb-7c9f-49e0-abbd-fd58e07a0a0e" />

Configuraremos correctamente

<img width="934" height="309" alt="image" src="https://github.com/user-attachments/assets/bfefabed-bac4-4633-ab38-d62bf828b7f9" />

Y tenemos Shell

<img width="887" height="127" alt="image" src="https://github.com/user-attachments/assets/7cc03e38-fbe3-4cd4-aae2-d2ce5e24f5c8" />

Comprobamos archivos

<img width="108" height="409" alt="image" src="https://github.com/user-attachments/assets/f4da0ee9-3f3f-47fa-9551-dc0ef9a39900" />

- Ataque de fuerza bruta

En caso de no tener credenciales podriamos utilizar un ataque de diccionario con hydra.

<img width="942" height="166" alt="image" src="https://github.com/user-attachments/assets/7b9d563a-aebf-4030-b56f-caa35f6cdc5e" />

Credenciales obtenidas 'user:msfadmin | password: msfadmin'

- Comprobación de credenciales obtenidas con hydra

<img width="931" height="496" alt="image" src="https://github.com/user-attachments/assets/514842b3-3dc2-4424-a859-7550fb28d6b8" />

Hemos obtenido acceso a mas información sensible, incluso obtener el archivo 'id_rsa' que es donde se encuentran las claves públicas y privadas.

### Puerto 22

<img width="579" height="67" alt="image" src="https://github.com/user-attachments/assets/75ade74d-d319-431f-8ce2-64aac7bd0f01" />

Como hemos obtenido credenciales en el paso anterior, las utilizaremos para realizar conexión remota

<img width="897" height="57" alt="image" src="https://github.com/user-attachments/assets/07b872fa-1127-43e6-8fcc-83a79588d48a" />

No es posible, por lo que pasaremos a usar msfconsole

- Msfconsole

Buscamos el exploit 'ssh login'

<img width="937" height="143" alt="image" src="https://github.com/user-attachments/assets/b4102fd9-ccbf-498d-9926-cea5fdf20198" />

Configuramos correctamente

<img width="932" height="474" alt="image" src="https://github.com/user-attachments/assets/60220725-e4c9-42b7-9bce-5b00188981f2" />

Se ha creado la sesión

<img width="949" height="146" alt="image" src="https://github.com/user-attachments/assets/c7575243-2bed-4b97-933f-79e183b74e1b" />

Y comprobamos 

<img width="660" height="271" alt="image" src="https://github.com/user-attachments/assets/8a269f1f-f9e1-45e8-86a7-b0f41e2f3d54" />

### Puerto 23 Telnet

<img width="335" height="22" alt="image" src="https://github.com/user-attachments/assets/45856ea2-7699-4a32-9c7d-caa71c0f28c9" />

Al igual que en los puertos anteriores usaremos msfconsole y buscaremos 'telnet login'

<img width="401" height="70" alt="image" src="https://github.com/user-attachments/assets/de8f9a7e-fb33-4654-90d5-749c11fca5ce" />

Configuramos correctamente

<img width="937" height="478" alt="image" src="https://github.com/user-attachments/assets/1f504610-c838-40c5-924e-f05beed1bfdf" />

Run/exploit y tenemos shell 

<img width="882" height="120" alt="image" src="https://github.com/user-attachments/assets/fbdc0bd8-bed6-42d2-86fd-b06b01ae3557" />

Abrimos la session creada con 'sessions 1'

<img width="649" height="343" alt="image" src="https://github.com/user-attachments/assets/200cce1f-1719-4110-9efe-3e80aed90585" />

### Puerto 25 SMTP

<img width="937" height="245" alt="image" src="https://github.com/user-attachments/assets/9819f425-1ff9-4994-99d1-3bdd35a54fa1" />

Buscaremos el exploit 'smtpd enum' 

<img width="445" height="197" alt="image" src="https://github.com/user-attachments/assets/74d5dc10-325e-4a4c-8965-4b60fa2ddce1" />

Configuramos correctamente

<img width="936" height="209" alt="image" src="https://github.com/user-attachments/assets/e8f11215-311b-4a65-bb17-c0cfc4c6393b" />

Damos a exploit

<img width="931" height="525" alt="image" src="https://github.com/user-attachments/assets/ee46d2da-fdcf-4004-8e52-90d008e52b8d" />

Obtenemos usuarios:
- backup, bin, daemon, distccd, ftp, games, gnats, irc, libuuid, list, lp, mail, man, mysql, news, nobody, etc

Con estos usuarios, podriamos explotar el puerto 21 con otro exploit ej 'auxiliary/scanner/ftp/ftp_login'

### Puerto 53 open domain

<img width="349" height="55" alt="image" src="https://github.com/user-attachments/assets/972cf869-896e-4bb2-94e6-f419724c78a8" />

Para este puerto, teniendo en cuenta la versión ISC BIND 9.4.2, vamos a proceder con un exploit que envenenara el cache y controlara el tráfico de los clientes que se conecten

<img width="351" height="110" alt="image" src="https://github.com/user-attachments/assets/cefa87fb-4903-4ddd-9fd0-0ae0621c8edf" />

Configuramos correctamente

<img width="935" height="294" alt="image" src="https://github.com/user-attachments/assets/2cc3a594-a476-4805-8961-3ee6cb9dd8ab" />

Exploit

<img width="938" height="219" alt="image" src="https://github.com/user-attachments/assets/727ba090-f800-419f-981b-784764bf7785" />

En este caso no hubo respuesta ya que no cuenta con salida a internet.

### Puerto 80 HTTP

<img width="526" height="51" alt="image" src="https://github.com/user-attachments/assets/2053ac23-95e3-405e-a10e-7137756f1f2c" />

Abrimos la direcciñón ip en el navegador

<img width="562" height="468" alt="image" src="https://github.com/user-attachments/assets/56a90018-0cba-49c4-a4f1-ead2feb92794" />

Y en este caso ya nos muestra credenciales validas 'msfadmin:msfadmin' 

Utilizamos gobuster para buscar ficheros ocultos

<img width="849" height="722" alt="image" src="https://github.com/user-attachments/assets/fe61b26d-cc6e-4fea-86d4-e24a6e0fc325" />

Si exploramos un poco 

<img width="576" height="189" alt="image" src="https://github.com/user-attachments/assets/b1023470-0cce-4ad5-8276-cc0cbb8fd0d4" />

Tenemos acceso a archivos 

<img width="497" height="537" alt="image" src="https://github.com/user-attachments/assets/7f0bf4a7-3c8f-48ca-b2c3-b5e49679b5a8" />

<img width="952" height="743" alt="image" src="https://github.com/user-attachments/assets/77b661d7-81af-46f1-9aaf-9b962cbbae64" />

<img width="425" height="609" alt="image" src="https://github.com/user-attachments/assets/d11194f1-1d60-493e-b227-bb002524dfd5" />

En 'DVWA' también nos proporciona usuarios validos 'admin:password'

<img width="900" height="739" alt="image" src="https://github.com/user-attachments/assets/e6637a22-7f67-4ea7-90a8-fc37b5bec022" />

<img width="543" height="246" alt="image" src="https://github.com/user-attachments/assets/b351e54a-a239-43bf-bda0-ed00b16c3655" />

Si lo quisieramos hacer con 'msfconsole' buscamos el exploit 'slowloris dos' que es una de las vulnerabilidades que nos dio nessus

<img width="316" height="118" alt="image" src="https://github.com/user-attachments/assets/48094ec5-d5f6-4642-94d5-7ecd0a803e2d" />

Configuramos correctamente 

<img width="753" height="182" alt="image" src="https://github.com/user-attachments/assets/15ea3989-6ac3-4b29-adf5-e3b759097579" />

 Y, exploit

<img width="430" height="357" alt="image" src="https://github.com/user-attachments/assets/05a5cf3c-c598-4c18-92ff-a7c54a74e2c4" />








