# 🎬 Seedance 2.0 – Guida completa

Guida pratica e avanzata per generare **qualsiasi tipo di video** con Seedance 2.0:  
short virali, reel, spot prodotto, contenuti UGC, video lunghi per YouTube, con e senza voiceover.

> **Note preliminari**
> - I parametri `model`, `size` e `seconds` sono gestiti esternamente (UI/API, integrazioni): in questa guida NON li tocchiamo.
> - Qui trovi tutto ciò che puoi controllare **da prompt** e tramite **reference** (immagini, video, audio).
> - L’obiettivo è avere una struttura **ripetibile**, adatta sia a un singolo video che a produzioni in serie.

---

## 📌 Indice

1. [Concetti base di Seedance 2.0](#1-concetti-base-di-seedance-20)  
2. [Architettura del prompt](#2-architettura-del-prompt)  
3. [Sistema di reference `@`](#3-sistema-di-reference-)  
4. [Parametri controllabili (esclusi model/size/seconds)](#4-parametri-controllabili)  
5. [Movimenti camera – vocabolario pratico](#5-movimenti-camera--vocabolario-pratico)  
6. [Audio e voiceover (con e senza file)](#6-audio-e-voiceover)  
7. [Stili visivi e lighting](#7-stili-visivi-e-lighting)  
8. [Template pronti per tipo di video](#8-template-pronti-per-tipo-di-video)  
9. [Workflow pratici completi](#9-workflow-pratici-completi)  
10. [Best practice e limiti pratici](#10-best-practice-e-limiti-pratici)  

---

## 1. Concetti base di Seedance 2.0

Seedance 2.0 è un modello di generazione video **multimodale**: può usare testo, immagini, video e audio nello stesso progetto per guidare stile, composizione, movimento e ritmo del video.

Le quattro modalità logiche con cui penserai sempre sono:

- **Text-to-video**: solo prompt testuale.
- **Image-to-video**: una o più immagini come primo/ultimo frame o reference di stile.
- **Video-to-video**: un video di riferimento per copiare movimento di camera, coreografia o ritmo.
- **Multimodale completo**: combinazione di immagini, video e audio, collegati nel prompt con `@Image1`, `@Video1`, `@Audio1`, ecc.

Questa guida è organizzata per funzionare **indipendentemente dall’interfaccia** (Dreamina, Jimeng, WaveSpeed, ecc.) e concentrarsi su ciò che non cambia mai: il **modo di scrivere i prompt** e di usare le reference.

---

## 2. Architettura del prompt

### 2.1 Formula base universale

```text
[SOGGETTO] + [AZIONE] + [SCENA/AMBIENTE] + [CAMERA] + [STILE/LUCE] + [AUDIO]
```

### 2.2 Struttura a livelli (consigliata per tutto)

```text
OBIETTIVO: [scopo del video, piattaforma, pubblico]
FORMATO/DURATA: [aspect ratio, secondi]
SOGGETTO: [chi/cosa vediamo, aspetto]
AZIONE: [cosa succede, step principali, tempo presente]
SCENA/AMBIENTE: [dove, quando, atmosfera]
CAMERA: [inquadrature, movimenti, transizioni]
STILE VISIVO: [look, palette, riferimento cinematografico]
LUCE: [tipo di luce, direzione, intensità]
AUDIO: [voiceover, musica, SFX, lingua]
VINCOLI: [cosa evitare, coerenza, continuità]
```

**Esempio per short verticale prodotto tech (solo testo)**

```text
OBIETTIVO: short virale verticale per TikTok/Reels che mostri un nuovo smartphone in modo spettacolare.
FORMATO/DURATA: 9:16, 7 secondi.
SOGGETTO: smartphone nero lucido, bordo metallico, schermo acceso con wallpaper astratto blu.
AZIONE: il telefono ruota in aria a rallentatore, luci che scorrono sulla superficie.
SCENA/AMBIENTE: sfondo scuro astratto, riflessi luminosi in movimento.
CAMERA: inizio con close-up sul bordo, poi orbit shot a 360°, chiusura con push-in sul logo posteriore.
STILE VISIVO: futuristico, high-tech, colori neon blu/viola, ultra pulito.
LUCE: key light morbida frontale, rim light blu, accenti viola.
AUDIO: musica elettronica energica, colpo di bass nei cambi di inquadratura.
VINCOLI: nessun testo su schermo, nessuna mano, nessuna interfaccia software.
```

### 2.3 Prompt “poveri” vs prompt “regia”

**❌ Esempio povero**

```text
A man walks in a city.
```

**✅ Esempio con regia**

```text
A tall man in a worn leather jacket walks through a rain-soaked
neon-lit Tokyo alley at midnight. He glances over his shoulder, tense.
Medium tracking shot, slight handheld wobble.
Cyberpunk atmosphere, volumetric fog, warm amber street lights
reflecting in puddles.
Sound of rain, distant traffic, his footsteps echo.
```

Regola: scrivi il prompt come se stessi dando **indicazioni a una troupe** (regia, fotografia, suono), non solo “descrivendo un’immagine”.

---

## 3. Sistema di reference `@`

### 3.1 Sintassi base

```text
@Image1    → prima immagine caricata
@Image2    → seconda immagine caricata
@Video1    → primo video caricato
@Audio1    → primo file audio caricato
```

Li userai sempre così:

- per fissare **stile** (palette, look del personaggio, tipo di luce)
- per copiare **camera/movimento** da un video
- per sincronizzare **ritmo** con un audio
- per mantenere **coerenza** di personaggi e ambienti tra più clip

### 3.2 Tabella comandi `@` (rapida)

| Cosa vuoi fare                         | Sintassi tipica                                                |
|----------------------------------------|-----------------------------------------------------------------|
| Fissare primo frame                    | `@Image1 as the first frame`                                   |
| Fissare ultimo frame                   | `@Image2 as the last frame`                                    |
| Usare l’identità di un volto           | `Man @Image1 walks into the office`                            |
| Copiare stile visivo                   | `Reference @Image1 for color and lighting style`               |
| Copiare ambientazione                  | `Reference @Image2 for the setting`                            |
| Copiare camera di un video             | `Reference @Video1's camera movements`                         |
| Copiare coreografia/movimenti          | `Reference @Video1 for the fighting choreography`              |
| Copiare transizioni                    | `Reference @Video1's transitions and timing`                   |
| Estendere un video                     | `Extend @Video1 by 5 seconds`                                  |
| Sostituire personaggio                 | `Replace the person in @Video1 with @Image1`                   |
| Cambiare completamente la trama        | `Subvert the plot of @Video1. [nuova direzione]`               |
| Usare file come voiceover              | `@Audio1 as the character's voice`                             |
| Usare audio come musica/ritmo          | `Use @Audio1 for background music` / `Video rhythm references @Audio1` |
| Copiare SFX da un video                | `Background audio references @Video1's sound effects`          |

### 3.3 Pattern multi-reference potente

```text
@Image1 as the first frame.
Reference @Image2 for the setting.
Man's appearance follows @Image3.
Reference @Video1's camera movements and transitions.
Use @Audio1 for background music.
[Descrizione completa della scena].
```

---

## 4. Parametri controllabili

> Ricorda: `model`, `size`, `seconds` sono esterni. Qui parliamo di **tutto il resto** che puoi controllare davvero.

### 4.1 Parametri da interfaccia (tipici)

| Parametro       | Opzioni tipiche                    | Uso pratico                                                 |
|-----------------|------------------------------------|-------------------------------------------------------------|
| Aspect ratio    | `16:9`, `9:16`, `1:1`, `4:3`, `21:9` | 16:9 YouTube; 9:16 short verticali; 1:1 feed quadrato       |
| Camera mode     | `Fixed` / `Unfixed`               | Usa `Unfixed` se nel prompt descrivi movimenti camera       |
| Frame rate      | ~`24 fps`                         | Look più “cinema”; eventuali alternative dipendono dalla UI |
| Quality         | `720p`, `1080p`, `2K`             | Più alta → più dettagli, ma più sensibile a luce e rumore   |

### 4.2 Parametri via prompt (logici)

| Parametro         | Come lo controlli                     | Esempio                                                |
|-------------------|----------------------------------------|--------------------------------------------------------|
| Intensità movimento | aggettivi + verbi                    | `"runs frantically"` vs `"walks slowly"`           |
| Ritmo / pacing    | parole di tempo                       | `"fast cuts"`, `"slow, deliberate movements"`      |
| Continuità        | esplicitando                          | `"One continuous shot. No cuts."`                    |
| Emozione          | aggettivi emotivi                     | `"subtle fear"`, `"explosive joy"`                 |
| Tipo di taglio    | keyword                               | `lens switch` per cut interni                          |
| Ambiente sonoro   | descrizione                            | `"busy street"`, `"quiet bedroom at night"`        |
| Lingua dialogo    | esplicitare lingua                    | `"He says in Italian: \"...\""`                  |
| Forze fisiche     | descrizione fisica                    | `"tires smoke as car drifts 90°"`                    |
| Voce da volto     | istruzione                             | `"Match voice to appearance"`                        |

### 4.3 Seed, creatività, variazioni (concetto)

- **Seed fisso** → se vuoi rigenerare variazioni coerenti.
- **Seed variabile** → per esplorare tante proposte diverse.
- **Creatività bassa** → più fedeltà a reference e prompt.
- **Creatività alta** → più sorprese, meno controllo.

Pattern operativo:

- **Fase test/ricerca stile**: creatività alta, seed non fissato.
- **Fase produzione in serie**: creatività medio-bassa, seed fissato.

---

## 5. Movimenti camera – vocabolario pratico

### 5.1 Movimenti principali

```text
MOVIMENTI LINEARI
- Dolly in / Dolly out          → la camera avanza/arretra fisicamente
- Tracking shot                 → segue il soggetto lateralmente
- Push in / Pull back           → simile al dolly, in avanti/indietro
- Crane shot                    → camera dall’alto verso il basso (o viceversa)

ROTAZIONI
- Pan left / Pan right          → rotazione orizzontale
- Tilt up / Tilt down           → rotazione verticale
- Orbit shot                    → camera gira attorno al soggetto
- Whip pan                      → pan velocissimo con motion blur

EFFETTI OTTICI
- Zoom in / Zoom out            → zoom ottico, non movimento fisico
- Hitchcock zoom                → dolly in + zoom out (effetto vertigine)
- Rack focus                    → cambio fuoco tra soggetto e sfondo
- Fisheye lens                  → lente grandangolare distorta
- Bokeh background              → sfondo molto sfocato

STILI
- Handheld feel                 → camera a mano, leggero tremolio
- Steadicam                     → movimento fluido e stabile
- Fixed / Static shot           → camera fissa
- Aerial / Overhead / Bird’s eye view → inquadrature dall’alto
- Low angle                     → camera bassa, soggetto dominante

INQUADRATURE
- Extreme close-up (ECU)        → dettaglio estremo (occhi, bocca, oggetto)
- Close-up                      → volto o dettaglio principale
- Medium shot                   → mezzo busto
- Wide / Establishing shot      → inquadratura ampia, contesto
- Over-the-shoulder shot        → spalle in primo piano, soggetto oltre
- POV shot                      → punto di vista soggettivo
- Two-shot                      → due personaggi in campo

TRANSIZIONI
- lens switch                   → taglio narrativo interno al prompt
- Cut to                        → cambio secco di inquadratura
- Fade to black / Fade through  → dissolvenza
- Wings sweep past camera       → elemento che “passa” davanti alla camera per transizione
- Enter scene through [object]  → transizione “attraverso” un oggetto o dettaglio
```

### 5.2 Pattern pronti

- **Viral/dinamico**

  ```text
  Whip pan transitions, fast cuts, handheld energy,
  low angle push-in on subject's face.
  ```

- **Cinematografico**

  ```text
  Slow dolly in from wide establishing shot to close-up.
  Hitchcock zoom when tension peaks.
  Orbit shot for the climax moment.
  ```

- **YouTube talking head**

  ```text
  Fixed medium shot. Slight rack focus between subject and background.
  Clean and stable. Professional studio lighting.
  ```

- **Long take artistico**

  ```text
  One continuous Steadicam shot following the character
  through three different rooms. No cuts.
  Camera moves organically, reacts to character.
  ```

---

## 6. Audio e voiceover

### 6.1 Solo testo (audio generato dal modello)

Descrivi:

- **cosa** si sente (dialoghi, musica, rumori)
- **come** si sente (vicino/lontano, secco/riverberato)
- **da dove** viene (ambiente: strada, studio, chiesa, natura)

**Formato base dialogo**

```text
A man in a suit sits at a boardroom table.
He says in Italian: "Dobbiamo prendere una decisione oggi."
Voice is low, authoritative, urgent.
Ambient office sound, subtle air conditioning hum.
No background music.
```

**Ambienti sonori utili**

```text
Recording studio with treated acoustic panels — close, intimate sound.
Busy street intersection at rush hour — traffic, horns, distant chatter.
Cathedral interior — long natural reverb, echo, distant footsteps.
Small coffee shop — soft background chatter, espresso machine hiss.
Forest clearing at dawn — birds, wind through leaves, small stream.
```

### 6.2 Con file audio di riferimento (`@Audio`)

- **Voiceover già registrato** → `@Audio1 as the narrator's voice`.
- **Musica di riferimento** → `Use @Audio1 for background music and rhythm`.
- **Beat-sync** → tagli e cambi camera seguono ritmo e beat dell’audio.

**Template voice-matching**

```text
@Audio1 as the narrator's voice.
The narration text: "[testo voiceover se vuoi che venga ricreato]".
Deliver with the same pacing and dramatic emphasis as @Audio1.
[Descrizione visiva B-roll che illustra la voce].
```

**Template beat-sync**

```text
Images @Image1 through @Image7 cut to the keyframe positions
and overall rhythm of @Audio1.
Characters in frame are more dynamic.
Add lighting changes between shots. Strong visual impact.
```

### 6.3 Voce da volto (senza audio)

```text
@Image1 as the first frame.
The person in @Image1 speaks naturally in Italian.
She says: "Ho solo bisogno di sapere che stai bene."
Match vocal characteristics to her appearance and expression.
Deliver with a slightly trembling, emotional tone.
```

---

## 7. Stili visivi e lighting

### 7.1 Stili visivi

```text
CINEMATOGRAFICI
- Cinematic 35mm film look
- Anamorphic widescreen, lens flares
- Documentary style, raw and real
- Noir, high contrast, deep shadows
- 70s film grain, New Hollywood
- French New Wave, naturalistic

DIGITALI MODERNI
- Clean commercial aesthetic
- 4K crisp, professional
- Hyperrealistic
- Color graded, teal and orange LUT
- Warm cinematic tones

ANIMAZIONE
- Pixar-quality 3D animation
- Studio Ghibli-inspired hand-drawn
- Anime style
- Stop-motion aesthetic
- Comic book, cel-shaded
- Claymation

SOCIAL / VIRAL
- UGC phone-shot vertical style
- Vlog aesthetic, natural lighting
- TikTok POV
- Found footage, raw and unfiltered
```

### 7.2 Lighting

```text
NATURALE
- Golden hour — warm amber, long shadows
- Blue hour — cool tones, dusk
- Harsh midday sun — hard shadows, high contrast
- Overcast — soft diffused light, no harsh shadows
- Magic hour — warm pink/purple at sunset/sunrise

ARTIFICIALE
- Neon-lit — strong colored practicals
- Volumetric fog with light beams
- Low key — dramatic, Rembrandt-style shadows
- High key — bright, flat, commercial
- Rim / Hair light — light from behind, outlining subject
- Practical lights — lamps, screens, candles, fire as sources

AMBIENTI
- Studio lighting — clean 3-point setup
- Mixed light — interior tungsten + exterior daylight
- Underwater caustics — rippling light on surfaces
- Firelight — warm, flickering orange glow
```

---

## 8. Template pronti per tipo di video

### 8.1 Short virale (TikTok, Reels, Shorts)

- **Ratio**: 9:16
- **Durata**: 5–8 s
- **Obiettivo**: hook immediato + un’idea chiara

```text
OBIETTIVO: short virale verticale che sorprende nei primi 2 secondi.
FORMATO/DURATA: 9:16, 7 secondi.
SOGGETTO: POV, mani che aprono una scatola misteriosa su un tavolo.
AZIONE: al primo colpo la scatola si apre da sola, esce una piccola creatura luminosa.
CAMERA: handheld POV, rapido push-in quando la creatura esce, breve whip pan su reazione del volto riflessa in una superficie.
STILE: TikTok UGC ma con effetto magico credibile.
LUCE: luce naturale da finestra + bagliore blu dalla creatura.
AUDIO: gasp naturale, piccolo suono magico brillante, nessuna musica lunga.
VINCOLI: nessun testo on screen, nessun logo.
```

### 8.2 UGC / contenuti “authentic”

```text
UGC [tipo contenuto] — [contesto quotidiano].
Phone-shot aesthetic, slight handheld shake, natural lighting.
No professional equipment feel. Authentic and unpolished.
[Azioni semplici + dialogo spontaneo in lingua locale].
```

### 8.3 Intro/Outro YouTube

```text
OBIETTIVO: intro di 10 secondi per un canale YouTube di tecnologia.
FORMATO/DURATA: 16:9, 10 secondi.
SOGGETTO: sequenza astratta di circuiti elettronici che si formano nello spazio.
AZIONE: la camera viaggia attraverso chip, cavi e luci fino al logo finale del canale.
CAMERA: inizio con wide shot della “città di circuiti”, poi push-in lungo un tracciato luminoso, chiusura con close-up sul logo che emerge.
STILE: cinematic tech, colori blu/verde, piccoli flare.
LUCE: bagliori interni dai circuiti, sfondo scuro.
AUDIO: musica elettronica crescente, piccolo whoosh quando appare il logo.
VINCOLI: nessun testo randomico, nessun volto umano.
```

### 8.4 Spot prodotto / e-commerce

```text
Commercial for [Nome Prodotto]. "[Tagline]".
Scene 1: Hero shot del prodotto isolato, camera orbit 360°, close-up dettagli.
Scene 2: Lifestyle shot — persona che usa il prodotto in contesto reale.
Scene 3: Packshot finale su fondo pulito con luce morbida.
Clean commercial aesthetic, warm and premium.
Soft, upbeat background music. Optional voiceover in Italian: "[testo]".
Without any text on screen or watermarks.
```

### 8.5 Dialogo / mini short film

```text
[Setting]. [Personaggio A] and [Personaggio B] in [situazione].
[A] says in [lingua]: "[dialogo A]".
[B] responds in [lingua]: "[dialogo B]".
[Azione/gesto chiave].
[A] says: "[linea di chiusura]".
Two-shot and over-the-shoulder coverage. Subtle, cinematic lighting.
Ambient sound fits the room. Optional soft music.
```

### 8.6 Nature / travel / docu

```text
Aerial drone shot over [paesaggio] at [ora del giorno].
Camera slowly glides forward, revealing [elemento forte: lago, città, montagne].
Cut to closer shot of [viaggiatore/animale/elemento].
Epic but gentle orchestral score. Natural ambient sound.
Documentary-style color grading.
```

---

## 9. Workflow pratici completi

### 9.1 Solo testo (text-to-video puro)

1. Definisci: piattaforma, durata, ratio, obiettivo (hook / storytelling / educazione).
2. Scrivi il prompt con la struttura completa (OBIETTIVO → VINCOLI).
3. Genera 2–3 varianti cambiando solo **seed/creatività**.
4. Scegli la migliore, affina con piccole correzioni testuali.

**Mini-template generico**

```text
OBIETTIVO: [tipo video, piattaforma].
FORMATO/DURATA: [ratio, secondi].
SOGGETTO: [chi/cosa].
AZIONE: [cosa succede step-by-step].
SCENA/AMBIENTE: [dove/quando].
CAMERA: [movimenti chiave].
STILE VISIVO: [cinematic / UGC / anime / ecc.].
LUCE: [tipo di luce].
AUDIO: [dialogo? musica? solo ambiente? lingua?].
VINCOLI: [no testo, no logo, no volti, ecc.].
```

### 9.2 Image-to-video (first/last frame, stile, personaggio)

Caso: hai una foto di un personaggio o di un frame forte.

1. Carica la foto come `@Image1` (eventualmente anche `@Image2` come last frame).
2. **Non** ridire nel prompt ciò che vedi nella foto.
3. Descrivi solo **movimento, camera, atmosfera, eventuale dialogo**.

```text
@Image1 as the first frame.
The camera slowly orbits around the character, from a medium shot to a close-up.
Her hair and clothes move gently in a soft breeze.
Keep the same lighting and background as in @Image1.
No cuts. One continuous shot. Soft ambient music only.
```

### 9.3 Video-to-video (copiare camera / ritmo)

Caso: hai un video di riferimento con camera/ritmo perfetti.

1. Carica il video come `@Video1`.
2. Nel prompt specifica chiaramente cosa copiare e cosa cambiare.

```text
Reference @Video1's camera movements and cutting rhythm.
Replace the original scene with a luxury skincare product on a marble table.
Keep the same pacing of cuts and camera arcs from @Video1.
Clean, minimalist background, soft natural window light.
No text on screen.
```

### 9.4 Multimodale con voiceover (video lunghi / YouTube)

1. Monta il **voiceover completo** fuori da Seedance (es. 2–10 minuti).
2. Spezza il voiceover in **blocchi da 10–15 s**.
3. Per ogni blocco:
   - carica l’audio come `@Audio1`
   - se usi un personaggio fisso, carica `@Image1` (volto)
   - scrivi un prompt B-roll che illustra ciò che viene detto in quei 10–15 s
4. Genera tutte le clip e montale sopra la traccia audio completa.

**Template per un blocco**

```text
@Audio1 as the narrator's voice for this 12-second segment.
Show dynamic B-roll of a programmer working in a modern office:
close-ups on hands typing, shots of code on screen (blurred, no readable text),
wide shots of the office with colleagues moving in the background.
Camera slowly pushes in and occasionally tracks sideways.
Clean, natural daylight from large windows.
No talking heads, only B-roll supporting the narration.
```

### 9.5 Multimodale senza voiceover (solo musica o silenzio)

- Se hai **musica**: caricala come `@Audio1` e chiedi beat-sync / cambi camera sui beat.
- Se vuoi **silenzio**: specifica “silent, no ambient sound, no music”.

```text
Use @Audio1 for background music and cutting rhythm.
Fast, energetic edits matching the main beats.
Show quick shots of different athletes training in an urban gym.
Handheld feel, dynamic lighting changes.
No dialogue, only music and subtle workout sound effects.
```

---

## 10. Best practice e limiti pratici

### 10.1 Regole d’oro

1. Scrivi sempre al **presente** (walks, runs, says).
2. Specifica **luce** e **atmosfera**, non solo soggetto e azione.
3. Usa `lens switch` per separare shot all’interno della stessa clip.
4. Non descrivere di nuovo ciò che già dai come immagine/video reference.
5. Quando qualcosa “non esce”:
   - semplifica il prompt
   - esplicita vincoli (`without text on screen`, `no watermarks`)
   - rinforza l’uso delle reference (`Reference @Video1's camera movements`)
6. Per serie di video con lo stesso personaggio:
   - usa SEMPRE la stessa `@Image` del volto
   - ricicla frame generati come nuove reference per aumentare coerenza.
7. Per video lunghi:
   - pensa in **clip da 10–15 s**
   - mantieni costanti: ratio, stile, luce generale, personaggi.

### 10.2 Limiti tipici (da gestire a monte)

- Testo on screen poco affidabile → aggiungi testi e grafica in **montaggio**.
- Lunghezza massima della singola clip → costruisci i contenuti lunghi come **sequenza di clip**.
- Eccesso di reference → massimo una dozzina di file, scegli solo quelli **cruciali** (volti, ambienti, camera, audio).
- Negative prompt stile Stable Diffusion non sempre supportati → usa frasi naturali tipo:
  - `without any text on screen`
  - `no logos or watermarks`
  - `no crowd, only the main character`.

---

*Puoi salvare questo file come `seedance-2.0-guida-completa-v2.md` nella cartella `seedance 2.0` del tuo repo GitHub `istruzioni`.*
