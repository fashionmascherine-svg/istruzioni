# Grok Imagine Master Prompt & Voiceover Guide

> Stato: aggiornato a febbraio 2026. Include Grok Imagine 0.1, 0.9 e 1.0, più il modulo **Audio with Video** (Aurora Engine) e best practice per prompt T2V/I2V con voiceover e dialogo sincronizzato.

---

## 1. Panoramica: cos'è Grok Imagine

Grok Imagine è il generatore di immagini e video con audio nativo integrato nell'ecosistema Grok/X di xAI, basato sul motore autoregressivo **Aurora**.[web:63][web:64][web:66][web:68][web:71][web:72] 
Permette di creare immagini e brevi clip video (tipicamente 6–15 secondi) con motion cinematografico, audio generato (musica, SFX, VO) e lip sync accurato a partire da prompt testuali o voce.[web:38][web:64][web:69]

Funzioni chiave:
- **Text‑to‑Video (T2V)**: da prompt testuale a clip video con audio.[web:38][web:64][web:69]
- **Image‑to‑Video (I2V)**: animazione di immagini statiche (generate o caricate) in brevi video con motion e soundscape coerenti.[web:38][web:64][web:69]
- **Edit/Sketch to Video**: modifica di immagini e trasformazione di sketch in scene dinamiche.[web:38][web:69]
- **Audio with Video**: secondo pass dedicato all'audio nativo (SFX, musica, dialogo, VO) per video creati con Grok Imagine.[web:42][web:70]

Aurora utilizza un modello **autoregressivo mixture‑of‑experts** che predice token di immagine e video in sequenza (anziché denoising diffusive), con vantaggi su aderenza al prompt, testo leggibile e coerenza spaziale/temporale.[web:63][web:66][web:68][web:74]

---

## 2. Versioni note e stato attuale (febbraio 2026)

Le principali versioni/iterazioni di Grok Imagine visibili pubblicamente sono:

### 2.1 Grok Imagine 0.1 (beta iniziale)

- Rilascio iniziale descritto come **"0.1"** e definito esplicitamente "beta" da Musk.[web:64][web:67]  
- Funzionalità:
  - Creazione di immagini e brevi video (fino a ~15s) a partire da prompt testuali o vocali.[web:64][web:67]
  - Animazione di foto in clip brevi con audio generato automaticamente (soundtrack/effects).[web:64][web:67]
  - Modalità **Spicy** per contenuti NSFW non completamente filtrati, molto discussa a livello di policy.[web:64][web:67]
- Modello: pipeline a due stadi (immagine → animazione video + audio) basata su Aurora e componenti custom, fortemente ottimizzata per velocità e iterazione rapida.[web:64][web:67]

### 2.2 Grok Imagine 0.9 (aggiornamento maggiore)

- Update importante (v0.9) orientato al miglioramento di velocità, durata clip e accessibilità free.[web:32][web:71]
- Caratteristiche chiave riportate:
  - Clip fino a ~6–15 secondi, generazione tipica intorno a 20 secondi su mobile/web app Grok.[web:32][web:71]
  - Modalità **fun / normal / spicy** per bilanciare creatività, realismo e libertà di contenuto.[web:32][web:71]
  - Accesso gratuito per tutti gli utenti X/Grok durante alcune finestre promozionali, con priorità/limiti più alti per abbonati SuperGrok.[web:71]
  - Integrazione diretta in app Grok (mobile) e interfaccia chat Grok con prefisso `Imagine:` per prompt multimediali.[web:71]

### 2.3 Grok Imagine 1.0 (modello attuale di riferimento)

