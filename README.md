# Visita del sorvegliante – prenotazioni

App per prenotare le uscite in servizio con il sorvegliante di circoscrizione durante la settimana della visita.

- **Sito**: `https://lucioros.github.io/visitasorvegliante/` (dopo la pubblicazione)

## Cosa fa

**Fratelli** (vedono solo la pagina delle prenotazioni)
- Aprono il link di invito, scelgono il proprio nome e creano un PIN personale (4–6 cifre)
- Scelgono se uscire **con il sorvegliante** o **con sua moglie** e prenotano una mezza giornata libera
- Inseriscono il proprio numero di telefono (resta salvato per le volte successive)
- Indicano il motivo, anche più di uno: *servizio di campo*, *visite ulteriori*, *studi biblici*
- Per gli studi biblici indicano pubblicazione, lezione e paragrafo (anche più studi)
- Possono modificare o annullare la propria prenotazione

**Amministratore** (pulsante ⚙︎ Gestione)
- **Giorni**: aggiunge i giorni della visita e indica per ogni mattina/pomeriggio orario, luogo, se escono il sorvegliante e la moglie e quanti appuntamenti può prendere ciascuno
- **Eventi**: adunanza con i pionieri regolari, adunanza con anziani e servitori di ministero, mezza giornata libera o altri eventi, per mattina, pomeriggio, tutto il giorno o sera. Si indica chi partecipa. Gli eventi compaiono nel programma e nel PDF; gli appuntamenti dipendono solo dalla casella “esce” (per la mezza giornata libera la spunta viene tolta automaticamente)
- **Fratelli**: manda l'invito con WhatsApp o Telegram a tutti quelli non ancora invitati (uno dopo l'altro) o a un singolo fratello dalla sua scheda; importa l'elenco dall'app *Gruppi di servizio* oppure lo scrive a mano, aggiunge o corregge i numeri di telefono (anche importandoli da un export di Hourglass, letto solo sul dispositivo), azzera un PIN e nomina altri amministratori
- **Riepilogo**: programma completo con eventi, telefoni, motivi e studi, e **PDF degli appuntamenti** in una pagina A4 verticale (un riquadro per il sorvegliante e uno per la moglie) da scaricare, stampare o condividere, da copiare o mandare su WhatsApp al sorvegliante. Mostra anche chi non ha ancora prenotato
- **Visite**: dati del sorvegliante e della moglie (nome e telefono), apertura e chiusura delle prenotazioni, creazione di una **nuova visita**. La precedente va nello storico; può copiare orari, luoghi ed eventi
- **Storico**: tutte le visite passate, le uscite di ogni fratello ed export in Excel (CSV)
- **Impostazioni**: notifiche all'amministratore su Telegram (con un bot personale creato con @BotFather) e/o WhatsApp (tramite il servizio gratuito CallMeBot) per ogni prenotazione, modifica o annullamento; link di invito, numero di appuntamenti predefinito, uscite massime per fratello, password, token GitHub

## Installazione come app sul telefono

Chi apre il link vede il riquadro **Installa l'app sul telefono**:
- **Android (Chrome)**: tocca *Installa*, poi conferma. L'app compare tra le altre con la sua icona.
- **iPhone (Safari)**: tocca *Installa* e segui le istruzioni (*Condividi → Aggiungi alla schermata Home*). Su iPhone l'app installata potrebbe chiedere una volta la password della congregazione: la finestra delle istruzioni la mostra.
- Se il link è stato aperto dentro WhatsApp, prima bisogna aprirlo in Chrome o Safari (menu ⋯ → *Apri nel browser*).

L'app installata si apre a schermo intero e legge sempre i dati aggiornati.

## Come sono protetti i dati

Funziona come *Gruppi di servizio*: tutti i dati stanno in `dati.json`, **cifrati** (AES-GCM, chiave ricavata dalla password con PBKDF2). Senza la password il file è illeggibile, anche se il repository è pubblico. Anche il token GitHub che serve per salvare è cifrato nello stesso file.

Ogni salvataggio crea una modifica nel repository con una descrizione generica, senza nomi. Ogni fratello si identifica con nome + PIN personale. Se due prenotano l'ultimo posto nello stesso istante, GitHub accetta solo il primo e l'altro riceve "Posti esauriti".

## Pubblicazione (una volta sola)

1. Su GitHub crea un nuovo repository **pubblico** chiamato `visitasorvegliante`
2. Carica tutti i file dello zip: `index.html`, `sw.js`, `manifest.webmanifest`, la cartella `icons`, `README.md` e `.nojekyll`
3. *Settings → Pages*: Source **Deploy from a branch**, branch **main**, cartella **/ (root)** → Save
4. Crea un token: *Settings (del tuo profilo) → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token*
   - Repository access: **Only select repositories** → `visitasorvegliante`
   - Permissions → Repository → **Contents: Read and write**
   - Scadenza: per esempio 1 anno (quando scade, incollane uno nuovo in Gestione → Impostazioni)
5. Apri il sito dopo 1–2 minuti. Compila la configurazione iniziale (password della congregazione, token, il tuo nome e PIN) e premi **Crea archivio**
6. Aggiungi i giorni della visita e importa i fratelli
7. Da **Impostazioni → Invita i fratelli** manda il link su WhatsApp

## File

| File | Cosa contiene |
|---|---|
| `index.html` | L'applicazione |
| `dati.json` | Dati cifrati, creati dall'app (non modificarlo a mano) |
| `sw.js`, `manifest.webmanifest` | Permettono di installare l'app sul telefono |
| `icons/` | Icone dell'app |
| `jspdf.umd.min.js` | Libreria jsPDF (MIT) per creare i PDF |
| `.nojekyll` | Serve a GitHub Pages |
