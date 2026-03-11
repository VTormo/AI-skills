# AI-skills

Colección de skills para Claude. Cada skill define comportamiento especializado que el agente activa automáticamente según el contexto.

## Estructura

```
skills/
└── git-commit/
    └── SKILL.md
```

## Skills disponibles

| Skill | Descripción |
|-------|-------------|
| [git-commit](./git-commit/SKILL.md) | Genera y ejecuta commits en español con formato estándar `tipo(scope): resumen` |

## Cómo añadir una skill

1. Crear carpeta con el nombre de la skill en `skills/`
2. Añadir `SKILL.md` con frontmatter `name` y `description`
3. Registrarla en la tabla de este README