- Descritto come **"Grok Imagine 1.0" – HD AI Video Generator with Native Audio"** e ampiamente trattato in guide 2025–2026.[web:38][web:69]  
- Miglioramenti principali rispetto a versioni precedenti:
  - **Clip fino a 15s** con motion più cinematografico e camera commands più stabili.[web:38][web:69]
  - **720p/1080p HD** con possibilità di upscaling rapido tramite pulsante "Upscale" per portare clip a definizione più alta.[web:38][web:69]
  - **Native audio completo**: musica, ambience, SFX e dialogo/lip sync nello stesso pass, con modulo dedicato **Audio with Video**.[web:38][web:42][web:69][web:70]
  - Supporto T2V e I2V multimodale, incluse trasformazioni "Sketches to Life" e editing con testo.[web:69]
  - Comprensione di comandi di camera professionali (zoom, pan, tilt, tracking) e fisica più realistica per interazioni oggetto‑ambiente.[web:69]

### 2.4 Stato "ultima versione" (Aurora Engine, 2026)

- La documentazione e le guide aggiornate al 2026 convergono su **Grok Imagine 1.0 (Aurora engine)** come modello consumer principale disponibile via Grok App / X / siti Grok Imagine.[web:38][web:66][web:69][web:72][web:73]  
- Non risultano numeri di versione pubblici superiori a 1.0 (es. 1.1, 2.0) nel materiale ufficiale; esistono però update continui lato Aurora e UI (es. apertura temporanea in free access, espansione di Audio with Video, refining del lip sync, ecc.).[web:63][web:66][web:69][web:71]  
- Lato marketing, molti siti terzi si riferiscono semplicemente a **"Grok Imagine (Aurora Engine)"** senza più esporre il numero, ma gli articoli tecnici e guide più recenti continuano a chiamarlo **1.0** come base.[web:66][web:68][web:69]

In pratica, per chi sviluppa template nel 2026 ha senso considerare **Grok Imagine 1.0 su Aurora** come target principale, compatibile verso il basso con 0.9/0.1.

---

## 3. Parametri e preset specifici di Grok Imagine

### 3.1 Parametri di generazione core

Le interfacce web/API (Kie.ai, Imagine wrappers, Grok App) espongono parametri molto simili:[web:10][web:11][web:18][web:21][web:69]

- **Mode / Style Mode**: generalmente `normal | fun | spicy | custom` a seconda della piattaforma.
  - *normal*: equilibrio tra realismo e creatività, adatto a fotorealistico e corporate.[web:21][web:69]
  - *fun*: look più cartoon/giocoso.[web:21]
  - *spicy*: stile più aggressivo e policy meno restrittiva, spesso associato all'uso NSFW (da usare con cautela).[web:64][web:67]
- **Duration**: tipicamente 6s o 10s via API, con opzione fino a ~15s nella UI 1.0.[web:21][web:38][web:64][web:69]
- **Resolution**:
  - 480p / 720p come opzioni comuni nelle API; UI 1.0 mostra preset 720p HD e possibilità di upscaling a 1080p.[web:21][web:38][web:69]
- **Aspect Ratio**:
  - Preset vertical (9:16), horizontal (16:9), square (1:1), selezionati a livello UI, non come flag in stile `--ar`.[web:10][web:69]
- **Modalità input**:
  - Text‑to‑Video (prompt testo).
  - Image‑to‑Video (immagine di base + prompt opzionale).[web:38][web:64][web:69]

In molte API wrapper per Grok Imagine (es. Kie.ai) la struttura base è:

```jsonc
{
  "prompt": "...",
  "mode": "normal" | "fun" | "spicy",
  "duration": "6" | "10",
  "resolution": "480p" | "720p"
  // + eventuali campi per image-to-video
}
```

> **Nota:** aspect ratio e opzioni avanzate (es. 1080p, Upscale) sono spesso gestite a livello UI o endpoint proprietari X/Grok, non come parametri pubblici di terze parti.[web:10][web:38][web:69]

### 3.2 Golden Prompt Formula di Grok

La *Prompt Guide* ufficiale Grok Imagine xAI e varie guide 2026 convergono su una "formula d'oro" per i prompt video:[web:11][web:14][web:37][web:69]

