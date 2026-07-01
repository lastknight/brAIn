---
name: learn
description: "Corso guidato autoconsistente: porta lo studente da un Claude Code vuoto al SUO agente cognitivo COMPLETO — identità (CLAUDE.md), memoria, brain (conoscenza canonica), tono/voce (da campioni da copiare), formati di scrittura, skill, preferenze, un sistema /decode per imparare, e auto-manutenzione. Tutti gli esempi sono dentro la skill: zero dipendenze da altri file o skill. Costruisce l'agente DELLO STUDENTE, sulla SUA macchina. Output: lezione interattiva + handout. Triggera su: '/learn', 'corso', 'insegnami a costruire un agente', 'parti da zero', 'onboarding'."
user-invocable: true
argument-hint: "[stage 0-10 | next | map | handout] — vuoto = profilo + mappa + Stage 0"
disable-model-invocation: false
category: EDUCATION
---

# /learn — Costruisci il TUO agente cognitivo da zero

Corso interattivo completo. Porta chi lo lancia da un Claude Code appena installato a un **agente cognitivo proprio**: identità, memoria, conoscenza, voce, capacità di scrittura, skill, e un sistema per imparare e mantenersi da solo.

> **IMPORTANTE — questa skill è l'unica cosa che lo studente ha.** Macchina vuota, nessun altro file, nessuna altra skill. Quindi:
> - **NON aprire file di sistema preesistenti** come reference: sulla macchina dello studente non esistono. Ogni esempio è **dentro questa skill**. Mostri quelli.
> - **Tutto ciò che si costruisce è dell'utente.** Mai "il sistema di Matteo Flora". Si costruisce il SUO, coi SUOI dati, nel SUO dominio.
> - **Non assumere cartelle esistenti.** Prima di scrivere in una dir, `mkdir -p`.
> - **Lo studente NON è uno smanettone: non apre terminali, non scrive file a mano.** Sei TU a eseguire — crei le cartelle, scrivi i file, lanci i comandi sulla sua macchina. Lui guarda, capisce, conferma con `next`. Quando uno stage mostra un comando o un file, è ciò che **fai tu per lui**: diglielo così ("questo lo creo io, tu guarda"), mai "adesso digita...".

---

## Avvio — raccogli il profilo (una volta sola)

Alla prima invocazione, prima della Mappa, chiedi in una riga:
> "Per cucirti tutto addosso: come ti chiami, di cosa ti occupi, in che lingua vuoi l'agente, e che tipo di cose scrivi di solito (email, pareri, post, codice...)?"

Salva `NOME`, `DOMINIO`, `LINGUA`, `COSA_SCRIVE` e **sostituiscili in ogni snippet**: gli esempi devono già contenere i suoi dati, non segnaposto. Se non risponde: `[Nome]`, dominio generico, italiano.

---

## Dispatcher

- **vuoto** → raccogli profilo → stampa **Mappa** → entra in **Stage 0**.
- **`map`** → solo la Mappa. **`next`** → stage successivo. **`0`..`10`** → quello stage.
- **`handout`** → genera il materiale (vedi *Handout*).

Lezione DAL VIVO: **uno stage alla volta**, poi ti fermi e aspetti `next`. Mai dumpare tutto.

---

## Il pattern di ogni stage — MOSTRA → SPIEGA → COSTRUISCI → VERIFICA

1. **🎬 MOSTRA** — incolla l'**esempio canonico** dello stage (è scritto qui dentro), già coi dati dello studente. NON leggere file esterni.
2. **💡 SPIEGA** — il principio, il *perché*, 2-3 frasi.
3. **🛠️ COSTRUISCI** — TU crei il file / lanci il comando sulla sua macchina (non lui a mano). Gli mostri cosa stai creando e perché, in una riga.
4. **✅ VERIFICA** — come controlla che funziona.

Diretto, concreto. Una battuta sì, il pippone no.

---

## Mappa del corso

