# mods_server_mine

Mods del servidor de Marcorp. Este repo existe para que todos los jugadores tengan
**exactamente la misma carpeta `mods`** y puedan actualizarla con `git pull`, sin
andar bajando `.jar` uno por uno.

| | |
|---|---|
| Minecraft | 1.20.1 |
| Mod loader | Fabric |
| Java | 17 |
| Contenido | 52 mods (`.jar`) + 2 configs de Glore (`glore_blocks.json`, `glore_brightness.json`) |

> Los mods de librería (Fabric API, Cloth Config, GeckoLib, Architectury, owo-lib,
> etc.) también están incluidos. No los borres: otros mods dependen de ellos.

## Instalación

La idea es que **el contenido del repo quede directamente dentro de la carpeta
`mods`**, no en una subcarpeta. Para eso se clona con un punto (`.`) al final.

### 1. Abrir la carpeta `mods`

| Sistema | Ruta |
|---|---|
| Windows | `%appdata%\.minecraft\mods` |
| Linux | `~/.minecraft/mods` |
| macOS | `~/Library/Application Support/minecraft/mods` |

En Windows, desde PowerShell o CMD:

```powershell
cd "$env:appdata\.minecraft\mods"
```

### 2. Clonar dentro de esa carpeta

```bash
git clone https://github.com/Navarro-Franco/mods_server_mine.git .
```

El **punto del final no es opcional**. Sin él, git crea
`mods/mods_server_mine/...` y Minecraft no lee mods en subcarpetas: el juego
arrancaría como si no hubiera instalado nada.

Así tiene que quedar:

```
.minecraft/mods/
├── .git/
├── fabric-api-0.92.12+1.20.1.jar
├── create-fabric-6.0.8.1+build.1744-mc1.20.1.jar
├── README.md
└── ...
```

La carpeta `.git` puede quedarse ahí sin problema; Minecraft la ignora.

Si solo vas a jugar y no te interesa el historial, podés bajar menos datos:

```bash
git clone --depth 1 https://github.com/Navarro-Franco/mods_server_mine.git .
```

### ¿La carpeta `mods` ya tiene cosas?

Si no está vacía, apartá lo que había antes de clonar. Si no, quedan dos versiones
del mismo mod y el juego crashea al arrancar:

```powershell
cd "$env:appdata\.minecraft"
Rename-Item mods mods_viejos
New-Item -ItemType Directory mods
cd mods
git clone https://github.com/Navarro-Franco/mods_server_mine.git .
```

Cuando confirmes que todo anda, borrá `mods_viejos`. Lo mismo aplica a la carpeta
`mods` del servidor.

## Actualizar

Cerrá el juego y ejecutá:

```bash
cd "$env:appdata\.minecraft\mods"
git pull
```

`git pull` agrega los mods nuevos y **elimina los que se hayan sacado del repo**,
así que después de actualizar la carpeta queda igual a la del resto.

## Servidor

La carpeta `mods` del servidor se instala igual que la del cliente: se clona con
el punto dentro de `mods`. Algunos mods son principalmente de cliente (Sodium,
Indium, JourneyMap, LambDynamicLights, ModMenu, Jade, ObsidianUI, More Hitboxes).
Fabric ignora en el servidor los mods marcados como client-only, así que dejarlos
no rompe nada; si querés una carpeta más limpia, podés quitarlos solo del servidor.

## Contribuir

Las reglas para mandar cambios están en [CONTRIBUTING.md](CONTRIBUTING.md).
Resumen: una rama por cambio, PR chico, compatible con 1.20.1 + Fabric y probado
antes de pedir review.

## Licencia

El contenido propio de este repo está bajo GPLv3 (ver [LICENSE](LICENSE)). Cada
mod conserva la licencia de su autor; este repo solo los distribuye para uso
privado del servidor.
