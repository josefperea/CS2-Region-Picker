# How it works / Cómo funciona

## English
1. Valve publishes the list of its Steam Datagram Relay (SDR) points of presence for CS2 at
   `https://api.steampowered.com/ISteamApps/GetSDRConfig/v1?appid=730`: each region has a name, coordinates and relay IPs.
2. You choose which regions you want. The program creates **Windows Firewall** rules named `CS2-Region-Picker`
   (inbound + outbound, block) for the relay IPs of every region you did *not* choose, using `netsh advfirewall`.
3. With those relays unreachable, matchmaking can only pick servers in your allowed regions.
4. Rules live in Windows Firewall, so they **persist after closing the program and after rebooting**.
5. On every start the program downloads the list again and, if the IPs of your regions changed, silently re-applies the rules.

What it does **not** do: it does not read or modify the game, its memory or its files, does not inject anything and
does not run while you play. It only edits firewall rules and reads a public web API. Even so, use it at your own risk.

## Español
1. Valve publica la lista de puntos de presencia de su Steam Datagram Relay (SDR) para CS2 en la URL de arriba:
   cada región trae nombre, coordenadas e IPs de relays.
2. Tú eliges las regiones. El programa crea reglas del **Firewall de Windows** llamadas `CS2-Region-Picker`
   (entrada y salida, bloquear) para las IPs de todas las regiones que *no* elegiste, con `netsh advfirewall`.
3. Sin acceso a esos relays, el matchmaking solo puede escoger servidores de tus regiones permitidas.
4. Las reglas viven en el Firewall de Windows, así que **siguen activas al cerrar el programa y al reiniciar el PC**.
5. En cada inicio vuelve a descargar la lista y, si cambiaron las IPs de tus regiones, reaplica las reglas en silencio.

Lo que **no** hace: no lee ni modifica el juego, su memoria ni sus archivos, no inyecta nada y no corre mientras juegas.
Solo edita reglas del firewall y lee una API web pública. Aun así, úsalo bajo tu propia responsabilidad.


`CS2RegionPicker-data\` next to the exe (or `%APPDATA%\cs2region` if the folder is read-only; override with env var `CS2REGION_DATA`):
`settings.json` (language, location) and `state-<PC>.json` (selection, per computer).

## Remove everything / Quitar todo
Button **Remove all blocks**, or manually: `netsh advfirewall firewall delete rule name=CS2-Region-Picker` (admin).
