# RootMe - TryHackMe Writeup
![RootMe Room](rootme.png.png)
## Introducción

Este writeup documenta el proceso de compromiso de la máquina **RootMe** en TryHackMe.

Durante el laboratorio se realizaron tareas de reconocimiento, enumeración, explotación web mediante file upload, obtención de una reverse shell y escalada de privilegios hasta conseguir acceso como **root**.

---

## Reconocimiento

Se realizó un reconocimiento inicial del objetivo para identificar servicios expuestos y posibles vectores de entrada.

Como primer paso, se ejecutó un escaneo con **Nmap** para detectar puertos abiertos y servicios activos en la máquina objetivo.

```bash
nmap -sS -sV -O 10.128.172.51
```

![Nmap Scan](Nmap.png)

A partir de los resultados obtenidos, se identificaron dos servicios principales expuestos:

- **SSH (puerto 22)**: utilizado para acceso remoto al sistema.
- **HTTP (puerto 80)**: servidor web Apache.

Dado que no se dispone de credenciales para el servicio SSH, el enfoque se centra en el servicio web, ya que suele ser un vector de ataque común en este tipo de escenarios.

Por lo tanto, se decide continuar con la enumeración del servidor HTTP en busca de directorios ocultos o funcionalidades vulnerables.


## Enumeración

Dado que el servicio HTTP se encuentra disponible, se procedió a realizar una enumeración de directorios utilizando Gobuster.

```bash
gobuster dir -u http://10.128.172.51 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
![Gobuster](2.png)

Posteriormente, se realizó una enumeración más específica incluyendo extensiones comunes como **.php**, **.txt** y **.html**, con el objetivo de identificar archivos potencialmente sensibles en el servidor.

```bash
gobuster dir -u http://10.128.172.51 -w /usr/share/wordlists/dirbuster/directory-list-1.0.txt -x php,txt,html
```
![Gobuster](3.png)

Este segundo escaneo permitió identificar archivos adicionales como **index.php**, así como confirmar la existencia de directorios previamente descubiertos como **/panel** y **/uploads**.

Estos directorios resultan especialmente interesantes:

- **/panel**: podría contener funcionalidades administrativas o formularios de entrada.
- **/uploads**: sugiere la posibilidad de carga de archivos, lo cual puede ser un vector de ataque potencial.

A partir de estos hallazgos, se decide enfocar la siguiente fase en la exploración del directorio **/panel**.


## Explotación

Una vez identificado el directorio `/panel`, se accedió a la funcionalidad de carga de archivos disponible en el sitio web.

El formulario permitía seleccionar y subir archivos al servidor, por lo que se evaluó si esta funcionalidad podía ser utilizada para obtener ejecución remota de código.


