```
DA ZERO  →  IL TUO AGENTE COGNITIVO COMPLETO

Tre layer: IDENTITÀ (chi è) · CAPACITÀ (cosa fa) · MEMORIA & APPRENDIMENTO (come impara).
Gli stage si fanno IN ORDINE, 0 → 10. Il [layer] è solo la lente per capire a cosa serve ognuno.

  Stage 0  · Setup & modello mentale     [identità]   i 3 layer, "non è una chat, è una protesi"
  Stage 1  · CLAUDE.md                   [identità]   la TUA identità che sovrascrive i default
  Stage 2  · Memoria + /ricorda          [memoria]    un fatto = un file + scorciatoia salva-al-volo
  Stage 3  · Brain                       [identità]   la TUA conoscenza canonica (moduli + INDEX)
  Stage 4  · Tono & voce                 [identità]   la TUA voce, distillata da campioni che ami
  Stage 5  · Formati di scrittura        [capacità]   i TUOI template di output riusabili
  Stage 6  · Skill /scrivi               [capacità]   lega voce + formati + brain → produce  ← il picco
  Stage 7  · Preferenze & feedback loop  [memoria]    impara come lavori
  Stage 8  · /decode                     [memoria]    impara da fonti esterne (documenti, appunti)
  Stage 9  · /sogna                      [memoria]    impara dalle TUE sessioni passate (con registro)
  Stage 10 · /backup & manutenzione      [memoria]    copie zip datate + l'abitudine di consolidare

  → /learn handout
```

I tre modi di imparare: **/ricorda** (manuale, al volo) · **/decode** (da fonti esterne) · **/sogna** (introspettivo, dalle conversazioni già fatte).

Promessa: a fine corso, tuoi, hai identità + memoria + brain + voce + formati + una skill che scrive nella tua voce + tre modi di imparare + copie di sicurezza.

---

## Stage 0 — Setup & modello mentale

**💥 SENTI IL PROBLEMA (1 minuto, prima di costruire qualsiasi cosa)** — fagli fare questo esperimento: in una sessione nuova digli un fatto su di sé ("mi chiamo Anna, faccio l'avvocata civilista"). Poi chiude tutto e riapre Claude Code. Riapre e chiede: *"cosa sai di me?"*. Non sa niente. **Quello è il buco.** Un assistente generico riparte da zero a ogni sessione: nessuna memoria, nessuna voce, nessuna competenza tua. Tutto il corso serve a riempire quel buco — dargli uno **stato su disco** che si ricarica ogni volta. Non costruiamo una chat più carina: costruiamo la memoria che gli manca.

> **Come lavoriamo da qui in poi:** tu non apri terminali e non scrivi file a mano. Quando serve creare una cartella o un file, **lo faccio io** sulla tua macchina e ti mostro cosa sto facendo e perché. Tu guardi, capisci, e quando funziona scrivi `next`.

**🎬 MOSTRA** — la struttura completa che costruiremo:
```
~/.claude/
├── CLAUDE.md          ← chi è (Stage 1)
├── brain/             ← cosa sa, conoscenza canonica (Stage 3)
│   └── INDEX.md
├── styles/            ← come parla, la voce (Stage 4)
├── memory/            ← cosa ricorda, fatti (Stage 2)
│   ├── MEMORY.md
│   └── .sogna-fatte.md  ← registro sessioni già consolidate (Stage 9)
├── skills/            ← cosa fa
│   ├── scrivi/        ← produce nella tua voce (Stage 6)
│   ├── ricorda/       ← salva un fatto al volo (Stage 2)
│   ├── decode/        ← impara da fonti esterne (Stage 8)
│   ├── sogna/         ← impara dalle sessioni passate (Stage 9)
│   └── backup/        ← fa copie zip datate (Stage 10)
└── (~/claude-backups/ ← le copie, fuori da qui)
```

**💡 SPIEGA** — un assistente generico dimentica a fine sessione. Un *agente cognitivo* ha **stato su disco** ricaricato ogni volta, tutto in testo leggibile. Tre layer:
- **Identità** (chi è) → CLAUDE.md + brain + voce
- **Capacità** (cosa fa) → skill + formati
- **Memoria & apprendimento** (come ricorda e impara) → memory + preferenze + i tre modi di imparare (ricorda / decode / sogna)

Distinzione chiave da subito: **memoria** = fatti episodici ("Anna ha una causa il 12/07"). **Brain** = sapere stabile ("come si struttura un parere legale"). Due cose diverse, due cartelle diverse.

