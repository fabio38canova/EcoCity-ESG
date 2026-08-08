# EcoCity ESG — Come pubblicare l'alpha su GitHub Pages con login Supabase

Due servizi, entrambi gratuiti per un'alpha con pochi tester:
- **GitHub Pages** ospita il gioco (file statico, nessun server).
- **Supabase** gestisce utenti, verifica email e 2FA (login vero, non aggirabile).

Il repository Git è già pronto in questa cartella (`D:\SimCityESG`), con tutte le
versioni salvate (v1.0 → v2.1).

---

## Parte 1 — Creare il progetto Supabase (login)

1. Vai su **https://supabase.com** → *Start your project* → registrati (puoi
   usare l'accesso con GitHub).
2. Crea un nuovo progetto: dagli un nome (es. `ecocity-esg`), scegli una
   password del database (da conservare, non ti servirà per l'uso quotidiano)
   e una regione vicina (es. Frankfurt/EU).
3. Attendi 1-2 minuti che il progetto sia pronto.
4. Nel menu a sinistra vai su **Project Settings → API**. Copia due valori:
   - **Project URL**: per questo progetto è `https://srpkzecstxfbzrlzzopd.supabase.co`
     (ATTENZIONE: senza `/rest/v1/` in fondo — già inserita nel gioco)
   - **anon public key**: è la stringa LUNGA che inizia con `eyJ...` nel
     riquadro "Project API keys" (NON l'ID del progetto `srpkzecstxfbzrlzzopd`)
   Questi due valori NON sono segreti: sono fatti per stare in un sito
   pubblico (la sicurezza vera è garantita dal login, non dal nasconderli).
5. Vai su **Authentication → Providers** e verifica che **Email** sia
   attivo (lo è di default). Nella stessa sezione, verifica che
   **"Confirm email"** sia attivato (di default lo è): senza conferma email
   nessuno può accedere con un account creato a caso.
6. Vai su **Authentication → URL Configuration**. Dovrai tornarci al
   Passo 3 (dopo aver pubblicato su GitHub Pages) per inserire l'indirizzo
   del sito come **Site URL**, altrimenti il link di conferma email non
   funziona correttamente.

---

## Parte 2 — Inserire le chiavi nel gioco

1. Apri il file `EcoCityESG.html` con un editor di testo (Blocco Note va bene).
2. Cerca il testo `CONFIG SUPABASE` (vicino all'inizio dello script).
3. Sostituisci:
   ```
   const SUPABASE_URL = "INCOLLA_QUI_LA_TUA_PROJECT_URL";
   const SUPABASE_ANON_KEY = "INCOLLA_QUI_LA_TUA_ANON_KEY";
   ```
   con i due valori copiati al Passo 1.4. Esempio:
   ```
   const SUPABASE_URL = "https://xxxxxxxx.supabase.co";
   const SUPABASE_ANON_KEY = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...";
   ```
4. Salva il file.

---

## Parte 3 — Pubblicare su GitHub Pages

### 3.1 Crea l'account e il repository su GitHub
1. Se non hai un account, registrati su **https://github.com**.
2. Clicca **+ → New repository** in alto a destra.
3. Nome repository: es. `ecocity-esg`. Impostalo **Private** se vuoi che il
   codice sorgente non sia visibile a chiunque (consigliato per un'alpha),
   oppure **Public** (GitHub Pages funziona con entrambi, ma su piano
   gratuito Pages da repo *privato* richiede un account GitHub Pro/Team —
   verifica il tuo piano; in caso di dubbio scegli Public: il login
   Supabase protegge comunque l'accesso al GIOCO, non al codice).
4. NON aggiungere README/licenza automatici (il repository locale ne ha già).
5. Clicca **Create repository**. Nella pagina successiva GitHub mostra
   un indirizzo tipo `https://github.com/tuonome/ecocity-esg.git`: copialo.

### 3.2 Collega il repository locale e carica i file

> **PREREQUISITO**: sul PC deve essere installato Git, che su Windows non è
> presente di serie. Due alternative:
> - **GitHub Desktop** (consigliata, senza terminale): installa da
>   https://desktop.github.com, accedi col tuo account GitHub, poi
>   File → Add local repository → `D:\SimCityESG` → **Publish repository**.
>   Fatto questo, salta direttamente al punto 3.3.
> - **Git per Windows** (riga di comando): installa da
>   https://git-scm.com/download/win con le impostazioni predefinite, poi
>   CHIUDI E RIAPRI il terminale e prosegui con i comandi qui sotto.
Apri un terminale nella cartella `D:\SimCityESG` (su Windows: tasto destro
nella cartella → "Apri nel terminale" oppure `cd D:\SimCityESG` in un
prompt) ed esegui, uno alla volta, i comandi qui sotto.

> NOTA: le righe con i tre apici (` ``` `) NON vanno digitate: sono solo la
> cornice del blocco di codice. Copia e incolla SOLO i comandi al loro
> interno, uno per volta, sostituendo `tuonome` con il tuo utente GitHub.

```bash
git remote add origin https://github.com/tuonome/ecocity-esg.git
git branch -M main
git push -u origin main
```

Al primo push, GitHub chiederà di autenticarti (nel browser, o con un
Personal Access Token se richiesto al posto della password).

Da questo momento, ogni volta che vorrai pubblicare una nuova versione
basterà:
```bash
git add -A
git commit -m "descrizione della modifica"
git push
```

### 3.3 Attiva GitHub Pages
1. Nel repository su GitHub, vai su **Settings → Pages** (menu a sinistra).
2. In **Source**, seleziona **Deploy from a branch**.
3. In **Branch**, seleziona **main** e cartella **/ (root)** → **Save**.
4. Attendi 1-2 minuti. GitHub mostrerà l'indirizzo pubblico, tipo:
   `https://tuonome.github.io/ecocity-esg/`
5. Il gioco vero e proprio sarà su:
   `https://tuonome.github.io/ecocity-esg/EcoCityESG.html`
   (puoi anche rinominare il file in `index.html` — vedi nota in fondo —
   per avere l'indirizzo pulito senza `/EcoCityESG.html` alla fine).

---

## Parte 4 — Completare la configurazione Supabase

1. Torna su Supabase → **Authentication → URL Configuration**.
2. In **Site URL** incolla l'indirizzo del gioco ottenuto al Passo 3.3
   (es. `https://tuonome.github.io/ecocity-esg/EcoCityESG.html`).
3. Salva. Da ora i link di conferma email che Supabase invia ai tester
   punteranno correttamente al tuo gioco pubblicato.
4. Ricarica la pagina del gioco: dovresti vedere il cancello di accesso
   con le schede **Accedi** / **Registrati**.

---

## Come funziona per i tuoi tester

1. Aprono il link del gioco → schermata di accesso.
2. **Registrati**: inseriscono email e password → ricevono un'email da
   Supabase con un link di conferma → cliccano il link → possono accedere.
3. **Accedi**: email + password.
4. Al primo accesso il gioco propone di attivare la **verifica in due
   passaggi** (2FA): se accettano, mostra un QR code da inquadrare con
   un'app come Google Authenticator o Authy, poi chiede il codice a 6
   cifre per confermare. Da quel momento, ogni login richiederà anche
   quel codice.
5. Una volta dentro, il gioco funziona esattamente come prima (i
   salvataggi restano nel browser di ciascun tester tramite localStorage:
   ogni tester vede solo le proprie città salvate su quel dispositivo).
6. Per uscire: menu **☰ → 🚪 Esci**.

---

## Gestire i tester (facoltativo)

Su Supabase, **Authentication → Users** mostra l'elenco di chi si è
registrato: puoi eliminare un account, o disattivarlo, in qualsiasi momento.
Se vuoi limitare l'accesso a un elenco chiuso di persone, in
**Authentication → Providers → Email** puoi disattivare la registrazione
libera e creare tu manualmente gli account dei tester da quella stessa
sezione **Users → Add user**.

---

## Note

- **Il codice sorgente e l'anon key sono visibili** a chi ispeziona la
  pagina: è normale e sicuro per Supabase (la sicurezza reale è nelle
  policy del database, non nel nascondere questa chiave). Ciò che è
  protetto è l'ingresso al gioco, non il codice HTML in sé — se vuoi
  nascondere anche il codice, usa un repository **Private** (nota al
  punto 3.1 sul piano GitHub necessario).
- Per rinominare `EcoCityESG.html` in `index.html` (indirizzo più pulito):
  rinomina il file, poi `git add -A && git commit -m "rename" && git push`.
- Per il rollback a una versione precedente: `git checkout v2.0 -- EcoCityESG.html`
  seguito da commit e push, oppure chiedimelo direttamente.
- Aspetti privacy/GDPR: raccogliendo email di utenti registrati in UE,
  valuta di aggiungere una breve informativa privacy nella pagina di
  registrazione prima di allargare i tester oltre una cerchia ristretta
  di conoscenti; non sono un consulente legale, quindi per un uso esteso
  ti conviene un parere professionale.
