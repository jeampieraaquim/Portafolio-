# RootMe
```
Creador: ReddyyZ
Direccion Ip: 10.10.102.147
Arquitectura: Linux
Dificultad: Facil
```
# Respuestas 
- 1: No requiere respuesta 
- 2.1: 2 
- 2.2: 2.4.41
- 2.3: ssh
- 2.4: No requiere respuesta
- 2.5: /panel/

- 3.1: THM{y0u_g0t_a_sh3ll}

- 4.1: /usr/bin/python
- 4.2: No requiere respuesta
- 4.3: THM{pr1v1l3g3_3sc4l4t10n}

# Metología
### Ping
Comenzamos verificando la conexion con el servidor

<img width="591" height="273" alt="image" src="https://github.com/user-attachments/assets/968a1273-d78a-4389-bd6a-2eaabf5776e4" />

Confirmada la conexion, escaneamos los puertos

### NMAP
Con el comando "nmap -sC -sV 10.10.102.147"

<img width="806" height="454" alt="image" src="https://github.com/user-attachments/assets/6409fbec-c6a1-486b-b97e-cc7763fd403c" />

Los puertos interesantes seran:
- 22: TCP 
- 80: HTTP

### Comprobacion Web
Antes de usar `gobuster`comprobamos la pagina web 

<img width="1112" height="703" alt="image" src="https://github.com/user-attachments/assets/b1277f08-0fe6-4593-89ee-f87f684ffde2" />

Abrimos el codigo fuente para ver si hay algo interesante

<img width="619" height="475" alt="image" src="https://github.com/user-attachments/assets/bedd64d3-09cc-43f7-9d07-be51073e9715" />

No nos dice mucho, por lo que pasamos al siguiente paso

### Gobuster
Utilizamos el comando "gobuster dir -u http://10.10.102.147 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt"

<img width="1111" height="447" alt="image" src="https://github.com/user-attachments/assets/0adf5814-2632-4bbb-9eab-75b1982842cd" />

Uno de los directorios que coinciden con los espacios de la respuesta es `/panel/`, por lo que comprobamos

<img width="995" height="615" alt="image" src="https://github.com/user-attachments/assets/1a4cc46e-74eb-4a31-a954-0486a650743d" />

Nos deja un menu donde se pueden subir archivos, por lo que podemos usar un php reverse para conseguir acceso

### PHP Reverse
Primero debemos configurar en otra ventana la "conexion", escribiendo "nc -lvp 4444"; eso deja a la escucha todo lo que ocurra en ese puerto

<img width="378" height="111" alt="image" src="https://github.com/user-attachments/assets/1cb40267-39aa-45c4-a04f-a610d94b2c4a" />

Ahora, debemos descargar el php reverse, por lo que en el navegador escribiremos "php reverse shell"

<img width="656" height="179" alt="image" src="https://github.com/user-attachments/assets/59dbe90e-74b5-4bcc-b6bd-b128bd493162" />

Utilizaremos este de github

<img width="745" height="524" alt="image" src="https://github.com/user-attachments/assets/affb9820-3dc5-473c-b10d-12373245272f" />

Abriremos aqui, y copiaremos su contenido

<img width="782" height="177" alt="image" src="https://github.com/user-attachments/assets/ab0c6d47-e436-4722-937a-2072be145bb4" />

Ahora, tenemos que crear un archivo php para que se pueda ejecutar, por lo que en la terminal escribiremos "nano reverse.php" y copiaremos lo de github ahi

<img width="405" height="66" alt="image" src="https://github.com/user-attachments/assets/3368a98e-855f-4d89-9160-3fd91bad0539" />

<img width="728" height="489" alt="image" src="https://github.com/user-attachments/assets/62955022-734c-4b12-98a5-d187396a76a2" />

Dentro, tenemos que modificar lo que dice "change this", en este caso es la direccion ip de nuestra maquina atacante y el puerto donde va a realizarse (4444)
Para conocer neustra ip, escribimos "ip a" y el apartado donde pone "ens5" "inet" nos muestra la direccion ip