> **[Subject] + [Movement/Action] + [Scene/Environment] + [Shot/Camera] + [Style] + [Audio Direction]**[web:11][web:14][web:37]

Con varianti come:
- "subject + movement + scene + shot, style" (nella prompt guide xAI).[web:11]
- "Subject + Action/Motion + Camera Movement + Visual Style + Audio Direction" (guide dedicate a Grok video).[web:14]

Regole aggiuntive:
- Le **prime 5–20 parole sono critiche** perché Aurora legge il prompt in modo strettamente sequenziale (autoregressivo); si consiglia di introdurre immediatamente soggetto, azione chiave e tipo di shot.[web:11][web:14][web:74]
- Prompt concisi e strutturati funzionano meglio di paragrafi lunghi: soggetto, azione, scena, camera e stile devono stare nella parte alta; dettagli secondari possono seguire.[web:11][web:14][web:66]

---

## 4. Voiceover, dialogo e lip sync in Grok Imagine

### 4.1 Capacità audio di base

Grok Imagine 1.0, tramite l'integrazione Aurora, genera **audio nativo** insieme al video:[web:32][web:38][web:42][web:64][web:69][web:70]

- **Soundscape automatico**: musica di sottofondo e ambience coerenti con la scena possono essere generati anche senza specifiche dettagliate.
- **SFX**: rumori di oggetti, passi, motore, vento, ecc. vengono inferiti dal movimento visivo e da parole chiave nel prompt.[web:38][web:69]
- **Dialogo & Lip Sync**: il modello è in grado di generare dialogo sincronizzato con i movimenti della bocca di personaggi on‑screen, specialmente per frasi brevi.[web:32][web:38][web:42][web:69]

Il modulo **Audio with Video** (Grok Imagine xAI — Audio with Video) permette di aggiungere o rielaborare audio su un video esistente in tre step:[web:42][web:70]
1. Scegli modalità (Text‑to‑Video o Image‑to‑Video) e genera il video base.
2. Apri "Audio with Video" e incolla un **audio prompt** dedicato che descrive soundscape, stile/lingua della voce e timing.
3. Genera e scarica il video con audio sincato.

### 4.2 Script esplicito: far dire frasi precise

Tutorial e guide su talking animations con Grok mostrano un pattern ricorrente per ottenere frasi precise e lip sync:[web:35][web:36][web:39][web:41]

- Lo script del dialogo va incluso **esplicitamente** nel prompt, in forma testuale virgolettata.
- È utile usare etichette come `Dialogue:`, `Character says:`, `Off-screen narrator:`.
- Le clip devono contenere frasi relativamente brevi (5–10s di parlato) per mantenere alta la qualità del lip sync.[web:32][web:35][web:36][web:39]

Esempi di pattern T2V/I2V:

```text
A 3D animated presenter standing in front of a car, medium shot, clean studio lighting.
Dialogue: she says in Italian, clearly and slowly: "Benvenuto al corso di sicurezza stradale".
Perfect lip sync, friendly tone.
```

```text
A realistic mechanic looks directly into camera in a workshop, serious mood.
Off-screen narrator: deep male voice in Italian says: "Prima di partire, controlla sempre freni e pneumatici".
On-screen character remains mostly silent while the narrator speaks.
```

Per clip multi‑scene o long‑form, i flussi tutorial mostrano che ogni scena viene generata con:
- descrizione del personaggio (coerente tra scene),
- descrizione della posa/azione per quella scena,
- porzione di dialogo specifica per quel beat narrativo.

**Best practice:** ripetere in ogni scena **descrizione del personaggio + voce + dialogo testuale** per ancorare stile e lip sync.[web:35][web:39][web:41]

### 4.3 Voiceover fuoricampo vs personaggio parlante

Distinzione importante per controllare visivamente il labiale:

- **Personaggio parlante on‑screen**:
  - Il prompt deve dire esplicitamente che il personaggio parla e che la bocca si muove in sync.
  - Pattern tipico:

    ```text
    Character: [descrizione fisica e ruolo].
    Dialogue: he says in Italian: "testo esatto".
    Perfect lip sync, mouth movements match each syllable.
    ```