**🛠️ COSTRUISCI**:
```
# installa: https://claude.com/claude-code
mkdir -p ~/.claude/{brain,styles,memory,skills}
```

**✅ VERIFICA** — `ls ~/.claude` mostra le cartelle.

---

## Stage 1 — CLAUDE.md, la TUA identità

**🎬 MOSTRA** — esempio con NOME=Anna, DOMINIO=avvocata:
```markdown
# Chi sono
Sono l'agente di Anna, avvocata civilista. Mi parli in italiano.

# Come lavori
1. Diretto, niente preamboli. Prima frase = la risposta.
2. Se citi una norma o una sentenza, linka la fonte. Mai inventarle.

# Dove guardare
- Conoscenza stabile: ~/.claude/brain/ (vedi INDEX.md)
- La mia voce: ~/.claude/styles/
- Cosa ricordi: ~/.claude/memory/MEMORY.md
```

**💡 SPIEGA** — `CLAUDE.md` è caricato in testa a OGNI sessione: il contratto su chi è l'agente e cosa non deve mai fare. Le righe "Dove guardare" insegnano all'agente la mappa del proprio cervello: gli altri layer si agganciano qui.

**🛠️ COSTRUISCI** — `~/.claude/CLAUDE.md` coi suoi dati e 2-3 regole vere. Poche regole rispettate > venti ignorate.

**✅ VERIFICA** — nuova sessione, "chi sei e dove tieni la tua conoscenza?": risponde col file.

---

## Stage 2 — Memoria: un fatto, un file

**🎬 MOSTRA** — l'indice e un fatto (inline):

`~/.claude/memory/MEMORY.md`:
```markdown
# Memoria
- [Tono diretto](feedback-tono-diretto.md) — niente preamboli
- [Causa Rossi](project-causa-rossi.md) — udienza 12/07, attesa CTU
```
`~/.claude/memory/feedback-tono-diretto.md`:
```markdown
---
name: feedback-tono-diretto
description: Preferisco risposte dirette senza preamboli
metadata:
  type: feedback
---
Vai dritto al punto, niente "Certo!".
**Why:** coi preamboli perdo il filo.
**How to apply:** prima frase = la risposta.
```

**💡 SPIEGA** — **un fatto = un file**. Tipi: `user`, `feedback`, `project`, `reference`. `MEMORY.md` è l'indice, l'unica cosa sempre caricata; i file singoli si recuperano alla bisogna. Granularità fine = correggi/cancelli un fatto senza toccare gli altri.

**🛠️ COSTRUISCI** — primo file in `memory/` + riga in `MEMORY.md`.

**✅ VERIFICA** — riga nell'indice, file con UN solo fatto.

### + Costruisci `/ricorda` (la scorciatoia)

Scrivere a mano frontmatter e indice ogni volta è una rottura. Diamo subito una skill che lo fa lei:
```markdown
---
name: ricorda
description: "Salva al volo un fatto in memoria. /ricorda <il fatto>."
user-invocable: true
argument-hint: "<il fatto da ricordare>"
model: claude-sonnet-4-6
effort: medium
---
# /ricorda
0. Se il modello attivo non è `claude-sonnet-4-6`, cambialo (`/model claude-sonnet-4-6`) e riparti — questa skill è ancorata a lì.
1. Scegli il tipo del fatto: user / feedback / project / reference.
2. Crea ~/.claude/memory/<tipo>-<slug>.md col frontmatter giusto e il fatto nel corpo.
3. Aggiungi una riga in ~/.claude/memory/MEMORY.md.
4. Conferma in una riga cosa hai salvato e dove.
```
```
mkdir -p ~/.claude/skills/ricorda
# crea ~/.claude/skills/ricorda/SKILL.md con l'esempio sopra
```

