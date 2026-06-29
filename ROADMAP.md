# BrAIn — stato e da fare

## 1. Repo GitHub  ✅ fatto
- [x] Creato `lastknight/brAIn` (pubblico) e primo push → https://github.com/lastknight/brAIn
- [x] `LICENSE` MIT (il README la dichiara).
- [x] `.gitignore` (esclude `.DS_Store` e gli zip).
- [x] Zip di release (`learn/` + `INSTALLA.md`) allegato a `v1.0.0` → /releases/latest

## 2. README dichiarativo  ✅ fatto
- [x] Cos'è un agente cognitivo (con tabella prima/dopo, zero gergo).
- [x] Cosa NON è (gestione aspettative).
- [x] Premesse operative + prerequisiti onesti (abbonamento/API, costo).
- [x] I 6 comandi in dettaglio (cosa fa · quando · esempio · razionale).
- [x] I razionali di fondo (testo non DB, un fatto un file, MERGE, memoria≠brain, poche regole).
- [x] Buone norme · I tuoi dati (privacy con onestà) · struttura file · licenza · crediti.

## 3. Installazione "dai lo zip a Claude"  ✅ fatto
- [x] Path primario: avvii Claude Code, gli dai lo zip, dici "installa".
- [x] `INSTALLA.md` con blocco "ISTRUZIONI PER CLAUDE" (payload auto-installante).
- [x] Per-piattaforma (drag&drop desktop / path nel CLI) + "riavvia Claude Code".
- [x] `cp -R` manuale come fallback.
- [x] Zip generato e allegato alla release v1.0.0.

## 4. Fix on-ramp nella skill  ✅ fatto
- [x] Stage 0 "💥 SENTI IL PROBLEMA": far sentire la statelessness prima di costruire.
- [x] Corsia unica dichiarata: non apri terminali, parli all'agente e lui esegue.
- [x] Pattern COSTRUISCI riscritto: i file li crea l'agente, non lo studente.
- [x] Nota "le skill caricano al riavvio" alla prima skill creata (Stage 2).
- [x] Bug minori sistemati: range stage 0-10, accenti monchi, mappa in ordine.

## Idee aperte (non bloccanti)
- [ ] Coprire l'installazione di Claude Code stesso per chi parte davvero da zero (oggi è solo un link).
- [ ] Alleggerire il carico cognitivo dello Stage 2 (YAML+markdown+shell+path tutto insieme).
- [ ] `/sogna` su macchina vergine: poche sessioni da cui imparare — chiarire nel verify.