- **Voce fuoricampo (voiceover)**:
  - Il personaggio sullo schermo resta in gran parte muto (o con movimenti minimi), mentre una voce esterna narra.
  - Pattern tipico:

    ```text
    Scene: [descrizione visiva].
    Off-screen narrator: warm female voice in Italian says: "testo esatto".
    On-screen characters remain mostly silent, no exaggerated mouth movement.
    ```

- **Audio with Video**:
  - Nel prompt audio si può enfatizzare ancora di più chi parla e quando ("early in the clip", "midway", "at the end"), oltre a lingua, timbro e intensità.[web:42][web:70]

### 4.4 Layering audio (VO, SFX, ambience, musica)

Grok Imagine genera una **singola traccia audio mixata**, non stem separati, ma accetta indicazioni di mix via testo.[web:32][web:38][web:42][web:69][web:70]

Pattern robusto:

```text
Audio: calm Italian male narrator voice is the main foreground.
Background: very soft ambient workshop noise.
SFX: crisp but subtle tool sounds exactly when the hands move.
Music: no music.
```

Oppure per scena action:

```text
Audio: cinematic music bed, moderately loud.
SFX: engine roar, tire screech, crowd cheering, synchronized with visible motion.
Dialogue: short shouted line "Ora o mai più!" in Italian, clearly audible above the music.
```

Le guide mettono in guardia sull'uso di negative prompt audio ("no music", "no loud SFX") perché il modello li considera poco affidabili; è quindi preferibile **dichiarare positivamente** cosa si vuole e solo opzionalmente aggiungere note "no ...".[web:11][web:14]

---

## 5. Negative prompt in Grok Imagine

La *Prompt Guide* di Grok Imagine xAI nota esplicitamente che:

> "Negative Prompts do not elicit responses"[web:11]

Implicazioni pratiche:
- Non esiste un canale strutturato di negative prompt in stile Stable Diffusion.
- Frasi del tipo `no text`, `avoid blur`, `no extra limbs` hanno effetto limitato o nullo se messe in fondo al prompt.[web:11][web:14]
- Meglio formulare i vincoli **in positivo**, integrandoli nei segmenti core del prompt (soggetto, scena, camera, stile, audio).

Un blocco "[NEGATIVE_PROMPT]" può comunque essere usato come memo personale nella progettazione di template, ma va tradotto in assertivi positivi all'interno del prompt effettivo.

---

## 6. Master Template per Grok Imagine (con Voiceover)

Questa sezione propone un **Master Template universale** progettato specificamente per Grok Imagine 1.0 (Aurora), compatibile con T2V, I2V e con il modulo Audio with Video.

### 6.1 Parametri Grok (fuori dal prompt)

Prima di scrivere il testo, imposta sempre:

- **Mode**: `normal | fun | spicy | custom` (in base al genere e al livello di stilizzazione desiderato).[web:21][web:64][web:69]
- **Duration**: 6s o 10s (UI e API), eventualmente fino a 15s dove disponibile.[web:21][web:38][web:64][web:69]
- **Resolution**: almeno 720p; usa Upscale per 1080p se la UI lo offre.[web:38][web:69]
- **Aspect Ratio**: 16:9 (YouTube), 9:16 (Shorts/Reels/TikTok), 1:1 (feed classico).[web:10][web:69]
- **Input Mode**: Text‑to‑Video oppure Image‑to‑Video (con immagine base coerente col prompt).[web:38][web:64][web:69]

### 6.2 Template logico a blocchi

> **Nota:** il prompt finale da incollare in Grok deve essere una versione fluida concatenata di questi blocchi. Le prime 1–2 frasi devono già includere `Subject + Action + Camera + Style + Audio Direction`.

