# Fenix VPN Reversed Configs

Este repositorio contiene el analisis, descifrado y normalización de las configuraciones de servidores la aplicacion **Fenix VPN**. En el proyecto documento como se superaron las multiples capas de seguridad para exponer los servidores.

## Detalles de la ingeniería inversa

El proceso de extraccion se dividio en tres fases criticas para romper la seguridad de la aplicacion:

1.  **Formatos camuflados:** Las configuraciones se ocultan en archivos `.png` dentro de los assets. Se descifraron usando **AES-256-CBC** con una derivación de clave basada en MD5 (similar a OpenSSL).
    * **Clave Layer 1:** `🔥🔥🔥vpnfenix⭐️⭐️⭐️`

2.  **Ofuscacion de bits:**
    Las claves internas no estaban en texto plano. Se recuperaron analizando operaciones de bits (`>>>`) y desplazamientos en el codigo Java ofuscado.
    * **Clave Layer 2:** `FenxM22_07!89Dev`

3.  **Nested Encryption:**
    Los valores individuales del JSON (Ips, Payloads, Snis) estaban doblemente encriptados con **AES-128-CBC** (donde los primeros 16 bytes del Base64 son el IV) y un post-procesado de **Cifrado cesar (ROT-21)**.



## Estructura

* `/configs`: Archivos JSON normalizados con nombres de servidores, IPs, puertos y payloads legibles.
* `/raw`: Ejemplos de las peticiones encriptadas originales (`dehere...`).

## Normalizacion
Durante el proceso de reversion, mapee algunas llaves ofuscadas nada mas para hacerlas mas entendibles:
* `p0PgL3l0d89...` -> **Name**
* `U7V8DoP4cY...` -> **ServerIP**
* `p9ZPlMv9V7...` -> **ServerPort**
* `66P9ZUEM1j...` -> **Payload_Info**
* `mtw364P3Zs...` -> **SNI**