> **Nota didattica — scelta modello.** `/ricorda` gira sempre su **`claude-sonnet-4-6`** con **`effort: medium`**. Non l'alias generico `sonnet` (risolverebbe al Sonnet corrente = Sonnet 5), non un modello più grande. Motivo: `/ricorda` fa una cosa piccola e ripetibile — smistare UN fatto in UN file col frontmatter giusto. Un modello ancorato a una versione precisa produce lo stesso output oggi e fra sei mesi; se cambia il Sonnet di default sotto di te, il tuo agente comincia a scrivere in modo leggermente diverso senza che tu te ne accorga. **Regola generale del corso**: quando una skill fa lavoro meccanico e sensibile a stabilità (memoria, indici, registri), forzi il modello. Quando fa lavoro creativo (scrivere nella tua voce), lasci lo standard.

**✅ VERIFICA** — questa è la **prima skill** che creiamo: avvisalo che le skill nuove si attivano solo **riavviando Claude Code** (chiudi e riapri), altrimenti sembra che non esista. Dopo il riavvio: `/ricorda il cliente Bianchi preferisce essere chiamato di mattina` crea il file e la riga, senza che tu tocchi niente. Differenza con `/decode`: `/ricorda` è UN fatto a mano, `/decode` ingerisce una fonte intera.

---

## Stage 3 — Brain: la TUA conoscenza canonica

**🎬 MOSTRA** — un brain è una libreria di moduli tematici, con un indice che li auto-seleziona.

`~/.claude/brain/INDEX.md`:
```markdown
# Brain — conoscenza canonica
Prima di scrivere su un tema, leggi il modulo giusto.

| Modulo | Tema | Quando usarlo |
|--------|------|---------------|
| [responsabilita-civile](responsabilita-civile.md) | RC, danni | cause risarcimento |
| [voce-clienti](voce-clienti.md) | come parlo ai clienti | email, pareri |
```
`~/.claude/brain/responsabilita-civile.md` (un modulo = un sapere stabile):
```markdown
# Responsabilità civile — nozioni operative
- Art. 2043 c.c.: danno ingiusto, nesso causale, colpa/dolo.
- Onere della prova: [...]
- Errori tipici da evitare: [...]
```

**💡 SPIEGA** — differenza con la memoria: la memoria ricorda *fatti che capitano* (la causa di Rossi), il **brain sa cose che restano vere** (come funziona la RC). Le skill avranno la *procedura*, il brain ha il *sapere*. L'`INDEX.md` permette all'agente di pescare il modulo giusto da solo. È la tua competenza, scritta una volta, riusata sempre.

**🛠️ COSTRUISCI** — `~/.claude/brain/INDEX.md` + **un** modulo sul suo dominio (chiedigli il tema che padroneggia di più e scrivetelo insieme).

**✅ VERIFICA** — chiedi all'agente di usare quel sapere: deve citare il modulo, non improvvisare.

---

## Stage 4 — Tono & voce: distillala da campioni che ami

> Questo stage è **interattivo per davvero**: non inventare una voce, estraila da testi reali.

**🎬 MOSTRA** — la struttura di uno style file:
```markdown
# Voce — [nome stile]
## Come suona
[3-4 aggettivi: es. diretta, ironica, mai burocratica]
## Fai
- Frasi brevi. Verbi forti. Esempi concreti.
## Non fare
- Niente "si rende noto che". Niente latinismi inutili.
## Esempi (verbatim)
> "[frase reale presa dai campioni]"
```

**💡 SPIEGA + RACCOGLI** — chiedi allo studente:
> "Incollami 2-3 pezzi che catturano la voce che vuoi: cose tue che ti piacciono, o di un autore che ammiri."

Poi **analizza i campioni** ed estrai: lunghezza frasi, registro, parole ricorrenti, cosa NON fa mai, 2-3 citazioni verbatim. Da lì scrivi lo style file. La voce non si descrive a memoria, si **distilla da esempi reali** — è la differenza tra "scrivi simpatico" e una voce riproducibile.

**🛠️ COSTRUISCI** — `~/.claude/styles/<nome>.md` con la distillazione. E un puntatore allo stile attivo (es. una riga in CLAUDE.md: "Voce di default: styles/<nome>.md").

**✅ VERIFICA** — fai scrivere all'agente due righe sul suo dominio: devono suonare come i campioni, non come un comunicato.

---

## Stage 5 — Formati di scrittura: i tuoi template di output