```text
[GENRE_SELECTOR]:
[SUBJECT] + [ACTION/MOTION] + [CAMERA TYPE/MOVEMENT] + [VISUAL STYLE] + [AUDIO DIRECTION]
(es. "A realistic mechanic explaining car safety to camera, medium shot, clean studio lighting, clear Italian dialogue and subtle workshop ambience")

[SCENE_FOUNDATION]:
Scene: [AMBIENTE/SFONDO] in [MOMENTO DEL GIORNO] con [MOOD sintetico].
Physics & Style: [REALISTIC MOTION PHYSICS / CARTOON-STYLE MOTION, SQUASH & STRETCH / SURREAL DREAMY MOTION] coerente con [GENRE_SELECTOR].
Lighting & Color: [TIPO DI ILLUMINAZIONE] + [PALETTE COLORE].
Static Elements: solo pochi elementi statici fondamentali (max 1 frase).

[SUBJECT_ACTION]:
Main Subject: [DESCRIZIONE COMPATTA DEL PERSONAGGIO, con feature chiave].
Multi-Beat Actions (ordine temporale, 1–3 frasi brevi):
1) [AZIONE 1 iniziale]
2) [AZIONE 2]
3) [AZIONE 3 finale]
Shot Continuity: "one continuous shot" oppure usare la parola chiave "Shot Switch" tra blocchi d'azione se vuoi stacchi.

[CAMERA_DYNAMICS]:
Shot Type: [wide / medium / close-up / extreme close-up / macro].
Camera Movement: massimo 1–2 istruzioni, es. "low-angle follow-shot", "slow push-in", "orbit 180°".
Esempio: "Camera: medium close-up at eye level, very slow push-in toward the character, no shaky cam."

[AUDIO_ENGINEERING]:
Soundscape & Music:
"Audio: [descrizione del mix generale: musica sì/no, tipo di musica, intensità, ambience principale]."
SFX:
"SFX: [elenco breve di suoni chiave] sempre sincronizzati con i movimenti visibili, mai più forti della voce."

[VOICEOVER_SCRIPT]:
-- Se il personaggio parla on-screen --
"Character: [ruolo e stile di voce, lingua, tono]."
"Dialogue: [he/she/they] says in [lingua], clearly and slowly: \"TESTO ESATTO DELLA FRASE 1\". Perfect lip sync."
[Eventuale seconda frase breve, sempre esplicita e in virgolette, se la durata lo consente.]

-- Oppure, se usi un narratore fuoricampo --
"Off-screen narrator: [tipo di voce, lingua, tono]."
"Narrator says: \"TESTO ESATTO DELLA FRASE FUORICAMPO\"."
"On-screen characters remain mostly silent while the narrator speaks, minimal mouth movement."

Mix Priority:
"Voiceover is the main foreground element, background music low and subtle, ambience very soft. SFX are crisp but never louder than the voice."

[NEGATIVE_PROMPT] (solo come memo interno, NON da incollare così com'è):
- Evita stile cartoon se [GENRE_SELECTOR] è fotorealistico → traduci in positivo: "photorealistic proportions, realistic lighting".
- Evita camera tremolante → "no shaky cam, smooth stabilized camera".
- Evita musica allegra se il mood è dark → "dark, tense sound design, no upbeat music".
```

### 6.3 Esempio A – Scena d'azione cinematografica (realistico)

```text
A photorealistic street racer drifting a red sports car at night, low-angle follow-shot, cinematic lighting, engine roar and crowd audio.
Neon-lit city street, wet asphalt reflecting colored lights, intense and electric mood, realistic motion physics.
A young female driver in a red racing suit and helmet speeds toward the camera, initiates a long controlled drift around a tight corner, then straightens the car and raises her fist in victory in one continuous shot.
Camera: low-angle tracking behind and slightly beside the car, smooth movement, no shaky cam.
Audio: cinematic music bed, moderately loud, with powerful engine roar and tire screech, crowd cheering along the track.
Dialogue: she shouts in Italian, clearly: "Ora o mai più!" Perfect lip sync.
```

