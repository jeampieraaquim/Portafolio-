# HeartBleed
```
Creador: Dex01
Direccion Ip: 54.194.103.67
Arquitectura: Linux
Dificultad: Facil
```
# Respuestas 
- THM{sSl-Is-BaD}

# Metología
### Ping
Comenzamos verificando la conexion con el servidor

<img width="574" height="260" alt="image" src="https://github.com/user-attachments/assets/bbe2ca7f-94bb-49a4-a8ed-8c795444b32d" />

Es positiva, por lo tanto escanearemos los puertos para ver que hay

### NMAP
Realizamos el escaneo con el comando "nmap -sC -sV 54.194.103.67"

<img width="807" height="611" alt="image" src="https://github.com/user-attachments/assets/3ccd9fdd-31ee-4aa4-916c-cd297d7f3222" />

Los puertos abiertos son:
- 22: SSH
- 111: RPCBIND
- 443: SSL/HTTP

# MSFCONSOLE
Como estamos revisando la vulnerabilidad `Heartbleed` vamos a usar msfconsole ya que posee un expoloit que nos ayudara a explotarla
Para ello, abrimos la interfaz con "msfconsole", luego "search heartbleed"

<img width="753" height="510" alt="image" src="https://github.com/user-attachments/assets/7e032936-1e85-49ae-a591-af9c43567bc4" />

<img width="811" height="468" alt="image" src="https://github.com/user-attachments/assets/7874aa9e-55c6-41b4-a7c4-f70ec4175b0b" />

En este caso usaremos este exploit, para ellos añadimos "use scanner/ssl/openssl_heartbleed", luego "set RHOST 54.194.103.67" y luego para que nos muestre los resultados "set verbose true" y luego "run"

<img width="680" height="129" alt="image" src="https://github.com/user-attachments/assets/abde9762-05f1-4797-9cc0-44a1a548c20c" />

Esperamos los resultados, y buscamos la "flag"

<img width="806" height="666" alt="image" src="https://github.com/user-attachments/assets/452d86a9-abae-47c7-9997-2a11b9ef5503" />

¡Lo tenemos!



