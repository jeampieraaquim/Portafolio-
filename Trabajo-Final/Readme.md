# Informe Técnico de auditoria
```
Autor: Jeampier Aquim Núñez
Fecha: 03/11/2025
```

# Índice
```
Contents
Portada	1
Índice	2
Introducción	3
Requisitos técnicos	3
Marco teórico	4
Recopilación de información	4
Fase de explotación	9
Post explotación	22
Priv / esc	24
Situación actual	25
Posibles riesgos asociados	26
Tabla de vulnerabilidades	26
Descripción de cada vulnerabilidad detectada	27
Recomendaciones	30
Recomendaciones Generales	31
Valoración del auditor	31
Conclusión	32
Anexos	33
```

# Introducción 

El informe realizado, documenta el proceso y los resultados de la auditoría de seguridad (pentest) realizada en un entorno controlado de laboratorio sobre dos máquinas virtuales: Máquina 1 (Windows Server 2012) y Máquina 2 (Terremoto). 
El objetivo fue identificar, explotar y evidenciar vulnerabilidades, mostrar el riesgo real y proponer medidas correctivas. Se realizaron reconocimiento, enumeración, explotación no destructiva, post-explotación y escalada de privilegios.
 La severidad de los hallazgos se ha evaluado con CVSS v3.1 y complementada con el juicio técnico del auditor. Las pruebas se llevaron a cabo bajo autorización explícita del cliente; quedaron excluidas denegaciones de servicio, ingeniería social y cualquier acción fuera del entorno autorizado.

# Requisitos técnicos

1.	Requisitos técnicos y metodológicos
Las pruebas se realizaron en un entorno de laboratorio aislado compuesto por dos máquinas virtuales:
-	Máquina 1: Windows Server 2012
-	Máquina 2: Windows (Terremoto)
El equipo atacante fue una distribución Kali Linux, configurada en red interna para garantizar aislamiento total y control del tráfico. Se emplearon herramientas de uso profesional (Nmap, Gobuster, WPScan, Nessus, Hydra, Crackmapexec, Evil-WinRM y Metasploit)
2.	Requisitos legales y éticos
Las pruebas realizadas fueron autorizadas por escrito, limitadas al entorno controlado del laboratorio, con fines educativos. Se prohíbe compartir cualquier tipo de información sensible o información acerca de los laboratorios y de la práctica realizada.





















