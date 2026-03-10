# EngramClaw 🧠

[![Skill para OpenClaw](https://img.shields.io/badge/OpenClaw-Skill-blue)](https://github.com/gentleman-programming/openclaw)
[![Engram](https://img.shields.io/badge/Engram-MCP-green)](https://github.com/Gentleman-Programming/engram)

Skill de OpenClaw que integra **Engram** - sistema de memoria persistente para agentes IA.

## ¿Qué hace?

Permite que los agentes recuerden entre sesiones:
- Bugfixes y cómo se resolvieron
- Decisiones de arquitectura
- Patrones descubiertos y gotchas
- Configuraciones importantes

## Instalación

```bash
# 1. Instalar Engram
brew install gentleman-programming/tap/engram

# 2. Registrar en MCPorter
mcporter config add engram --stdio "engram mcp"

# 3. Verificar
mcporter list engram
```

## Quick Start

```bash
# Inicio de sesión - recuperar contexto
mcporter call engram.mem_context project="mi-proyecto"

# Guardar un bugfix
mcporter call engram.mem_save \
  title="Query N+1 corregido" \
  type="bugfix" \
  project="mi-proyecto" \
  content='**Qué**: Agregué eager loading
**Por qué**: Performance degradado con 100+ registros
**Dónde**: src/services/users.ts
**Aprendido**: ORM requiere Preload() explícito'

# Buscar en memoria
mcporter call engram.mem_search query="auth"

# Fin de sesión - guardar resumen
mcporter call engram.mem_session_summary \
  project="mi-proyecto" \
  content='## Objetivo
Implementar autenticación JWT
...'
```

## Características

| Característica | Descripción |
|----------------|-------------|
| **Memoria curada** | El agente decide qué guardar, no captura automática |
| **Revelación progresiva** | Search → Timeline → Full content (eficiente en tokens) |
| **Búsqueda FTS5** | Full-text search en SQLite |
| **13 herramientas MCP** | CRUD + session lifecycle + stats |
| **Integración OpenClaw** | Complementa MEMORY.md y memory/YYYY-MM-DD.md |

## Cuándo Usar

| Disparador | Herramienta |
|------------|-------------|
| Inicio de sesión | `mem_context` |
| Después de bugfix/decisión | `mem_save` |
| Usuario dice "recuerda" | `mem_search` |
| Fin de sesión | `mem_session_summary` |

## Estructura

```
EngramClaw/
├── SKILL.md          # Instrucciones completas del skill
├── references/
│   └── tools.md      # Referencia de las 13 herramientas MCP
└── README.md         # Este archivo
```

## Documentación

- **[SKILL.md](./SKILL.md)** - Guía completa: protocolo de memoria, anti-patrones, troubleshooting
- **[references/tools.md](./references/tools.md)** - Referencia de todas las herramientas MCP

## Ecosistema OpenClaw

```
MEMORY.md (estático) → memory/YYYY-MM-DD.md (diario) → Engram (técnico) → self-improving (comportamiento)
```

| Tipo de info | Dónde guardar |
|--------------|---------------|
| Info permanente del usuario | MEMORY.md |
| Notas del día | memory/YYYY-MM-DD.md |
| Bugfix técnico | Engram |
| Correcciones de comportamiento | self-improving |

## Licencia

MIT

## Links

- [Engram](https://github.com/Gentleman-Programming/engram) - Backend de memoria
- [OpenClaw](https://github.com/gentleman-programming/openclaw) - Framework de agentes
