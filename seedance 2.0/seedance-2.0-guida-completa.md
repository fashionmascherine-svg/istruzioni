# 🎬 GUIDA COMPLETA A SEEDANCE 2.0
## Struttura dei Prompt, Parametri e Workflow per Qualsiasi Tipo di Video
### Versione verificata — Febbraio 2026 | ByteDance / Dreamina / Jimeng

> **Note preliminari:**
> - I parametri `model`, `size` e `seconds` sono gestiti esternamente dall'interfaccia o API.
> - Questa guida copre esclusivamente ciò che puoi controllare tramite prompt e configurazione interna.
> - Seedance 2.0 è stato lanciato ufficialmente il **10 Febbraio 2026** da ByteDance.
> - Accessibile su: **Jimeng** (CN), **Dreamina** (International), **WaveSpeed API**

---

## 📌 INDICE

1. [Architettura del Prompt — Formula Universale](#1-architettura-del-prompt)
2. [Modalità di Generazione](#2-modalità-di-generazione)
3. [Sistema di Riferimento @ (Reference System)](#3-sistema-di-riferimento-)
4. [Parametri Disponibili](#4-parametri-disponibili)
5. [Movimenti Camera — Vocabolario Completo](#5-movimenti-camera)
6. [Audio e Voiceover — Guida Completa](#6-audio-e-voiceover)
7. [Stili Visivi e Lighting](#7-stili-visivi-e-lighting)
8. [Template per Tipo di Video](#8-template-per-tipo-di-video)
9. [Prompt Avanzati — Esempi Reali](#9-prompt-avanzati)
10. [Funzionalità Avanzate Uniche di Seedance 2.0](#10-funzionalità-avanzate-uniche)
11. [API Access](#11-api-access)
12. [Best Practices e Limitazioni](#12-best-practices-e-limitazioni)

---

## 1. ARCHITETTURA DEL PROMPT

### Formula Base Universale

```
[SOGGETTO con dettagli visivi] + [AZIONE al presente] + [SCENA/AMBIENTE] + [CAMERA] + [STILE/LUCE] + [AUDIO]
```

### Struttura Completa a Livelli

```
LAYER 1 — SOGGETTO:    Chi/Cosa appare, com'è fatto, vestiti, età, caratteristiche
LAYER 2 — AZIONE:      Cosa fa (presente indicativo), intensità, emozione
LAYER 3 — SCENA:       Dove, quando, ambiente, contesto
LAYER 4 — CAMERA:      Tipo di inquadratura, movimento, transizioni
LAYER 5 — STILE:       Estetica visiva, colori, riferimento cinematografico
LAYER 6 — LUCE:        Sorgente, direzione, temperatura colore
LAYER 7 — AUDIO:       Dialogo, SFX, musica, ambiente sonoro
```

### Esempio Minimo vs Esempio Completo

**❌ Prompt minimo (risultati inconsistenti):**
```
A man walks in a city.
```

**✅ Prompt completo (risultati cinematografici):**
```
A tall man in a worn leather jacket walks through a rain-soaked 
neon-lit Tokyo alley at midnight. He glances over his shoulder, tense. 
Medium tracking shot, slight handheld wobble. 
Cyberpunk atmosphere, volumetric fog, warm amber street lights 
reflecting in puddles. 
Sound of rain, distant traffic, his footsteps echo.
```

---

## 2. MODALITÀ DI GENERAZIONE

### 2A — Text-to-Video (Solo Testo)

**Accesso:** First Frame / Last Frame mode → lascia vuoti i campi immagine

```
[Descrizione soggetto] + [Azione] + [Scena] + [Camera] + [Stile]
```

- Limite prompt: fino a **800 caratteri** (consigliati 30–150 parole)
- Usa il **presente indicativo**: "walks" non "walked"
- Per multi-scena: usa **"lens switch"** per indicare un taglio
- Il modello ha "directorial thinking" autonomo: pianifica camera e visual template da solo

**Esempio Text-to-Video Singola Scena:**
```
A young chef in a white apron tosses flames in a professional kitchen. 
Close-up on his concentrated face, sparks fly around him. 
Warm orange light from the fire. 
Dramatic documentary style. 
Sound of sizzling oil and kitchen noise.
```

**Esempio Text-to-Video Multi-Scena (con "lens switch"):**
```
A detective enters a dark warehouse. Handheld shot, tense music.
Lens switch — close-up of a briefcase on the floor.
Lens switch — his hand reaches for it slowly.
Lens switch — wide shot, a figure steps from the shadows behind him.
Low key lighting, noir atmosphere. Dramatic orchestral sting.
```

---

### 2B — Image-to-Video (Immagine → Video)

**Accesso:** First Frame / Last Frame mode → carica una o due immagini

```
@Image1 as the first frame, [descrivi SOLO movimento e camera, non re-descrivere l'immagine]
```

**Regola d'oro:** Non ridescrivere quello che si vede già nell'immagine.
Descrivi **solo il movimento** e **la camera**.

```
@Image1 as the first frame. Camera slowly zooms in. 
Hair and fabric gently moving in wind. Soft bokeh in background.
```

**Con First + Last Frame (controllo massimo):**
```
@Image1 as the first frame. @Image2 as the last frame.
Smooth dolly forward movement. Character walks toward camera. 
Cinematic fade between environments.
```

**⭐ Feature unica: Voice from Face**
Seedance 2.0 può generare una voce simile a quella reale del personaggio 
**basandosi solo sulla sua foto**, senza bisogno di file audio di riferimento:
```
@Image1 as the first frame. The person speaks naturally.
He says: "Welcome to the future of AI."
Match voice characteristics to the person's appearance.
```

---

### 2C — Video-to-Video (Video di Riferimento)

**Accesso:** Universal Reference Mode

```
Reference @Video1 for [camera movement / fighting choreography / 
style / transitions]. New content: [descrivi il nuovo video]
```

**Modalità principali:**

| Uso | Sintassi |
|-----|---------|
| Replicare camera | `Reference @Video1's camera movements` |
| Estendere il video | `Extend @Video1 by [X] seconds` |
| Sostituire personaggio | `Replace the woman in @Video1 with @Image1` |
| Cambiare la trama | `Subvert the plot of @Video1. [nuova direzione]` |
| Stile visivo | `Reference @Video1's visual style and color grading` |
| Audio da video | `Background audio references @Video1's sound effects` |

---

### 2D — Multimodale Completo (Immagini + Video + Audio + Testo)

**Accesso:** Universal Reference Mode

```
@Image1 as the first frame. 
Reference @Video1 for camera movement and shot language. 
Use @Audio1 for background music rhythm. 
[Descrizione narrativa completa della scena]
```

**⭐ Feature unica: Storyboard Text Reference**
Puoi caricare uno storyboard testuale come riferimento diretto:
```
Reference the following storyboard:
SHOT 1: Wide establishing shot of the city at dusk.
SHOT 2: Close-up on the protagonist's determined face.
SHOT 3: Tracking shot following her as she runs.
SHOT 4: Low angle, she leaps and the camera follows.
Execute each shot with cinematic quality. 
Dramatic orchestral score building throughout.
```

**Limiti di upload:**
- Max **9 immagini**
- Max **3 video** (max 15 secondi totali)
- Max **3 file audio** MP3/AAC/FLAC/WAV (max 15 secondi totali)
- **Limite totale: 12 file** per generazione

---

## 3. SISTEMA DI RIFERIMENTO @

### Sintassi Base

```
@Image1  →  prima immagine caricata
@Image2  →  seconda immagine caricata
@Video1  →  primo video caricato
@Audio1  →  primo file audio caricato
```

### Tabella Comandi @ Completa

| Comando | Funzione | Esempio |
|---------|----------|---------|
| `@Image1 as the first frame` | Imposta il primo fotogramma | `@Image1 as the first frame, camera pulls back slowly` |
| `@Image2 as the last frame` | Imposta il fotogramma finale | `@Image2 as the last frame` |
| `Man @Image1` | Usa l'identità del personaggio | `Man @Image1 walks into the office` |
| `Reference @Image1 for style` | Replica lo stile visivo | `Reference @Image1 for color and lighting style` |
| `Reference @Image1 for the setting` | Replica l'ambiente | `Reference @Image2 for the setting` |
| `Reference @Video1 for camera` | Replica i movimenti camera | `Reference @Video1's camera movements` |
| `Reference @Video1 for motion` | Replica la coreografia | `Reference @Video1 for the fighting choreography` |
| `Reference @Video1 for transitions` | Replica le transizioni | `Reference @Video1's transitions and timing` |
| `Extend @Video1` | Estende il video | `Extend @Video1 by 5 seconds` |
| `Replace person in @Video1 with @Image1` | Sostituzione personaggio | `Replace the woman in @Video1 with @Image1` |
| `Subvert the plot of @Video1` | Cambia la narrativa | `Subvert the plot of @Video1. [nuova direzione]` |
| `@Audio1 as voice` | Voce di riferimento | `@Audio1 as the character's voice` |
| `@Audio1 for background music` | Musica di sfondo | `Use @Audio1 for background music` |
| `@Audio1 for rhythm` | Ritmo per beat-sync | `Video rhythm references @Audio1` |
| `Background audio references @Video1's sound effects` | Effetti sonori da video | `Background audio references @Video1's sound effects` |
| `Reference @Video1's fisheye effect` | Effetto lente specifico | `Reference @Video1's fisheye effect and speaking motion` |

### Pattern Multi-Reference (Combinazioni Avanzate)

```
@Image1 as the first frame. 
Reference @Image2 for the setting.
Man's appearance follows @Image3. 
Reference @Video1's camera movements and transitions.
Use @Audio1 for background music. 
[Narrativa della scena]
```

---

## 4. PARAMETRI DISPONIBILI

> I parametri `model`, `size` e `seconds` sono gestiti esternamente.
> I seguenti sono configurabili tramite prompt o interfaccia.

### Parametri di Configurazione Interfaccia

| Parametro | Opzioni | Note |
|-----------|---------|------|
| **Aspect Ratio** | `16:9` `4:3` `1:1` `3:4` `9:16` `21:9` | 16:9 per YouTube, 9:16 per TikTok/Reels |
| **Camera Mode** | `Fixed` / `Non-Fixed (Unfixed)` | Seleziona "Unfixed" se il prompt include movimenti camera |
| **Frame Rate** | `24 fps` | Standard cinematografico |
| **Quality** | `720p` / `1080p` / `2K` | 2K richiede illuminazione specificata nel prompt |

### Parametri Controllabili Via Prompt

| Parametro | Controllo Prompt | Esempio |
|-----------|-----------------|---------|
| **Intensità movimento** | Aggettivi di intensità | `"roaring madly"` vs `"roaring"` |
| **Ritmo/Pacing** | Descrizione temporale | `"slow, deliberate movements"` / `"rapid cuts"` |
| **Stile audio** | Keyword audio | `"reverb"`, `"muffled"`, `"metallic clink"` |
| **Emozione** | Aggettivi emotivi | `"subtle fear"`, `"explosive joy"` |
| **Lingua dialogo** | Specifica la lingua | `"He speaks in Italian:"` |
| **Tipo di taglio** | `"lens switch"` | Indica un cut all'interno della generazione |
| **Continuità** | `"One continuous shot"` / `"No cuts"` | Per long take |
| **Forze fisiche** | Descrizione fisica esplicita | `"tires smoke as car drifts 90°"` |
| **Ambiente sonoro** | Keyword ambiente | `"recording studio"`, `"cathedral reverb"` |
| **Voce da volto** | `"Match voice to appearance"` | Genera voce da foto senza audio ref |

---

## 5. MOVIMENTI CAMERA

### Vocabolario Camera Completo

```
MOVIMENTI LINEARI:
- Dolly in / Dolly out         → Camera avanza/retrocede fisicamente
- Tracking shot                → Segue il soggetto lateralmente
- Push in / Pull back          → Simile al dolly
- Crane shot                   → Movimento verticale alto→basso o viceversa

ROTAZIONI:
- Pan left / Pan right         → Rotazione orizzontale su asse fisso
- Tilt up / Tilt down          → Rotazione verticale su asse fisso
- Orbit shot                   → Camera ruota attorno al soggetto
- Whip pan                     → Pan rapidissimo, effetto sfocatura

EFFETTI OTTICI:
- Zoom in / Zoom out           → Zoom ottico (non fisico)
- Hitchcock zoom               → Zoom out + dolly in simultanei (effetto vertigine)
- Fisheye lens                 → Lente grandangolare distorta
- Bokeh background             → Sfondo sfuocato, soggetto nitido
- Rack focus                   → Cambio fuoco da soggetto a sfondo o viceversa

STILI:
- Handheld feel                → Effetto camera a mano, leggero tremolio
- Steadicam                    → Movimento fluido, stabilizzato
- Fixed shot / Static shot     → Camera ferma
- Aerial shot / Overhead shot  → Vista dall'alto
- Bird's eye view              → Dall'alto in picchiata
- Low angle                    → Camera bassa, soggetto imponente
- Close-up                     → Dettaglio ravvicinato
- Extreme close-up (ECU)       → Dettaglio estremo (occhi, mani, oggetti)
- Medium shot                  → Mezzo busto
- Wide shot / Establishing shot → Inquadratura larga
- Over-the-shoulder shot       → Spalle del soggetto in primo piano
- POV shot                     → Punto di vista soggettivo
- Two-shot                     → Due personaggi in campo

TRANSIZIONI:
- lens switch                  → Indica un taglio narrativo interno
- Cut to                       → Taglio diretto
- Fade through / Fade to black → Dissolvenza
- Wings sweep past camera for transition → Transizione con elemento fisico
- Enter scene through [object]'s [feature] → Transizione attraverso un oggetto
```

### Esempi Pratici Camera

**Per video viral/dinamico:**
```
Whip pan transition, fast cuts, handheld energy, 
low angle push-in on subject's face.
```

**Per video cinematografico:**
```
Slow dolly in from wide establishing shot to close-up. 
Hitchcock zoom when tension peaks. 
Orbit shot for the climax moment.
```

**Per YouTube/Talking Head:**
```
Fixed medium shot. Slight rack focus between subject and background. 
Clean and stable. Professional studio lighting.
```

**Per long take artistico:**
```
One continuous Steadicam shot following the character 
through three different rooms. No cuts. 
Camera moves organically, responds to character's path.
```

---

## 6. AUDIO E VOICEOVER

### 6A — Audio Auto-Generato (Solo Prompt)

Seedance 2.0 genera audio **nativamente e simultaneamente** al video tramite 
architettura audio-video unificata.
Basta descrivere il suono nel prompt.

**Tipi di audio auto-generati:**
- Dialogo lip-sync in 8+ lingue (IT, EN, ZH, JA, KO, ES, FR, DE, PT)
- Sound effects ambientali (automatic acoustic field simulation)
- Musica di sottofondo
- Suoni fisici (passi, vento, pioggia, oggetti)
- **Environmental Sound** → genera automaticamente l'ambiente sonoro dal contesto visivo

#### Template — Voiceover Auto (Senza File Audio)

**Formato dialogo:**
```
[Nome/descrizione personaggio] says: "[testo esatto del dialogo]"
Deliver with [tono emotivo]. [descrizione visiva della scena].
```

**Esempio completo:**
```
A man in a suit sits at a boardroom table. He leans forward and says: 
"The numbers don't lie. We have exactly 48 hours before this company collapses." 
Voice is low, authoritative, urgent. 
The board members exchange nervous glances. 
Dramatic orchestral sting in background.
```

**Ambiente sonoro (Acoustic Field Simulation):**
```
Recording studio with treated acoustic panels — close, intimate sound.
Busy street intersection at rush hour — ambient noise, traffic, horns.
Cathedral interior — natural reverb, echo, distant footsteps.
Small coffee shop — soft background chatter, espresso machine hiss.
Forest clearing at dawn — birds, wind through leaves, stream in distance.
```

---

### 6B — Voiceover con File Audio di Riferimento (@Audio)

**Formato base:**
```
@Audio1 as the character's voice.
[Personaggio] speaks the dialogue from @Audio1 while [azione visiva].
Natural ambient [ambiente] sounds in background.
```

**Template Voice Matching:**
```
The narrator's voice should match the deep, authoritative timbre from @Audio1. 
The narration text: "[testo del voiceover]"
Deliver with the same pacing and dramatic emphasis as the reference.
[Descrizione visiva delle scene]
```

**Template Beat-Sync con Audio:**
```
Images @Image1 through @Image7 cut to the keyframe positions 
and overall rhythm of @Audio1. 
Characters in frame are more dynamic. 
Add lighting changes between shots. Strong visual impact.
```

**Template Video + Audio Reference:**
```
Reference @Video1's fisheye effect and speaking motion.
Make the character from @Image1 look up at the camera.
Background audio references @Video1's sound effects.
```

---

### 6C — ⭐ Voice from Face (Feature Unica)

Seedance 2.0 può generare una voce verosimile **solo dalla foto** del personaggio,
senza alcun file audio di riferimento:

```
@Image1 as the first frame.
The person in @Image1 speaks naturally in [lingua].
He/She says: "[testo del dialogo]"
Match vocal characteristics to the person's appearance and expression.
Deliver with [tono emotivo: warm / authoritative / gentle / urgent].
```

---

### 6D — Lingue Supportate per Lip-Sync

| Lingua | Codice nel prompt |
|--------|-----------------|
| Italiano | `He speaks in Italian:` |
| Inglese | `She says in English:` |
| Cinese (Mandarino) | `speaks in Mandarin:` |
| Giapponese | `speaks in Japanese:` |
| Coreano | `speaks in Korean:` |
| Spagnolo | `speaks in Spanish:` |
| Francese | `speaks in French:` |
| Tedesco | `speaks in German:` |
| Portoghese | `speaks in Portuguese:` |

**Multi-lingua in un singolo prompt:**
```
Scene 1: Italian man says in Italian: 
"Dobbiamo prendere una decisione oggi."
Lens switch — Japanese partner responds in Japanese: 
"[dialogo in giapponese]"
Lens switch — American CEO says in English: 
"Gentlemen, we're all on the same team."
Over-the-shoulder shots. Professional lighting. 
Subtle tension in body language. 
Ambient office sound, air conditioning hum.
```

---

## 7. STILI VISIVI E LIGHTING

### Stili Visivi Principali

```
CINEMATOGRAFICI:
- Cinematic 35mm film look
- Anamorphic widescreen, lens flares
- Documentary style, raw and real
- Noir, high contrast, deep shadows
- New Hollywood, 70s film grain
- French New Wave, naturalistic

DIGITALI/MODERNI:
- Clean commercial aesthetic
- 4K crisp, professional
- Hyperrealistic
- Color graded, teal and orange LUT
- Warm cinematic tones

ANIMAZIONE:
- Pixar-quality 3D animation
- Studio Ghibli-inspired hand-drawn
- Anime style
- Stop-motion aesthetic
- Comic book, cel-shaded
- Claymation

SOCIAL/VIRAL:
- UGC (User Generated Content) style
- Phone-shot, vertical, authentic
- Vlog aesthetic
- TikTok POV
- Found footage
- Raw, unfiltered, no production value
```

### Lighting Vocabulary

```
NATURALE:
- Golden hour — warm amber, long shadows
- Blue hour — cool tones, dusk
- Harsh midday sun — hard shadows, high contrast
- Overcast — soft diffused light, no shadows
- Magic hour — warm pink/purple tones at sunset/sunrise

ARTIFICIALE:
- Neon-lit — colored practical lights
- Volumetric fog + light beams
- Low key — dramatic shadows, Rembrandt style
- High key — bright, flat, commercial
- Rembrandt lighting — classical portrait, triangle shadow
- Rim light / Hair light — contour light from behind
- Practical lights — motivated by scene (lamps, screens, fire, candles)

AMBIENTI SPECIFICI:
- Studio lighting — clean, professional three-point
- Mixed — interior tungsten + exterior daylight
- Underwater caustics — rippling light patterns
- Firelight — warm, flickering orange
```

---

## 8. TEMPLATE PER TIPO DI VIDEO

### 8A — 🔥 Viral Short (TikTok / Reels / Shorts)

**Aspect Ratio:** 9:16  
**Durata:** 5–10 secondi  
**Camera:** Non-Fixed

```
[Hook visivo immediato — 1 secondo].
[Azione principale dinamica]. 
[Reveal o twist].
POV / Handheld style. Fast cuts. Whip pan transitions.
High energy background music. Viral aesthetic.
```

**Esempio:**
```
POV: You open a mystery box and a tiny dragon flies out. 
It lands on your hand and breathes a small flame. 
Handheld camera, surprised reaction, quick zoom-in on the dragon.
Gasping sound, magical sparkle SFX. TikTok aesthetic.
```

---

### 8B — 📱 UGC / Authentic Content

```
UGC [tipo di contenuto] — [contesto]. 
Phone-shot aesthetic, natural lighting. 
No professional equipment feel. Authentic, unpolished.
[Azione + dialogo genuino]
```

**Esempio:**
```
UGC day-in-the-life of a Gen Z girl in Milan — morning routine, 
espresso at home, getting ready, heading to university.
Phone-shot aesthetic, vertical framing, natural window light.
She says casually in Italian: 
"Okay ragazzi, vi mostro la mia mattina."
```

---

### 8C — 🎬 Cinematic / YouTube Long-Form

**Aspect Ratio:** 16:9 o 21:9  
**Strategia:** Genera più clip da 10–15s, assemblarle in editing

```
SCENE [N]: [Descrizione dettagliata]. 
[Camera movement]. [Lighting]. [Audio/musica].
Lens switch — SCENE [N+1]: [...]
Cinematic color grade. [Mood emotivo complessivo].
```

**Template Narrativo a 3 Atti:**
```
ACT 1 — SETUP:
Establishing wide shot of [luogo]. 
[Personaggio] enters frame from [direzione]. 
[Personaggio] says in [lingua]: "[dialogo di apertura]"
Ambient sound, subtle orchestral score begins.

Lens switch —

ACT 2 — CONFLICT:
Close-up on [dettaglio drammatico]. 
[Azione di conflitto]. Dramatic cut to [reazione].
Music intensifies. Fast handheld cuts.

Lens switch —

ACT 3 — RESOLUTION:
[Risoluzione]. Slow pull back to wide shot.
[Personaggio] says in [lingua]: "[dialogo finale]"
Music swells and fades. Fade to black.
```

---

### 8D — 📣 Commercial / Product Video

```
Commercial for [Nome Prodotto/Brand]. "[Tagline]".
Scene 1: [Scena uso prodotto — hero shot]. 
Close-up details. [Lighting specifico].
Scene 2: [Beneficio visivo — lifestyle shot].
Scene 3: [Closing frame con prodotto e brand].
Professional studio lighting. Clean commercial aesthetic.
Upbeat [tipo] background music. 
Voiceover in [lingua]: "[Testo voiceover]"
```

**Esempio:**
```
Commercial for a premium Italian espresso brand. 
"Taste the tradition."
Scene 1: Barista's hands expertly pulling an espresso shot. 
Close-up on crema forming. Warm, intimate coffee shop.
Scene 2: A couple at a table, first sip reaction — eyes close, smiles.
Scene 3: Product packaging on marble counter, soft morning light.
Elegant orchestral music. 
Voiceover in Italian: 
"Ogni tazza è una storia. Scopri il gusto autentico."
Cinematic color grade, warm tones.
```

---

### 8E — 🎭 Dialogo / Short Film

```
[Setting]. [Personaggio A] and [Personaggio B] in [situazione].
[A] says in [lingua]: "[dialogo A]"
[B] responds in [lingua]: "[dialogo B]"
[Azione o momento di tensione/emozione]
[A] says in [lingua]: "[dialogo climax]"
[Descrizione visiva conclusiva].
[Camera work]. [Mood/stile].
```

**Esempio:**
```
A dimly lit detective office, rain against the window. 
A hard-boiled detective sits across from a nervous client.
Detective says in English: "You didn't come here to talk about the weather."
Client leans forward, voice shaking: "My husband isn't who I think he is."
Detective's expression hardens. He opens a drawer.
Detective says: "Tell me everything."
Two-shot over-the-shoulder framing. Film noir style. 
Jazz piano music in background. Rain sound throughout.
```

---

### 8F — 🌍 Nature / Travel / Documentary

```
[Tipo di paesaggio]. [Elemento naturale in azione].
[Clima e ora del giorno]. [Fauna se presente].
Drone aerial shot / Epic wide shot.
[Stile documentaristico].
[Narrazione ambientale: suoni naturali + musica epica].
```

**Esempio:**
```
Aerial drone shot over the Dolomiti mountains at golden hour.
Snow-capped peaks catch the last light, valleys fill with shadow.
An eagle glides below the drone, wings spread wide.
Epic orchestral score. Wind sound. 
BBC Natural World documentary cinematography style. 
Anamorphic 21:9. Ultra-wide establishing shot.
```

---

### 8G — 🎥 One-Take / Long Shot (No Cuts)

```
[Soggetto e punto di partenza].
One continuous tracking shot: [sequenza di azioni e spostamenti].
Camera follows through [ambiente 1], past [elemento], 
into [ambiente 2], ending with [finale visivo].
No cuts. Steadicam. [Musica continua].
```

**Esempio:**
```
Spy thriller style. @Image1 as first frame.
Front-facing tracking shot of a woman in a red coat walking forward. 
Full shot following her. Pedestrians repeatedly block the frame. 
She reaches a corner, camera pans to follow her. 
Fixed shot as she exits frame, disappears around corner. 
Camera pushes forward toward the building. 
No cuts. One continuous take. Tense orchestral score.
```

---

### 8H — 🔄 Video Estensione / Sequel

```
Extend @Video1 by [X] seconds.
Scene 1: [Prima nuova scena dopo il finale del video originale].
Lens switch — Scene 2: [Seconda nuova scena].
Maintain character consistency with @Video1.
Same visual style and color grading as @Video1.
```

---

### 8I — 🎵 Music Video / Beat-Sync

```
Images @Image1 through @Image[N] cut to the 
keyframe positions and overall rhythm of @Audio1.
Characters in frame are more dynamic and expressive.
Overall style: [estetica]. Strong visual impact.
Add dramatic lighting changes between shots.
Adjust framing for visual flow and music sync.
```

---

### 8J — 🏋️ Action / Sports / High Motion

```
[Atleta/personaggio]. [Tipo di sport/azione].
Physically accurate simulation. 
[Sequenza di movimenti difficili descritta step-by-step].
Slow motion on key impact moment. 
[Camera: handheld / low angle / orbit].
Crowd noise / ambient sport sound.
[Stile: broadcast sports / cinematic / documentary].
```

**Esempio (basato su feature ufficiale Seedance 2.0):**
```
Pair figure skaters on Olympic ice rink. 
Synchronized takeoff, mid-air spin, precise landing together. 
Physically accurate movement, no glitches.
Full shot maintaining both skaters. 
Slow motion during the spin. 
Camera orbits during the jump sequence.
Olympic broadcast style. Crowd cheering ambient sound. 
Orchestral classical music throughout.
```

---

## 9. PROMPT AVANZATI — ESEMPI REALI

### Scena d'Azione con Multi-Reference

```
Reference @Image1 for the man's appearance in @Image2's 
elevator setting. Fully replicate @Video1's camera movements 
and the protagonist's facial expressions. 
Hitchcock zoom when startled, then several orbit shots 
inside the elevator. Doors open, tracking shot following him out. 
Exterior scene references @Image3, man looks around. 
Reference @Video1's multi-angle following shots 
tracking his line of sight.
```

---

### Video con Sostituzione Personaggio

```
Replace the person in @Video1 with the girl in @Image1. 
Replace the background CG with an angel referencing @Image2. 
When the girl crouches, wings grow from her back. 
Wings sweep past camera for transition. 
Reference @Video1's camera work and transitions. 
Enter the next scene through the angel's pupil. 
Aerial shot spiraling, camera descends following the angel's face, 
pulls back on arm raise. One continuous shot throughout.
```

---

### Video Commerciale con Estensione

```
Extend @Video1 by 10 seconds. 
Reference @Image1 for the product appearance.

Scene 1: Side shot, product launches into frame dramatically, 
slow motion impact.

Scene 2: Close-up of product details, rotating 360°. 
Clean white background. Professional studio lighting.

Scene 3: Lifestyle shot — person uses product naturally. 
Final close-up product shot. Fade to white.
Upbeat electronic music. 
Voiceover in Italian: "[Testo voiceover]"
```

---

### Dialogo Multi-Lingua Professionale

```
Corporate conference room, morning.
Italian executive says in Italian: 
"Dobbiamo prendere una decisione oggi."
Lens switch — Japanese partner responds in Japanese: 
"[Risposta in giapponese]"
Lens switch — American CEO says in English: 
"Gentlemen, we're all on the same team."
Over-the-shoulder shots. Professional lighting. 
Subtle tension in body language. 
Ambient office sound, air conditioning hum.
```

---

### Scena Emotiva con Voice from Face

```
@Image1 as the first frame.
A woman sits alone at a kitchen table at night. 
She speaks quietly into a phone in Italian: 
"Ho solo bisogno di sapere che stai bene."
Her voice trembles slightly. Match voice to her appearance in @Image1.
Tears forming in her eyes. 
Close-up on hands gripping the phone. 
Natural kitchen light, single lamp, rest in shadow. 
Ambient sound: distant rain, refrigerator hum. No background music.
```

---

### Storyboard Testuale come Reference

```
Execute this storyboard:

SHOT 1 (0-3s): Aerial establishing shot, camera descends over foggy mountains at dawn.
SHOT 2 (3-6s): Medium shot, lone traveler with backpack on a mountain path.
SHOT 3 (6-9s): Close-up on worn boots, footsteps on gravel.
SHOT 4 (9-12s): Wide shot, traveler reaches summit, arms spread wide.
SHOT 5 (12-15s): POV from summit — endless mountains in morning light.

Lens switches between each shot.
Cinematic grade, desaturated with warm highlights.
Epic ambient orchestral score. Wind SFX.
Documentary/adventure style.
```

---

## 10. FUNZIONALITÀ AVANZATE UNICHE

### 🧠 Directorial Thinking
Seedance 2.0 ha pensiero registico autonomo — pianifica camera language,
template visivi e shot sequence da solo se non specificati nel prompt.
Per override completo: specifica ogni shot esplicitamente.

### 🎙️ Environmental Sound (Acoustic Field Simulation)
Il modello genera automaticamente suoni ambientali coerenti con il visivo:
- Città → traffico, voci, clacson
- Foresta → uccelli, vento, rami
- Oceano → onde, gabbiani, vento marino
- Ufficio → AC, tastiere, voci lontane
Per disabilitare: `"Silent, no ambient sound. Music only."`

### 🏃 Physical Accuracy Engine
Motore fisico migliorato per:
- Acrobazie sportive complesse (pattinaggio sincronizzato, arti marziali)
- Interazioni fisiche tra personaggi
- Fluidi, fumo, fuoco, tessuti
Usa descrizioni fisiche esplicite per massima accuratezza.

### 📝 Text Storyboard Reference
Puoi usare uno storyboard testuale scritto come reference diretto nel prompt.

### 🔄 Character/Background Replacement
Sostituisci personaggi o sfondi mantenendo movimenti e camera dal video originale:
```
Replace the [person/background] in @Video1 with [nuovo elemento].
Maintain all camera movements and timing from @Video1.
```

### 🎭 Multi-Shot Narrative (lens switch)
Genera sequenze multi-shot in una singola generazione usando `lens switch` 
come marker di taglio narrativo interno.

---

## 11. API ACCESS

Seedance 2.0 offre **API REST** per utenti Pro ed Enterprise:

```
Endpoint: REST API
Autenticazione: API Key
Modalità: Text-to-Video, Image-to-Video
Job type: Async (webhook-based)
Parametri API: model, size, seconds, prompt, image_url, aspect_ratio
```

Documentazione ufficiale disponibile su: WaveSpeed.ai / Dreamina Developer Portal

---

## 12. BEST PRACTICES E LIMITAZIONI

### ✅ Regole d'Oro

1. **Usa il presente indicativo** — `"walks"` non `"walked"` o `"will walk"`
2. **Specifica l'intensità** — `"roaring madly"` non solo `"roaring"`
3. **Descrivi le forze fisiche** — `"tires smoke as car drifts 90°"` non `"car turns"`
4. **Specifica sempre la luce** — senza luce specificata, 2K è sprecato
5. **Usa "lens switch"** per indicare cut narrativi interni
6. **Sii esplicito con gli @** — `"Reference @Video1's camera movement"` non solo `"use @Video1"`
7. **Non ridescrivere l'immagine** — con @Image1 come first frame, descrivi solo movimento e camera
8. **Seleziona i file strategicamente** — limite 12 totali, scegli gli asset più impattanti
9. **"No cuts. One continuous take."** per long take cinematografici
10. **Includi keyword audio** — `"reverb"`, `"muffled"`, `"metallic clink"` guidano il motore audio
11. **Non usare negative prompts** — usa esclusioni naturali: `"without text on screen"`, `"no watermarks"`
12. **Camera Mode "Unfixed"** — selezionalo sempre quando includi movimenti camera nel prompt
13. **Aggiungi la lingua** — specifica sempre la lingua per dialoghi lip-sync accurati

---

### ⚠️ Limitazioni Note

| Limitazione | Descrizione | Workaround |
|-------------|-------------|------------|
| Testo on-screen | Testo/loghi distorto o illeggibile | Aggiungere in post-produzione |
| Diagrammi precisi | Formule/grafici imprecisi | Usare schermi generici |
| Voice cloning famosi | Non replicabile per policy | Usa @Audio di riferimento generico |
| Tempo di generazione | Clip 15s multi-scena: fino a 10 min | Pianifica in anticipo |
| Lunghezza max per clip | 15 secondi | Assembla clip in editor esterno |
| Negative prompts | Non supportati | Usa esclusioni in linguaggio naturale |
| File limit | Max 12 file totali | Prioritizza gli asset chiave |
| Audio format | MP3, AAC, FLAC, WAV | Max 15 secondi per clip audio |

---

### 🔄 Workflow per Contenuto YouTube Lungo

Per video YouTube da 2–10 minuti, la strategia ottimale è:

```
1. SCRIVI lo script in scene da 10–15 secondi ciascuna
2. GENERA ogni scena separatamente con prompt coerenti
3. MANTIENI consistenza: usa gli stessi @Image per i personaggi in ogni clip
4. USA "lens switch" per sotto-scene dentro una singola generazione
5. ASSEMBLA in CapCut / DaVinci Resolve / Premiere Pro
6. AGGIUNGI audio/voiceover globale in post se necessario
7. COLORE GRADE finale per coerenza tra clip
```

**Template prompt per consistenza personaggio su più clip:**
```
Man @Image1 [azione diversa per ogni clip]. 
Same character, same clothing, same environment as previous clip.
[Camera diversa per varietà]. Maintain visual style consistency.
Same color grade throughout.
```

---

### 📊 Formato Prompt per Aspect Ratio

| Piattaforma | Ratio | Stile Prompt Consigliato |
|-------------|-------|--------------------------|
| YouTube | 16:9 | `Cinematic widescreen, establishing shots` |
| TikTok / Reels / Shorts | 9:16 | `Vertical framing, subject centered, phone aesthetic` |
| Instagram Post | 1:1 | `Square composition, subject dominant, minimal background` |
| Cinema | 21:9 | `Anamorphic, ultra-wide, epic landscape` |
| Portrait/Story | 3:4 | `Portrait-oriented, close-mid shot range` |

---

### 📐 Confronto Seedance 2.0 vs Competitor (Febbraio 2026)

| Feature | Seedance 2.0 | Kling 3.0 | Veo 3.1 | Sora |
|---------|-------------|-----------|---------|------|
| Durata max | 15s | 15s | 8s (ext. 60s+) | 60s |
| Audio nativo | ✅ Upload + reference | ✅ Nativo + lip-sync | ✅ Nativo | Solo testo |
| Lingue lip-sync | 8+ | 5 | Limitato | — |
| Multi-reference | 12 file | Limitato | No | No |
| Voce da foto | ✅ | ❌ | ❌ | ❌ |
| Storyboard text ref | ✅ | ❌ | ❌ | ❌ |
| Physical accuracy | Alta | Media | Alta | Media |
| API access | Pro/Enterprise | Sì | Sì | Sì |

---

*Guida creata e verificata — Febbraio 2026*  
*Basata su: ByteDance Seed Official Blog, WaveSpeed.ai, Freepik Blog, JXP.com, Morphic.com*  
*Piattaforme: Dreamina (International) | Jimeng (CN) | WaveSpeed API*
