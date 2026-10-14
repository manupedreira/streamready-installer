<p align="center"><img src="logo.svg" width="96" height="96" alt="StreamReady"></p>

<h1 align="center">StreamReady</h1>

<p align="center"><em>Like streaming, minus the buffering.</em></p>

StreamReady monta en tu casa un servidor multimedia para la tele. Tiene listo el siguiente episodio antes de que le des al play, no descarga lo que ya está en Netflix o Prime, y se configura en unos clics.

> **Versión de pruebas.** Este repositorio solo contiene el instalador. El código de StreamReady es privado y está protegido por derechos de autor (ver [LICENSE.txt](LICENSE.txt)).

## Qué necesitas

- Un **ordenador con Windows 10 u 11** que esté encendido cuando queráis ver algo. Hará de servidor para todas las teles y móviles de casa.
- Espacio en disco: unos 2–4 GB por película en HD, o el doble o más en 4K.
- Una **tele con tienda de apps** (LG, Samsung, Android TV, Fire TV…) o un móvil.

## Instalación

1. Descarga `StreamReady-Setup-x.y.z.exe` desde [Releases](../../releases/latest).
2. *(Recomendado)* Comprueba que el archivo es el original. En PowerShell:
   ```powershell
   Get-FileHash .\StreamReady-Setup-x.y.z.exe -Algorithm SHA256
   ```
   El resultado tiene que coincidir con el que aparece en la página de la versión.
3. Ábrelo. Como es una versión de pruebas sin firma digital, Windows mostrará **"Windows protegió tu PC"**. Pulsa **Más información → Ejecutar de todas formas**.
4. Acepta la licencia y deja que instale lo necesario. Al terminar se abre el asistente en tu navegador.
5. Responde a las preguntas del asistente: dónde guardar el contenido, tu usuario, si tu tele es 4K, el idioma y tus plataformas.
6. Último paso: añade tus fuentes de búsqueda en Prowlarr, como te indica el asistente.

## En la tele

1. Abre la tienda de apps de la tele e instala **Jellyfin**.
2. Ábrela: encontrará tu ordenador sola. Si no, escribe la dirección que te mostró el asistente al terminar.
3. Entra con el usuario que creaste.

## Panel de StreamReady

Desde el móvil o el ordenador, en `http://<tu-ordenador>:8765`: qué está listo para ver, qué está en tus plataformas, qué se está descargando y todos los ajustes. En el iPhone, **Compartir → Añadir a pantalla de inicio** para tenerlo como una app.

## Problemas y sugerencias

Abre un [issue](../../issues) contando qué hacías, qué esperabas y qué pasó. Una captura ayuda mucho.

## Aviso

StreamReady no incluye ni recomienda fuentes de contenido. Cada usuario es responsable de las fuentes que configura y de respetar la legislación y los derechos de autor. Los programas de terceros que instala (Jellyfin, Sonarr, Radarr, Prowlarr, Bazarr, qBittorrent…) se rigen por sus propias licencias.

Copyright © 2026 Manuel Pedreira. Todos los derechos reservados.
