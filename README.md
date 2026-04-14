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

<img width="961" height="757" alt="1" src="https://github.com/user-attachments/assets/fb91d9f0-bc56-4783-9779-817179f94ab4" />
