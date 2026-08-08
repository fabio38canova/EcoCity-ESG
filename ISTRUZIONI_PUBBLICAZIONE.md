# EcoCity ESG — Pubblicazione su GitHub Pages con login Supabase

Stato attuale (aggiornato): il repository è pubblicato su
**https://github.com/fabio38canova/EcoCity-ESG** (pubblico), GitHub Pages è
attivo sul branch `main`, e il file di gioco è stato rinominato in
`index.html` per avere un indirizzo pulito:

**https://fabio38canova.github.io/EcoCity-ESG/**

Cartella locale collegata: `D:\EcoCity-ESG` (repository Git con cronologia
completa v1.0 → v2.4).

---

## Cosa resta da fare per completare il login

1. **Inserire la anon key di Supabase** nel gioco (vedi Parte 2 sotto) —
   finché manca, il gioco mostra l'avviso di configurazione invece del login.
2. **Impostare il Site URL su Supabase** (Parte 4 sotto) con l'indirizzo
   pubblico sopra, altrimenti i link di conferma email non funzionano.
3. Da GitHub Desktop: **Push** di ogni nuova modifica per pubblicarla
   (Commit → Push origin).

---

## Parte 1 — Progetto Supabase (già creato)

Project URL di questo progetto: `https://srpkzecstxfbzrlzzopd.supabase.co`
(già inserita nel gioco). Manca solo la **anon public key**: la trovi su
Supabase in **Project Settings → API**, riquadro "Project API keys",
voce **anon / public** — è una stringa lunga che inizia con `eyJ...`
(NON è l'ID del progetto).

Verifica anche che in **Authentication → Providers → Email** la voce
**"Confirm email"** sia attiva (di default lo è): senza conferma email
nessuno può accedere con un account creato a caso.

---

## Parte 2 — Inserire la anon key nel gioco

1. Apri `index.html` con un editor di testo (Blocco Note va bene), oppure
   incolla la chiave qui in chat e la inserisco io.
2. Cerca il testo `CONFIG SUPABASE` (vicino all'inizio dello script).
3. Sostituisci la riga:
   ```
   const SUPABASE_ANON_KEY = "INCOLLA_QUI_LA_TUA_ANON_KEY";
   ```
   con la chiave vera, tra virgolette. Esempio:
   ```
   const SUPABASE_ANON_KEY = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...";
   ```
4. Salva il file.
5. In **GitHub Desktop**: scrivi un breve riassunto in "Summary" (es.
   "aggiunta anon key") → **Commit to main** → **Push origin**.
6. Attendi 1-2 minuti che GitHub Pages ripubblichi automaticamente, poi
   ricarica **https://fabio38canova.github.io/EcoCity-ESG/**: dovresti
   vedere il cancello di accesso con le schede Accedi/Registrati.

---

## Parte 3 — Come pubblicare ogni futura modifica

Con **GitHub Desktop** (nessun comando da digitare):
1. Modifica i file nella cartella `D:\EcoCity-ESG` (io lo faccio per te
   quando mi chiedi una modifica).
2. Apri GitHub Desktop: la modifica compare nella scheda **Changes**.
3. Scrivi una riga di descrizione in **Summary** → **Commit to main**.
4. Clicca **Push origin** in alto.
5. In 1-2 minuti il sito pubblico si aggiorna da solo.

---

## Parte 4 — Completare la configurazione Supabase (Site URL)

1. Su Supabase → **Authentication → URL Configuration**.
2. In **Site URL** incolla: `https://fabio38canova.github.io/EcoCity-ESG/`
3. Salva. Da ora i link di conferma email che Supabase invia ai tester
   punteranno correttamente al gioco pubblicato.

---

## Come funziona per i tuoi tester

1. Aprono **https://fabio38canova.github.io/EcoCity-ESG/** → schermata di accesso.
2. **Registrati**: inseriscono email e password → ricevono un'email da
   Supabase con un link di conferma → cliccano il link → possono accedere.
3. **Accedi**: email + password.
4. Al primo accesso il gioco propone di attivare la **verifica in due
   passaggi** (2FA): se accettano, mostra un QR code da inquadrare con
   un'app come Google Authenticator o Authy, poi chiede il codice a 6
   cifre per confermare. Da quel momento, ogni login richiederà anche
   quel codice.
5. Una volta dentro, il gioco funziona come sempre (i salvataggi restano
   nel browser di ciascun tester tramite localStorage: ogni tester vede
   solo le proprie città salvate su quel dispositivo).
6. Per uscire: menu **☰ → 🚪 Esci**.

---

## Gestire i tester (facoltativo)

Su Supabase, **Authentication → Users** mostra l'elenco di chi si è
registrato: puoi eliminare o disattivare un account in qualsiasi momento.
Per limitare l'accesso a un elenco chiuso di persone, in
**Authentication → Providers → Email** puoi disattivare la registrazione
libera e creare tu manualmente gli account da quella stessa sezione
**Users → Add user**.

---

## Note

- **Il codice sorgente e l'anon key sono visibili** a chi ispeziona la
  pagina: è normale e sicuro per Supabase (la sicurezza reale è nelle
  policy del database, non nel nascondere questa chiave). Ciò che è
  protetto è l'ingresso al gioco, non il codice HTML in sé.
- Per il rollback a una versione precedente: chiedimelo direttamente, oppure
  in GitHub Desktop scheda **History** → tasto destro sul commit della
  versione desiderata → **Revert Changes** (per annullare le modifiche
  successive mantenendo la cronologia).
- Aspetti privacy/GDPR: raccogliendo email di utenti registrati in UE,
  valuta di aggiungere una breve informativa privacy nella pagina di
  registrazione prima di allargare i tester oltre una cerchia ristretta
  di conoscenti; non sono un consulente legale, quindi per un uso esteso
  ti conviene un parere professionale.
