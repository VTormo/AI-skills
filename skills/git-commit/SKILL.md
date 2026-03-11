---
name: git-commit
description: Estandariza mensajes de commit en español con formato tipo(scope): resumen. Activar cuando el usuario pida crear, corregir o validar un commit, describa cambios de código, comparta un diff o diga "qué commit hago para esto".
---

# Git Commit Standard

## Formato

```
<tipo>(<scope>): <resumen>
```
Con ticket: `PROJ-104 feat(auth): ...` o `fix(api): ... (#42)`  
Con cuerpo (solo si hay cambios secundarios reales):
```
<tipo>(<scope>): <resumen>

- <cambio secundario>
- Por qué: <motivo si no es obvio>
```
Breaking change: `<tipo>(<scope>)!: <resumen>` + `BREAKING CHANGE: <qué se rompe>`

## Tipos
`feat` `fix` `refactor` `perf` `docs` `test` `chore` `style` `revert` `security`
- `refactor` → cambia código de producto · `chore` → herramientas, config, deps

## Scopes
Usar el nombre de la feature activa si el usuario la menciona. Si no:  
`api` `handlers` `service` `domain` `auth` `middleware` `db` `migrations` `repo` `cache` `queue` `config` `logging` `metrics` `events` `ui` `components` `pages` `router` `state` `hooks` `ci` `cd` `docker` `deps` `build` `docs` `security` `utils`

## Reglas del resumen
- Imperativo, español, sin punto final, ≤ 72 caracteres
- Nada vago: no `update`, `fix`, `cambios`, `wip`
- No terminar en participio: `añadido`, `arreglado` → `añadir`, `arreglar`

## Flujo de ejecución

**Por defecto: leer, decidir, ejecutar. Sin pedir confirmación.**

1. Leer contexto con `git diff --staged` o `git status` (un solo comando)
2. Generar el commit más preciso posible
3. Ejecutar `git commit -m "..."`
4. Ejecutar `git push origin <rama>` inmediatamente

**Pausar solo en estos 2 casos:**
| Caso | Acción |
|------|--------|
| Rama es `main` o `master` | Preguntar: ¿push aquí o crear rama? |
| Usuario pidió "proponer" o "redactar" (no ejecutar) | Solo mostrar el mensaje |

**Nunca pausar para**: confirmar el mensaje, pedir scope, preguntar si hacer push en rama de feature.

### Ramas (solo si el usuario elige crear una desde main)
Formato: `<tipo>/<scope>-<slug>` · ej: `fix/auth-token-expiracion`  
Con ticket: `PROJ-104/feat/billing-impuestos`

## Ejemplos
```
feat(api): añadir endpoint para listar plantillas de comando
fix(db): corregir FK grants_access_level_id en command_templates
refactor(command-templates): extraer parseo de respuestas a paquete dtmf

- Mover ResponseParser de service/ a internal/dtmf/
- Actualizar imports en handlers/command_handler.go
- Por qué: el parser crecía acoplado al servicio sin reutilización

feat(api)!: cambiar contrato de /command-templates a paginación

BREAKING CHANGE: requiere page y page_size. Actualizar clientes REST.
```