<img width="737" height="431" alt="image" src="https://github.com/user-attachments/assets/d8dabcc4-25bf-42aa-8305-47b7e6d8ecb4" />

Ahora, cambiamos

<img width="363" height="95" alt="image" src="https://github.com/user-attachments/assets/4f6a921c-6692-4adb-b73f-ea119958e545" />

"Ctrl 0" y "Ctrl x" y guardamos el archivo
Realizamos un "ls" para verificar que se creo el archivo 

<img width="585" height="127" alt="image" src="https://github.com/user-attachments/assets/4f29e661-c970-4b29-aa59-c5fd182c05ac" />

Con todo preparado, lo subiremos en la pagina web

<img width="532" height="454" alt="image" src="https://github.com/user-attachments/assets/acc647bf-3546-4fea-8878-a8948141a302" />

Parece ser que tiene una proteccion para que no se puedan subir "archivos php", por lo que intentaremos cambiando el nombre "reverse.php5" si esto no funciona, tendriamos que realizar un bypass

<img width="508" height="533" alt="image" src="https://github.com/user-attachments/assets/37599839-4d43-471f-b21c-ce4455f6587a" />

Ahora si se pudo, por lo que nuestro archivo se ha subido con exito, ahora con el comando "10.10.102.147/uploads/" verificamos que este subido

<img width="509" height="249" alt="image" src="https://github.com/user-attachments/assets/68c62cf6-7893-40c8-acac-0da32ca636cb" />

Lo esta, por lo que ahora si lo clicamos nos deberia dar respuesta en la ventana donde hicimos el "listening" del puerto 4444

<img width="723" height="198" alt="image" src="https://github.com/user-attachments/assets/0de6c5e8-e599-4b7b-bb38-408248d3b52f" />

Hemos tenido exito, por lo que comprobamos que permisos tenemos y ver que archivos tenemos acceso

<img width="505" height="585" alt="image" src="https://github.com/user-attachments/assets/c7f79384-9d9a-4f79-8ce6-dcbac5d6dedf" />

En este punto, tenemos que buscar el fichero "user.txt" por lo que escribiremos "find / -name user.txt 2>/dev/null"
Asi mismo, para abrirlo usamos el "cat /var/www/user.txt"

<img width="329" height="96" alt="image" src="https://github.com/user-attachments/assets/d94f591d-1550-45a1-ad41-5797e377be98" />

### Escalada de privilegios
Primero debemos buscar un archvio SSIUD interesante por lo que escribiremos "find / -user root -perm /4000"

<img width="455" height="307" alt="image" src="https://github.com/user-attachments/assets/eb2a8b21-998e-4a52-af10-ecbfea56c382" />

Hemos encontrado un "/usr/bin/python2.7"
Utilizaremos un comando de "GTFOBins", escribimos en el navegador

<img width="812" height="356" alt="image" src="https://github.com/user-attachments/assets/7bf8f50d-8c0f-44cb-ae73-de812af0a22c" />

Buscaremos un SSIUD de python

<img width="838" height="86" alt="image" src="https://github.com/user-attachments/assets/9489b26a-4761-4405-8ee1-29546b8c8b3a" />

<img width="872" height="311" alt="image" src="https://github.com/user-attachments/assets/ed9c28b3-0306-4ce5-bfe5-f4003fbd2000" />

Seleccionaremos este shell cambiando los datos por el archivo SSIUD que encontramos "/usr/bin/python2.7 -c 'import os; os.setuid(0); os.system("/bin/bash")'"

<img width="683" height="80" alt="image" src="https://github.com/user-attachments/assets/6496f6f4-356e-44cf-a79c-dd979274c457" />

Escribimos "whoami" y somos "root"
Para buscar el ultimo fichero, volvemos a usar el comando "find / -name root.txt 2>/dev/null"
Asi mismo, utilizamos "cat /root/root.txt" y tenemos la ultima bandera

<img width="303" height="88" alt="image" src="https://github.com/user-attachments/assets/f7ec8da6-02f1-42d5-bb22-c2072792a57a" />



