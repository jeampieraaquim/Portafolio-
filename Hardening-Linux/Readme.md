# Hardening-Linux
```
Arquitectura: Kali Linux GNU | Ubuntu | 2025.3
Dificultad: Fácil
```

# Objetivo 
Este proyecto consiste en la auditoría y endurecimiento completo de un sistema Linux, siguiendo buenas prácticas de seguridad usadas en entornos empresariales.

# Metodología
Vamos a repasar los pasos que necesitamos para realizar correctamente la práctica

### Creación de usuario
Comando utilizado: sudo adduser jjean
Creamos un usuario administrativo siguiendo buenas prácticas de seguridad.

<img width="418" height="219" alt="image" src="https://github.com/user-attachments/assets/dfa29d60-7924-4e27-8622-806809832669" />

### Añadir usuario a grupo sudo 
Comando utilizado: sudo usermod -aG sudo jeean

<img width="263" height="50" alt="image" src="https://github.com/user-attachments/assets/7cec3313-196b-40d3-9daf-16e94934e601" />

Y comprobamos que este dentro del grupo con 'groups jeean'

<img width="211" height="62" alt="image" src="https://github.com/user-attachments/assets/aa04e18a-975a-42cd-b15f-9ee971abd145" />

### Bloqueo del usuario root para evitar autenticación directa 
Esto nos sirve para que no haya inicios de sesión de root a menos que sea desde el usuario que hemos creado (jeean)
Con el comando: sudo passwd -l root (deshabilitamos) y con sudo passwd -S root (comprobamos que  este bloqueado)

<img width="256" height="130" alt="image" src="https://github.com/user-attachments/assets/808de2f6-1905-4277-b7c6-a29153112dcd" />

### Logear con usuario creado 
Comprobamos con el comando: sudo - 

<img width="231" height="76" alt="Captura de pantalla 2025-11-17 193706" src="https://github.com/user-attachments/assets/d4b885e6-3285-4f8a-b40d-254134f9d026" />

Aqui hemos comprobado que, el acceso a root esta bloqueado. Lo que nos reduce el riesgo criticos en el sistema

### SSH Hardening
Verificamos el estado del servicio ssh 

<img width="701" height="357" alt="Captura de pantalla 2025-11-17 195429" src="https://github.com/user-attachments/assets/7836a23b-b46a-4b43-a83c-8d565e0d0a30" />

Nos indica que esta activo, proseguimos

Aunque el sistema no permite acceso remoto, "endurecenmos" completamente el servicio ssh dentro de las configuraciones del mismo, deshabilitando el acceso root, habilitando las credenciales públicas

<img width="323" height="419" alt="image" src="https://github.com/user-attachments/assets/3cd18cac-db42-4bd9-a0d2-e398fe9e3eca" />

Guardamos, y reiniciamos el servicio 

<img width="711" height="330" alt="Captura de pantalla 2025-11-17 200719" src="https://github.com/user-attachments/assets/81ad103c-1a35-43a2-a10f-de1ec6d99e23" />



