**🎬 MOSTRA** — un formato = una struttura d'uscita riusabile. Esempio (dominio legale):
```markdown
# Formato: email-cliente
Scopo: rispondere a un cliente in modo chiaro e rassicurante.
Struttura:
1. Apertura (1 riga, riconosci il problema)
2. Dove siamo (stato in 2-3 frasi, zero gergo)
3. Cosa farò io / cosa serve da te (lista)
4. Chiusura (prossimo contatto)
Lunghezza: < 200 parole. Voce: styles/<nome>.md.
```

**💡 SPIEGA** — un formato è il *contratto della struttura*: dice all'agente quali sezioni produrre e in che ordine, ogni volta. La voce è *come* suoni; il formato è *come è organizzato* l'output. Insieme = output consistente senza ripeterti i requisiti ogni volta. (Es. nel suo dominio: `email-cliente`, `parere`, `post-linkedin`, `commit-message`...).

**🛠️ COSTRUISCI** — `~/.claude/skills/scrivi/formats/` con 1-2 formati che lo studente usa davvero (parti da `COSA_SCRIVE`).

**✅ VERIFICA** — i file formato esistono. Li useremo subito nello stage 6.

---

## Stage 6 — Skill /scrivi: lega tutto

**🎬 MOSTRA** — la skill che orchestra voce + formati + brain:
```markdown
---
name: scrivi
description: "Scrivi un testo nella mia voce in un formato dato. /scrivi <formato> <argomento>."
user-invocable: true
argument-hint: "<formato> <argomento o note>"
---
# /scrivi
1. Leggi il formato richiesto in formats/<formato>.md.
2. Carica la voce in ~/.claude/styles/<nome>.md.
3. Se l'argomento tocca un tema del brain, leggi il modulo da ~/.claude/brain/INDEX.md.
4. Produci il testo seguendo la struttura del formato, nella voce, coi fatti del brain.
```

**💡 SPIEGA** — ecco il senso di tutto: una skill è una procedura riusabile (`/nome`) che **mette insieme i layer**. La conoscenza sta nel brain, la voce negli styles, la struttura nei formati; la skill è sottile e li orchestra. Cambi la voce in un posto, tutte le skill la usano.

**🛠️ COSTRUISCI**:
```
mkdir -p ~/.claude/skills/scrivi
# crea ~/.claude/skills/scrivi/SKILL.md con l'esempio sopra
```

**✅ VERIFICA** — nuova sessione, `/scrivi email-cliente aggiornamento sulla causa`: esce un testo nella sua voce, struttura del formato, fatti dal brain. **Questo è il momento "aha" del corso.**

---

## Stage 7 — Preferenze & feedback loop

**🎬 MOSTRA**:
```markdown
# Preferenze
## DO
- Rispondi in italiano, tono diretto.
- Quando scrivi, usa sempre la mia voce di default.
## DON'T
- Niente preamboli. Mai dati o fonti inventate.
```

**💡 SPIEGA** — rende l'agente **vivo**: non configuri una volta e basta. Quando ti corregge bene, tieni la regola; quando sbaglia, la correzione diventa una memoria `feedback`; le ricorrenti salgono in `preferences.md`. Loop di apprendimento su testo, correggibile a mano.

**🛠️ COSTRUISCI** — `~/.claude/memory/preferences.md` con 3 DO / 3 DON'T suoi. Abitudine: "quando mi correggi, dì 'ricordatelo' e lo salvo".

**✅ VERIFICA** — "quali sono le mie preferenze?": le cita.

---

## Stage 8 — /decode: il TUO motore per imparare

**🎬 MOSTRA** — una skill che ingerisce una fonte e ne ricava memoria o brain:
```markdown
---
name: decode
description: "Impara da una fonte (documento, appunti, articolo) e aggiorna memoria e brain. /decode <file o testo>."
user-invocable: true
argument-hint: "<path file | testo incollato>"
---
# /decode
1. Leggi la fonte.
2. Estrai TUTTO: fatti su persone/progetti, e sapere stabile.
3. Classifica ogni elemento:
   - fatto episodico (chi, quando, stato) → memory/  (un fatto = un file) + riga in MEMORY.md
   - sapere stabile/riusabile           → brain/ (modulo) + riga in brain/INDEX.md
4. REGOLA D'ORO: leggi il file esistente PRIMA di scrivere. MERGE, mai sovrascrivere.
5. Report: cosa ho imparato, dove l'ho messo, cosa va verificato.
```

