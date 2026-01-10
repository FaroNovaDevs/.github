# Certainty-mvp Organization Workflows

Este repositorio contiene workflows reusables para todos los repos de la organización Certainty-mvp.

## Workflows Disponibles

### `update-docs.yml` - Actualización Automática de Documentación

Este workflow usa Claude Code Action para actualizar automáticamente la documentación del proyecto basándose en los commits nuevos.

#### Características

- Trackea qué commits ya fueron procesados (no repite trabajo)
- Actualiza README.md, CHANGELOG.md y carpeta /docs
- Agrupa cambios por tipo en el changelog
- Solo actualiza si hay cambios significativos

#### Cómo usarlo en tu repo

1. Crea el archivo `.github/workflows/docs.yml` en tu repositorio:

```yaml
name: Update Documentation
on:
  push:
    branches: [main]

jobs:
  update-docs:
    uses: Certainty-mvp/.github/.github/workflows/update-docs.yml@main
    secrets: inherit
```

2. (Opcional) Personaliza qué documentación actualizar:

```yaml
name: Update Documentation
on:
  push:
    branches: [main]

jobs:
  update-docs:
    uses: Certainty-mvp/.github/.github/workflows/update-docs.yml@main
    with:
      docs_folder: 'documentation'  # default: 'docs'
      update_readme: true           # default: true
      update_changelog: true        # default: true
      update_docs_folder: false     # default: true
    secrets: inherit
```

#### Sistema de Tracking

El workflow crea/actualiza un archivo `.github/docs-tracker.json` en tu repo:

```json
{
  "last_processed_commit": "abc123...",
  "last_update": "2025-01-09T12:00:00Z",
  "commits_processed": 5
}
```

Esto permite que Claude sepa exactamente qué commits ya fueron documentados y cuáles son nuevos.

## Requisitos

- El secret `CLAUDE_CODE_OAUTH_TOKEN` debe estar configurado a nivel de organización (ya está configurado)

## Soporte

Para issues o mejoras, abre un issue en este repositorio.
