# Nanobtw Farmer — descargas

Este repositorio solo distribuye los instaladores de **Nanobtw Farmer** para Windows y el aviso firmado que la
app usa para buscar actualizaciones. El código fuente no se publica aquí.

Nanobtw Farmer es una aplicación de Windows para ver y controlar teléfonos Android por ADB, en la red local o por
cable USB. Es software privado que su autor comparte para uso personal, «tal cual», sin garantía.

## Descargar

- Las versiones de la app se publican en [Releases](https://github.com/duarteenc/nanobtw-farmer-releases/releases):
  `NanobtwFarmer-X.Y.Z-setup.exe`, su `.sha256` y la guía de esa versión.
- Todavía no hay ninguna versión de la app publicada. La release `clave-nbf-2026-1` solo contiene la clave pública
  de las actualizaciones.
- Requisitos: Windows 10 u 11 de 64 bits. Se instala para tu usuario, sin permisos de administrador.

## Antes de instalar: comprueba el archivo

En PowerShell, en la carpeta donde lo descargaste:

```powershell
Get-FileHash .\NanobtwFarmer-X.Y.Z-setup.exe -Algorithm SHA256
```

El resultado debe coincidir con el SHA-256 publicado en la página de esa versión. Si no coincide, no lo ejecutes.

El instalador y el programa **no están firmados** con un certificado de Windows. Windows (SmartScreen o Smart
App Control), el navegador o el antivirus pueden mostrar una alerta o bloquearlo. Si aparece cualquier alerta,
detente: no desactives ninguna protección; comprueba el SHA-256 y consulta a quien te pasó el enlace.

## Actualizaciones

- La app instalada consulta
  `https://duarteenc.github.io/nanobtw-farmer-releases/stable/update.json` a los 3 minutos de abrirse y después
  cada 24 horas, o cuando pulsas «Buscar actualizaciones» en Ajustes.
- Ese aviso va firmado con **Ed25519**. La app solo acepta avisos firmados con una clave que su build ya trae;
  cualquier otro aviso se rechaza entero.
  - Clave `nbf-2026-1`: `yG7cqpfW2DHBE2djuAF1N490KrVC5hfMA5bsfZbra1Q=`
    (también en [docs/keys/nbf-2026-1.json](docs/keys/nbf-2026-1.json)).
  - Huella SHA-256 de esa clave pública (32 bytes): `5ae2d4f9a0b1a77dcf0dc8c659e71a343f44d8deb68fd003067645892e29ce76`.
- Nada se instala sin tu permiso: la app avisa de la versión nueva y tú eliges «Descargar» y después «Instalar y
  reiniciar». El instalador descargado solo se usa si su tamaño y su SHA-256 son exactamente los del aviso
  firmado.
- La app solo descarga de este repositorio en GitHub; cada redirección se comprueba (https y servidor permitido).
- Tus datos (`%APPDATA%\NanobtwFarmer`) se conservan al actualizar. Nunca se ofrece una versión anterior.
- La consulta no envía tus teléfonos, ajustes ni registros. Como cualquier web, GitHub ve tu dirección IP y la
  versión de la app (en la cabecera `User-Agent`).

## Qué contacta la app fuera de tu red

- **Google** (`dl.google.com`), la primera vez y solo con tu permiso: Android SDK Platform-Tools (adb), con su
  SHA-256 comprobado. adb no va dentro del instalador.
- **GitHub** (este repositorio): el aviso de actualizaciones y, si aceptas una, su instalador.
- El instalador ejecuta el instalador oficial de **Microsoft** solo si a Windows le falta WebView2.

No hay telemetría.

## Licencias

El programa incluye componentes de terceros (Python, scrcpy-server, pywebview, aiohttp, cryptography y otros).
Sus textos de licencia se instalan en la carpeta `licenses` de la aplicación.

---

## English

This repository only distributes the **Nanobtw Farmer** Windows installers and the signed notice the app reads
to look for updates. The source code is not published here.

- Releases: `NanobtwFarmer-X.Y.Z-setup.exe`, its `.sha256` and that version's guide. No app version has been
  published yet; the `clave-nbf-2026-1` release only holds the updates' public key.
- Before installing, compare `Get-FileHash .\NanobtwFarmer-X.Y.Z-setup.exe -Algorithm SHA256` with the SHA-256
  on the release page. The installer is **not** code-signed: Windows (SmartScreen or Smart App Control), the
  browser or an antivirus may warn or block it. If any warning appears, stop and do not disable any protection.
- Updates: the installed app reads `https://duarteenc.github.io/nanobtw-farmer-releases/stable/update.json`
  (3 minutes after start, then every 24 hours, or on «Buscar actualizaciones»). It is signed with Ed25519 key
  `nbf-2026-1` (`yG7cqpfW2DHBE2djuAF1N490KrVC5hfMA5bsfZbra1Q=`); nothing installs without your explicit
  «Descargar» and «Instalar y reiniciar», and the download must match the signed size and SHA-256. Your data is
  kept. The check sends no phones, settings or logs; GitHub sees your IP address and the app version.
- Outside your network the app only contacts Google (adb, first start, with your permission) and GitHub (updates);
  the installer runs Microsoft's WebView2 installer only if it is missing. No telemetry.
