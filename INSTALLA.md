# Installare /learn — il corso per costruire il tuo agente cognitivo

`/learn` è una skill per **Claude Code**. Insegna a chi la lancia a costruirsi, da una macchina
vuota, un agente cognitivo completo: identità (CLAUDE.md), memoria, brain, voce, formati di
scrittura, e 5 skill (`/ricorda`, `/scrivi`, `/decode`, `/sogna`, `/backup`).

## Prerequisito
Claude Code installato e funzionante: https://claude.com/claude-code

---

## Il modo più veloce (consigliato): fattelo installare

Non devi smanettare. Apri Claude Code, **dagli questo zip** e scrivi:

> installa questa skill

- **App desktop (Mac/Windows):** trascina lo zip nella finestra di Claude Code, poi scrivi `installa questa skill`.
- **Terminale (CLI):** scrivi `installa la skill che trovi in <percorso-dello-zip>`.

Claude scompatta, copia `learn/` nella cartella giusta e ti dice quando è pronto.
**Poi chiudi e riapri Claude Code** (le skill si attivano al riavvio) e digita:

```
/learn
```

---

## ISTRUZIONI PER CLAUDE (se ti hanno dato questo zip e ti chiedono di installarlo)

Sei tu a fare il lavoro — l'utente non apre terminali. Esegui:

1. Scompatta lo zip in una cartella temporanea. Dentro c'è una cartella `learn/` con `SKILL.md`.
2. Crea la cartella skill se non esiste e copiala:
   - macOS / Linux: `mkdir -p ~/.claude/skills && cp -R <tmp>/learn ~/.claude/skills/learn`
   - Windows (PowerShell): `mkdir $HOME\.claude\skills -Force; Copy-Item -Recurse <tmp>\learn $HOME\.claude\skills\learn`
3. Verifica che esista `~/.claude/skills/learn/SKILL.md`.
4. Di' all'utente: **"Fatto. Chiudi e riapri Claude Code, poi scrivi `/learn`."** (le skill caricano all'avvio).

---

## Installazione manuale (per chi mastica il terminale)

```bash
# macOS / Linux
mkdir -p ~/.claude/skills
cp -R learn ~/.claude/skills/learn
```
```powershell
# Windows (PowerShell)
mkdir $HOME\.claude\skills -Force
Copy-Item -Recurse learn $HOME\.claude\skills\learn
```
Riapri Claude Code e digita `/learn`.

---

## Come funziona

- Parte chiedendoti nome, dominio, lingua: cuce tutti gli esempi su di te.
- Procede UNO stage alla volta (0 → 10). Quando sei pronto a proseguire, scrivi `next`.
- Puoi fermarti e riprendere quando vuoi: `/learn 6` salta allo stage 6.
- `/learn map` mostra la mappa del corso. `/learn handout` ti genera una guida da tenere (`~/learn-handout.md`).

A fine corso avrai, tuoi e sulla tua macchina, tutti i file dell'agente più le 5 skill.

## Cosa NON serve
Niente git, niente terminale: parli all'agente, fa lui. Questa skill basta a sé stessa.