**💡 SPIEGA** — è lo stesso movimento di questo corso, ma diventa una tua skill: dai una fonte, l'agente la *interiorizza* nel posto giusto. Il principio non negoziabile: **estrazione cieca e completa, poi classifica, poi MERGE** (legge prima, somma dopo, non cancella). Così l'agente cresce nel tempo invece di ripartire ogni volta da zero.

**🛠️ COSTRUISCI**:
```
mkdir -p ~/.claude/skills/decode
# crea ~/.claude/skills/decode/SKILL.md con l'esempio sopra
```

**✅ VERIFICA** — `/decode <un suo appunto reale>`: deve creare/aggiornare file in `memory/` e/o `brain/` e aggiornare gli indici. L'agente ha imparato qualcosa di nuovo, da solo.

---

## Stage 9 — /sogna: impara dalle TUE sessioni passate

**🎬 MOSTRA** — `/sogna` è `/decode` puntato sulle tue conversazioni già fatte, con un registro di quelle già lavorate:
```markdown
---
name: sogna
description: "Rivedi le conversazioni passate e distillane fatti e sapere in memoria e brain. /sogna."
user-invocable: true
argument-hint: ""
model: claude-sonnet-4-6
effort: medium
---
# /sogna
0. Se il modello attivo non è `claude-sonnet-4-6`, cambialo (`/model claude-sonnet-4-6`) e riparti.
1. Trova i log delle sessioni recenti di Claude Code (i file in ~/.claude/projects/.../*.jsonl).
2. Salta quelle già consolidate: leggi il registro ~/.claude/memory/.sogna-fatte.md.
3. Per ogni sessione NUOVA, come fa /decode:
   - estrai fatti episodici → memory/ (un fatto = un file) + riga in MEMORY.md
   - estrai sapere stabile  → brain/ (modulo) + riga in brain/INDEX.md
   - REGOLA D'ORO: leggi il file esistente PRIMA di scrivere. MERGE, mai sovrascrivere.
4. Segna le sessioni fatte in ~/.claude/memory/.sogna-fatte.md (così non le rifai).
5. Report: quante sessioni nuove, cosa ho imparato, dove l'ho messo.
```

**💡 SPIEGA** — stesso motore di `/decode`, fonte diversa: invece di un documento esterno, l'agente rilegge **se stesso** — le conversazioni che avete avuto — e ne salva quello che conta. Il **registro** (`.sogna-fatte.md`) è la chiave: tiene traccia di cosa è già stato digerito, così ogni volta lavora solo il nuovo e non duplica. È l'agente che impara mentre dorme: tu chiudi la giornata, lui consolida.

> **Nota didattica — scelta modello.** Come `/ricorda`, anche `/sogna` è ancorata a **`claude-sonnet-4-6`** con **`effort: medium`**. Non l'alias generico `sonnet`, non Opus. Motivo: `/sogna` fa lavoro sensibile a stabilità — legge sessioni e scrive in file di memoria e brain che si stratificano nel tempo. Se domani il Sonnet di default cambia, il tuo agente comincerebbe a distillare in modo leggermente diverso, e col passare dei mesi la tua memoria diventa una torta a strati con voci diverse. Ancorandola a 4.6 medium ottieni ripetibilità: rilanci lo stesso `/sogna` fra tre mesi e produce lo stesso risultato. Diverso da `/decode`, che invece lasci sullo standard: lì lavori su fonti eterogenee (PDF lunghi, chat da mille messaggi), la potenza del modello serve.

**🛠️ COSTRUISCI**:
```
mkdir -p ~/.claude/skills/sogna
# crea ~/.claude/skills/sogna/SKILL.md con l'esempio sopra
```

**✅ VERIFICA** — dopo un po' di conversazioni, `/sogna`: crea/aggiorna file in `memory/` e `brain/`, e popola `.sogna-fatte.md`. Rilancialo subito: deve dire "nessuna sessione nuova" — la prova che il registro funziona.

