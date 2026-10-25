# Reglas para Pull Requests

Este repo es la lista oficial de mods del servidor. Un cambio acá le llega a todos
los jugadores, así que los PR tienen que ser chicos, probados y fáciles de revisar.

## Flujo de trabajo

```bash
git switch main
git pull
git switch -c feat/agregar-nombre-del-mod

# agregar, actualizar o borrar los .jar

git add -A
git commit -m "feat: agregar <mod> <version>"
git push -u origin feat/agregar-nombre-del-mod
```

Después abrí el Pull Request en GitHub contra `main`.

## Reglas

1. **Un PR, un tema.** No mezcles "agregar un mod" con "actualizar otro" ni con
   cambios de documentación. Si son cosas distintas, son PRs distintos.
2. **Rama nueva desde `main` actualizado.** Nombres: `feat/...`, `fix/...`,
   `chore/...`, `docs/...`. No pushees directo a `main`.
3. **Compatibilidad obligatoria:** Minecraft **1.20.1** y **Fabric**. Nada de
   Forge ni NeoForge.
4. **Sin duplicados ni versiones viejas.** Al actualizar un mod, borrá el `.jar`
   anterior en el mismo commit (`git rm` del viejo + `git add` del nuevo). Nunca
   dejes dos versiones del mismo mod en la carpeta.
5. **No renombres los archivos.** Dejá el nombre original que publica el autor.
6. **Incluí las dependencias.** Si el mod necesita una librería que no está en el
   repo, agregala en el mismo PR. Si ya está, no la dupliques: verificá que la
   versión sea compatible con 1.20.1.
7. **Avisá si es de cliente o de servidor.** Si el mod es client-only (o tiene
   partes que solo funcionan en un lado), decilo en la descripción del PR.
8. **Nada de archivos que no van:**
   - mundos, `logs`, `crash-reports`, `options.txt`, configs de jugador;
   - credenciales, tokens o claves;
   - ningún archivo de más de **100 MB** (límite de GitHub). El repo completo
     debería quedar por debajo de 1 GB.
9. **Probado antes de pedir review.** Arrancá el cliente con la carpeta completa
   y, si el cambio afecta al servidor, probá también el servidor. Sin crash y con
   el `latest.log` limpio.
10. **Commits claros**, en español y con prefijo:

    ```
    feat: agregar <mod> <version>
    chore: actualizar <mod> de <version-vieja> a <version-nueva>
    fix: quitar <mod> (crash al arrancar)
    docs: corregir instrucciones de instalación
    ```
11. **No toques `LICENSE`** ni cambies la estructura: todos los `.jar` van en la
    raíz del repo.
12. **Un maintainer revisa y mergea.** No hagas self-merge. Después del merge,
    borrá la rama y actualizá tu `main` con `git pull`.
13. **Si tu PR quedó viejo**, hacé rebase sobre `main` (`git rebase main`), no
    merges `main` dentro de tu rama.

## Plantilla para la descripción del PR

```markdown
## Qué cambia
- Agrega / actualiza / elimina: <nombre del mod>

| Campo | Valor |
|---|---|
| Mod | <nombre> |
| Versión | <version> |
| Link oficial | <Modrinth / CurseForge / GitHub> |
| Licencia | <licencia> |
| Lado | Cliente / Servidor / Ambos |
| Dependencias nuevas | <ninguna / lista> |

## Por qué
<motivo del cambio>

## Cómo lo probé
- [ ] Cliente 1.20.1 + Fabric con la carpeta completa
- [ ] Servidor con la carpeta completa (si aplica)
- [ ] Sin crash y sin errores nuevos en `latest.log`
```

## Mods pesados o conflictivos

Si el mod es grande (más de ~20 MB), cambia el rendimiento del servidor o puede
chocar con otro mod de la lista, abrí primero un **issue** para discutirlo antes
de mandar el PR.
