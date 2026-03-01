# Cole Medin - AI Layer Templates

Hämtat från: https://github.com/coleam00/link-in-bio-page-builder/tree/main/.claude

Baserat på videon: "My COMPLETE Agentic Coding Workflow to Build Anything"
https://youtu.be/goOZSXmrYQ4

## Innehåll

### .claude/commands/
| Fil | Användning |
|-----|-----------|
| `prime.md` | `/prime` - Kör i början av VARJE session. Läser PRD, CLAUDE.md, git log |
| `create-prd.md` | `/create-prd` - Skapar strukturerad PRD från konversation |
| `create-rules.md` | `/create-rules` - Genererar CLAUDE.md med regler för projektet |
| `plan-feature.md` | `/plan-feature` - PIV-loop steg 1: Planerar feature, sparar i `.agents/plans/` |
| `execute.md` | `/execute` - PIV-loop steg 2: Implementerar från plan-fil |
| `commit.md` | `/commit` - Standardiserade commit-meddelanden |
| `init-project.md` | `/init-project` - Initierar nytt projekt |

### .claude/
| Fil | Användning |
|-----|-----------|
| `CLAUDE-template.md` | Mall för CLAUDE.md i nya projekt |
| `PRD-example.md` | Exempel på färdig PRD |

## PIV-loop Workflow

```
1. /prime          → Förstå kodbas + rekommendera nästa fas från PRD
2. Vibe planning   → Diskutera feature informellt
3. /plan-feature   → Skapa strukturerad plan med tasks + validering
4. [Ny session]
5. /execute [plan] → Implementera (delegera allt till agenten)
6. Human validate  → Granska + manuell test
7. /commit         → Commit med standardiserat meddelande
```

## Hur man använder

Kopiera `.claude/`-mappen till ditt projekt och anpassa efter behov.
Kom ihåg: **Context is precious** - starta ny session mellan plan och execute.