I tre modi di imparare sono completi: `/ricorda` (a mano), `/decode` (da fonti), `/sogna` (da te stesso).

---

## Stage 10 — /backup & manutenzione: non perdere nulla

> Niente git: troppo da smanettoni. Facciamo copie zip datate, e le fa una skill — l'utente digita `/backup` e basta.

**🎬 MOSTRA** — la skill che salva tutto in una copia datata:
```markdown
---
name: backup
description: "Salva una copia di tutto l'agente in uno zip con data e ora. /backup."
user-invocable: true
argument-hint: ""
---
# /backup
1. Se non esiste, crea la cartella ~/claude-backups/
2. Crea uno zip dell'intera ~/.claude (esclusa ~/claude-backups) chiamato:
   ~/claude-backups/agente-AAAAMMGG-HHMM.zip
3. Conferma il path del file creato e dimmi quanti backup ho in tutto.
```

**💡 SPIEGA** — un agente che non si manutiene marcisce (ricordi duplicati, fatti contraddittori, brain stantio). Due abitudini bastano, zero terminale:
1. **Copia**: ogni tanto digita `/backup` → uno zip datato finisce in `~/claude-backups/`. Se qualcosa si rompe, riapri lo zip di ieri. Quei file puoi anche copiarli su una chiavetta o sul cloud.
2. **Consolida**: a fine giornata lancia `/sogna` → l'agente rilegge le conversazioni e salva da solo cosa avete imparato.

(Chi mastica git può versionare `~/.claude` invece degli zip: stesso scopo, sync su più macchine. Opzionale, non serve oggi.)

**🛠️ COSTRUISCI**:
```
mkdir -p ~/.claude/skills/backup
# crea ~/.claude/skills/backup/SKILL.md con l'esempio sopra
```
poi, in una nuova sessione, prova: `/backup`

**✅ VERIFICA** — in `~/claude-backups/` compare un file `agente-AAAAMMGG-HHMM.zip`. Cerchio chiuso: identità → conoscenza → voce → capacità → apprendimento → copia di sicurezza = **il tuo agente cognitivo**.

---

## Handout

Su `/learn handout`: genera un markdown autoconsistente in `~/learn-handout.md`, poi offri di mostrarlo o mandarlo con SendUserFile.

Struttura:
- **Testa**: titolo, il modello mentale a 3 layer, prerequisito (Claude Code: https://claude.com/claude-code).
- **11 stage** (0-10) come guida passo-passo: per ognuno obiettivo in una riga · snippet **COSTRUISCI** copy-paste (coi dati dello studente se noti) · riga **VERIFICA**.
- **Coda**: checklist finale "alla fine devi avere: CLAUDE.md ✓ · memory/ con 1 fatto ✓ · skill /ricorda ✓ · brain/ con 1 modulo + INDEX ✓ · styles/ con la tua voce ✓ · formati ✓ · skill /scrivi ✓ · preferences.md ✓ · skill /decode ✓ · skill /sogna ✓ · skill /backup + primo zip ✓". Cioè 5 skill: /ricorda · /scrivi · /decode · /sogna · /backup.

Vincoli: niente em-dash. Accenti corretti (è/à/ù). Lingua dello studente (default italiano).

---

## Note per il conduttore

- Guidata DAL VIVO: lo studente dice `next`, parte uno stage. Non anticipare.
- **Zero dipendenze**: ogni esempio è qui dentro. Mai aprire file che sulla macchina dello studente non esistono.
- Tutto è dell'utente, coi SUOI dati e nel SUO dominio. Mai esempi di terzi.
- Stage 4 (voce), 8 (decode) e 9 (sogna) sono i più interattivi: nel 4 raccogli campioni veri, nell'8 fai ingerire un suo appunto reale, nel 9 fai vedere il registro `.sogna-fatte.md` che evita i doppioni.
- Stage 6 è il picco: `/scrivi` che fonde voce + formati + brain. Tienilo come climax.
- Le 5 skill che restano allo studente: `/ricorda` `/scrivi` `/decode` `/sogna` `/backup` (+ `/learn` stessa).
- Durata: ~8-10 min a stage dal vivo (~100 min pieno), ~55 min secco.