### 6.4 Esempio B – Personaggio cartoon (stile Pixar) che spiega

```text
A cute Pixar-style 3D robot teacher explaining savings to camera, medium shot, soft classroom lighting, friendly Italian dialogue and playful UI sound effects.
Bright daytime in a colorful classroom, cheerful mood, cartoon-style motion with gentle squash and stretch.
The small round robot with big LED eyes waves to the viewer, then points at a digital whiteboard where icons of coins and piggy banks pop up, and ends with a thumbs-up toward camera.
Camera: centered medium shot at eye level, very slow push-in, no shake.
Audio: soft upbeat background music, very low; subtle classroom ambience; gentle "whoosh" and "pop" SFX when icons appear.
Character: friendly, slightly high-pitched cartoon voice in Italian.
Dialogue: he says in Italian, clearly and slowly: "Risparmiare un po' ogni mese ti aiuta a realizzare i tuoi sogni." Perfect lip sync, warm tone.
```

### 6.5 Esempio C – Tutorial macro realistico (mani che riparano un orologio)

```text
Ultra-realistic macro shot of gloved hands repairing a mechanical wristwatch on a wooden workbench, static top-down camera, neutral studio lighting, calm Italian voiceover and precise tool SFX.
Daytime in a quiet watchmaker's workshop, focused and meticulous mood, realistic motion physics.
Black-gloved hands pick up a tiny gear with tweezers, place it into the open watch movement, tighten a small screw, then hold the assembled movement steady under the lens at the end of the clip.
Camera: macro top-down shot on a tripod, almost static with a very subtle slow push-in, no zoom jumps.
Audio: no music, very soft workshop ambience with faint ticking in the background.
SFX: crisp close-mic metal clicks when tweezers and screwdriver touch the watch, synchronized with movements.
Off-screen narrator: calm male voice in Italian.
Narrator says: "Quando rimonti un movimento, lavora sempre con calma e non forzare mai gli ingranaggi." Voiceover is clearly on top of ambience and SFX.
On-screen hands remain naturally silent, no exaggerated motion during the narration.
```

---

## 7. Workflow consigliato per long‑form e agenti video

Per usare Grok Imagine in sistemi di **video agents** (multi‑scene, long‑form, automazione):

1. **Segmentazione in scene**: dividere lo script globale in scene/beat da 6–15 secondi con obiettivi visivi e frasi di dialogo molto chiari.
2. **Prompt per scena**: per ogni scena generare dinamicamente un prompt che riempie il Master Template sopra (in particolare [GENRE_SELECTOR], [SUBJECT_ACTION], [CAMERA_DYNAMICS], [VOICEOVER_SCRIPT]).
3. **Ripetizione coerente di personaggi e VO**: ripetere in ogni scena la descrizione sintetica del personaggio (outfit, età, stile visivo) e lo stile vocale.
4. **Uso di Image‑to‑Video per consistenza**: per scene successive, usare come input l'ultimo frame o un keyframe estratto dalla scena precedente, più un nuovo motion/audio prompt.[web:35][web:39][web:41]
5. **Secondo pass Audio with Video** (opzionale): se serve controllo fine del sound design, usare il modulo Audio with Video con un audio prompt che segue la stessa struttura di [AUDIO_ENGINEERING] + [VOICEOVER_SCRIPT] ma centrato sui timing.[web:42][web:70]
6. **Post‑processing esterno**: per pipeline pro (YouTube, ads), esportare i clip e rifinire mix audio e concatenazione in un NLE tradizionale, soprattutto se servono VO molto lunghi o colonne sonore complesse.

Questo markdown può fungere da base per gli agenti nel repository `grok-video-agents`, permettendo di generare automaticamente prompt Grok Imagine coerenti per diversi generi (cinema realistico, cartoon 3D/2D, corporate, documentario, tutorial tecnico) mantenendo un controllo esplicito sul voiceover e sul dialogo.
