# Instalar StreamReady en casa, paso a paso

StreamReady junta en un solo sitio lo que veis en Jellyfin, Netflix, Prime Video y Stremio: qué estáis viendo, vuestra lista, en qué plataforma está cada cosa y sugerencias. Todo aparece también en la tele, dentro de Jellyfin.

Tiempo: unos 30–45 minutos la primera vez.

## Qué hace falta

- **Un ordenador con Windows 10 u 11 que esté siempre encendido**. Hará de servidor para la tele y los móviles de casa. No hace falta que sea potente.
- **Google Chrome** en ese ordenador, con la sesión de Netflix y Prime Video iniciada.
- **Una tele con la app de Jellyfin**: LG (webOS), Android TV o Google TV y Fire TV la tienen en su tienda. En Samsung no está en la tienda oficial.
- Opcional: una cuenta de **Stremio**.

Ninguna contraseña de Netflix, Prime o Stremio pasa por StreamReady.

---

## 1 · Jellyfin

Jellyfin es la app que veréis en la tele. StreamReady pone en ella vuestra lista, lo que estáis viendo y las sugerencias.

1. **Instálalo** desde [jellyfin.org/downloads/server](https://jellyfin.org/downloads/server) (Windows). O en PowerShell como administrador:
   ```powershell
   winget install Jellyfin.Server
   ```
2. **Ábrelo**: en el navegador, `http://localhost:8096`. Sigue su asistente:
   - idioma **Español** y país **España**;
   - crea tu **usuario** (con él entraréis en la tele);
   - **bibliotecas**: si tenéis vídeos propios, añade una de *Series* y otra de *Películas* con sus carpetas. Si no tenéis, sáltalo: StreamReady crea las suyas.
3. **Ajuste recomendado**, para poder ordenar por «cuándo lo metimos en la lista»: *Panel de control → Bibliotecas → Visualización → Fecha de añadido* → **usar la fecha de creación del fichero**. El nombre exacto puede variar según la versión de Jellyfin.
4. **Opcional:**
   - *Intro Skipper*, para el botón «Saltar intro» en vuestros vídeos. Se añade su repositorio en *Panel → Plugins → Repositorios*.
   - *Home Screen Sections*, para que las colecciones salgan como filas en el inicio.

## 2 · La red de casa

Para que la tele y el móvil encuentren el ordenador:

1. *Configuración → Red e Internet → (tu conexión) → Tipo de perfil de red*: **Privada**. Si es «Pública», Windows bloquea a los demás dispositivos.
2. Permisos de Jellyfin en el cortafuegos. En PowerShell como administrador:
   ```powershell
   New-NetFirewallRule -DisplayName "Jellyfin" -Direction Inbound -Protocol TCP -LocalPort 8096 -Profile Private -Action Allow
   New-NetFirewallRule -DisplayName "Jellyfin descubrimiento" -Direction Inbound -Protocol UDP -LocalPort 7359 -Profile Private -Action Allow
   ```
   El de StreamReady (su panel) lo crea su instalador.

## 3 · StreamReady

1. Descarga `StreamReady-Setup-x.y.z.exe` de [Releases](../../releases).
2. *(Recomendado)* Comprueba que es el original: su huella SHA-256 está en la página de la versión.
   ```powershell
   Get-FileHash .\StreamReady-Setup-x.y.z.exe -Algorithm SHA256
   ```
3. Ábrelo. Como aún no tiene firma digital, el navegador puede avisar al descargarlo y Windows mostrará «Windows protegió tu PC»: **Más información → Ejecutar de todas formas**.
4. Al terminar se abre el **asistente** en el navegador: entra con tu usuario de Jellyfin y marca vuestras plataformas (Netflix, Prime Video…).

El panel de StreamReady queda en `http://localhost:8765` en ese ordenador, y en `http://<IP-del-ordenador>:8765` desde el móvil (el asistente te dice la dirección).

## 4 · Netflix y Prime Video (extensión de Chrome)

La extensión lee vuestra lista, por dónde vais y lo que habéis visto, con la sesión que ya tenéis abierta, y se lo pasa a StreamReady en el mismo ordenador. Lo hace una vez al día sola, y cada vez que abrís esas páginas.

1. En Chrome, abre `chrome://extensions` y activa **Modo de desarrollador** (arriba a la derecha).
2. **Cargar descomprimida** → elige `C:\Program Files\StreamReady\extension`.
3. Fíjala en la barra: icono del puzle → chincheta junto a StreamReady.
4. Inicia sesión en **Netflix** y **Prime Video** en ese Chrome. En Netflix, entra una vez con el perfil que uséis, para que no pregunte «¿Quién está viendo?».
5. Abre la extensión: tiene que decir **«● Conectado con StreamReady»**. Pulsa **Actualizar ahora**.
6. Para que la lectura diaria funcione sola, Chrome tiene que estar abierto: ponlo a arrancar con Windows (`Win + R` → `shell:startup` → acceso directo a Chrome).

En su ventana eliges la franja horaria de la lectura diaria (por defecto, de 18:00 a 22:00).

**Historial antiguo de Netflix** (recomendado, una vez): en Netflix → Cuenta → Perfiles → vuestro perfil → Actividad de visionado → **Descargar todo**. Sube ese fichero en StreamReady → *Ajustes → Conexiones → Carga inicial*. Así las sugerencias aprenden de años de historial. Para todos los perfiles a la vez, sube en su lugar el ZIP de *Cuenta → Descargar tu información personal* (tarda unos días en llegar).

**Historial antiguo de Prime Video** (opcional, una vez): en Amazon → Cuenta → *Solicitar tus datos* → Prime Video. El ZIP llega por correo en unos días; súbelo en el mismo sitio. StreamReady solo lee de él el historial y vuestra lista.

Las exportaciones no meten nada en vuestra lista: lo que estuvo en ella alguna vez sale en el panel, en «Estuvieron en vuestra lista», por si queréis recuperar algo.

## 5 · Stremio (opcional)

*Ajustes → Conexiones → Stremio → Conectar Stremio* y sigue los tres pasos (copiar la clave de sesión desde web.stremio.com). StreamReady lee vuestra biblioteca cada 6 horas.

## 6 · Cómo queda en Jellyfin

**Vuestra lista** es «Mi lista» de Netflix y Prime y la biblioteca de Stremio, tal como están hoy. Lo que quitáis en la plataforma sale también de StreamReady. Lo que la plataforma retira de su catálogo se queda en vuestra lista y sale en Novedades, para que no le perdáis la pista.

- **Fichas** de lo que está en vuestra lista o en «Para ti» y no tenéis en casa, con póster, sinopsis y temporadas. Al reproducirlas, un aviso dice en qué plataforma está.
- **Colecciones**: «Nuestra lista», «Viendo», «Para ti», y secciones por plataforma («Series · Netflix», «Películas · Jellyfin»…).
- **Bibliotecas**: por defecto, «Series en plataformas» y «Películas en plataformas». Si preferís todo junto en «Tus series» y «Tus películas», marcad *Ajustes → Jellyfin → Juntarlo con vuestras bibliotecas* (no mueve ni borra vuestros vídeos).
- **Sugerencias**: en sus propias bibliotecas, «Series para ti» y «Películas para ti».
- **Quitar algo de «Viendo»**: márcalo como visto (✓) en Jellyfin. Vuelve solo si avanzáis en alguna plataforma.
- **♥ = «Me gusta»**: no añade nada a vuestra lista, pero refuerza las sugerencias.
- **Orden**: en cada biblioteca, *Ordenar por → Fecha de añadido* (es el día que entró en vuestra lista).

## 7 · La tele y el móvil

- **Tele**: instala la app **Jellyfin** desde su tienda. Encontrará el ordenador sola; si no, escribe `http://<IP-del-ordenador>:8096`. Entra con tu usuario.
- **Móvil**: app de Jellyfin para ver, y el panel de StreamReady (`http://<IP-del-ordenador>:8765`) para la lista, las sugerencias y los ajustes. En el iPhone: Compartir → *Añadir a pantalla de inicio*.
- **Fuera de casa** (opcional): [Tailscale](https://tailscale.com/) en el ordenador y en el móvil, con la misma cuenta.

## 8 · Actualizar

Instala la versión nueva **encima**, sin desinstalar: se conserva todo. Después, en `chrome://extensions`, pulsa **↻** en StreamReady para que Chrome cargue su versión nueva.

## Problemas frecuentes

| Qué pasa | Qué hacer |
|---|---|
| La tele o el móvil no encuentran el ordenador | Red en **Privada** (paso 2). Si usáis una VPN en ese ordenador, que permita las conexiones de la red local |
| La extensión dice «StreamReady no responde» | Que el ordenador tenga StreamReady en marcha: `http://localhost:8765` tiene que abrir |
| La extensión dice «la página no traía datos» | Sesión cerrada en Netflix o Prime, o Netflix está preguntando «¿Quién está viendo?»: entra una vez a mano |
| Algo de vuestra lista sale «Sin identificar» | Avisad con el título: es un nombre que TMDB no reconoce bien |
| En Jellyfin todo tiene la misma fecha de añadido | Revisa el ajuste del paso 1.3 y borra la carpeta `C:\ProgramData\StreamReady\Plataformas` (se vuelve a crear) |

## Otra plataforma (HBO Max, Disney+, Filmin…)

- **Saber en cuál está cada cosa** ya funciona con cualquier plataforma: márcala en *Ajustes → Plataformas*.
- **Leer vuestra lista e historial** necesita un lector para esa plataforma. Para prepararlo: en su web, con la sesión iniciada, abre la extensión → *Otras plataformas y herramientas* → **Capturar esta web**. Chrome pedirá permiso **solo para esa web**. Recarga, pulsa *Cargar todo* y *Guardar captura* en las páginas de lista, «seguir viendo» e historial, y envía esos ficheros a quien mantiene StreamReady. Llevan datos vuestros: compártelos solo si estáis de acuerdo. El permiso se quita desde el mismo sitio.

---

Los datos de películas, series y plataformas proceden de [TMDB](https://www.themoviedb.org/) y [JustWatch](https://www.justwatch.com/). StreamReady usa la API de TMDB pero no está respaldado ni certificado por TMDB.
