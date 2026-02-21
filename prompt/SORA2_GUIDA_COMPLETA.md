# 🎬 SORA 2 — GUIDA COMPLETA AL PROMPT ENGINEERING
### Edizione Febbraio 2026 | Basata su OpenAI Cookbook Ufficiale + Ricerca Avanzata
> ⚙️ I parametri API (`model`, `size`, `seconds`) sono gestiti **esternamente** e NON fanno parte del prompt testuale.

---

## 📌 FILOSOFIA DI BASE

Pensa al prompt come al briefing che dai a un **direttore della fotografia** che non ha mai visto il tuo storyboard. Se lasci vuoti, lui improvvisa — e potrebbe non essere quello che hai in testa. Ma lasciare spazio creativo è altrettanto potente.

| Approccio | Risultato |
|---|---|
| **Prompt dettagliato** | Controllo e coerenza elevati |
| **Prompt leggero** | Creatività libera, risultati sorprendenti |

**Regola d'oro:** Lo stesso prompt usato più volte produce risultati DIVERSI. Questo è una feature, non un bug. Itera sempre su 2–3 varianti.

---

## ⚠️ VERITÀ SULLA CONSISTENZA DEL PERSONAGGIO

> **IMPORTANTE: il solo prompt testuale NON garantisce consistenza del personaggio tra più generazioni separate.**

Ogni generazione Sora 2 è **indipendente e stocastica**. Il modello re-interpreta il testo ogni volta da zero. Un prompt identico inviato due volte produce due personaggi diversi.

### Gerarchia reale dei metodi di consistenza

| Metodo | Consistenza stimata | Disponibilità |
|---|---|---|
| **Cameo** (likeness personale) | ~95% | Solo pannello web, previo setup |
| **Image-to-Video (I2V)** | ~85-90% | Pannello web + API con image reference |
| **Storyboard** (Sora 2 Pro) | ~80-85% | Sora 2 Pro, multi-shot in unica gen |
| **Last-frame stitching** (I2V chain) | ~75-80% | Pannello web + API |
| **Core Prompt testuale** (solo testo) | ~40-60% | Pannello web + API |

**Conclusione pratica:**
- Se usi il pannello o API **solo testo** → la consistenza è parziale e non garantita
- Il **Core Prompt testuale** è il MEGLIO che puoi fare senza immagini di riferimento
- Per consistenza alta → serve **I2V** o **Cameo**

---

## 🔑 METODI DI CONSISTENZA — TUTTI I DETTAGLI

### Metodo 1: Cameo (solo pannello web)

Cameo è la feature più affidabile. Registri un breve video di te stesso o del soggetto, Sora crea un "digital likeness" persistente.

```
Come usarlo nel prompt:
"[Cameo: nome_personaggio] turns toward the camera and speaks."

Regole Cameo:
- Mantieni vestiti e accessori esplicitati nel prompt anche con Cameo
- Specifica: "same outfit as previous scene" per continuità abbigliamento
- Cameo gestisce la faccia, NON il costume — quello va sempre descritto
- Max affidabilità su clip < 20 secondi
```

> ⚠️ Nota Jan 2026: OpenAI ha rimosso l'upload diretto di volti di terze parti. Cameo funziona solo per il proprio likeness verificato.

---

### Metodo 2: Image-to-Video (I2V) — Raccomandato via API

Fornisci un'immagine di riferimento del personaggio. Sora estrae le feature visive e le usa come vincolo durante la generazione.

```
API call con I2V:
{
  "model": "sora-2",
  "prompt": "[descrivere SOLO le azioni, NON l'aspetto]",
  "image": "[base64 o URL immagine reference]",
  ...
}

Cosa descrivere nel prompt I2V:
- NON ridescrivere l'aspetto (ci pensa l'immagine)
- Descrivi SOLO: azione, movimento, camera, luce, ambiente, audio
- Esempio: "The character turns their head slowly to the right,
  looking at something off-screen with curiosity. Subtle smile forming.
  Indoor lighting, shallow depth of field. Soft ambient sound."
```

**Immagine reference ideale:**
- Risoluzione: 1024x1024 o superiore
- Soggetto: viso ben illuminato, features visibili
- Background: semplice, non distrattivo
- Formato: PNG o JPEG alta qualità

**Last-frame stitching (I2V chain):**
```
Workflow per video lunghi:
1. Genera Clip 1 (T2V o I2V)
2. Esporta l'ULTIMO FRAME di Clip 1 come PNG
3. Usa quel frame come image reference per Clip 2
4. Ripeti: ultimo frame di Clip 2 → reference per Clip 3
5. Monta tutto in post-produzione

Vantaggio: la luce, il costume e l'ambiente "ereditano" dallo shot precedente
Limite: piccole derive accumulate dopo 4-5 clip
```

---

### Metodo 3: Storyboard (Sora 2 Pro, pannello web)

Permette di definire più shot in una singola generazione. Il modello mantiene consistenza interna perché è una sola elaborazione.

```
Struttura storyboard:

Card 01 | [durata]s | Purpose: Establish
[descrizione shot 1]

Card 02 | [durata]s | Purpose: Develop
[descrizione shot 2]

Card 03 | [durata]s | Purpose: Resolve
[descrizione shot 3]

Nota: ogni card può avere shot/camera diversi
ma il personaggio rimane consistente nell'intera generazione.
```

---

### Metodo 4: Core Prompt Testuale (solo testo, pannello o API)

Quando non hai immagini e non puoi usare Cameo, questo è il meglio possibile.
Ottieni ~40-60% di consistenza — non perfetta, ma gestibile con selezione.

**Come costruire un Core Prompt efficace:**

```
Step 1: Genera una descrizione ultra-dettagliata del personaggio
(puoi usare ChatGPT con questo prompt META):

"I'm working on a video using Sora 2. Write a very detailed core prompt
that describes ONLY the appearance, voice, and camera settings of [personaggio].
This will be reused across multiple scene prompts. Do NOT include pose or action.
Describe:
1. Character appearance: face, outfit, proportions, colors, overall style
2. Voice: tone, pitch, emotion, delivery, atmosphere
3. Camera: lens, aperture, lighting, color grading, framing style
Be as specific as possible."

Step 2: Salva il Core Prompt risultante
Step 3: Incollalo IDENTICO all'inizio di OGNI generazione separata
Step 4: Aggiungi DOPO il core prompt la descrizione della scena specifica
```

**Struttura del prompt con Core Prompt:**
```
[CORE PROMPT - identico in ogni clip]
Character: [nome] is a [età] [genere], [capelli: colore, lunghezza, stile],
[occhi: colore, forma], [incarnato], [corporatura].
Outfit: [capo superiore + colore + materiale], [capo inferiore], [scarpe],
[accessori specifici: ogni dettaglio conta].
Voice: [tono, pitch, emozione, ritmo].
Camera: [focale, DOF, grade, stile illuminazione].

[SCENE PROMPT - specifico per ogni clip]
[Descrizione scena + azione + camera + luce + audio]
```

**Regola "Genera 3, Scegli 1":**
Con il metodo solo testo, genera sempre 3 varianti per ogni shot
e seleziona quella più consistente. Il 33% di hit rate è normale.
Non riscrivere tutto — rigenera lo stesso prompt finché ottieni il risultato.

---

## 🧱 ARCHITETTURA UNIVERSALE DEL PROMPT

```
[BLOCCO 0 — CORE PROMPT PERSONAGGIO (se presente e solo testo)]
(copiato identico da ogni clip della stessa serie)

[BLOCCO 1 — STILE VISIVO]
(prima riga: definisce l'estetica dominante dell'intero video)

[BLOCCO 2 — PROSA DESCRITTIVA]
(scena, ambiente, atmosfera — 3-8 righe specifiche)

Cinematography:
Camera shot:      [inquadratura + angolo]
Camera movement:  [movimento preciso]
Depth of field:   [shallow / deep + dettagli]
Lens:             [focale e filtri]
Mood:             [tono generale]

Lighting:
Key:              [fonte principale + direzione + ora]
Fill:             [luce di riempimento]
Rim/Edge:         [luce di contorno]
Palette anchors:  [3-5 colori ancora]
Grade:            [tipo di color grade]

Actions:
- [Beat 1: azione specifica con timing]
- [Beat 2: evoluzione dell'azione]
- [Beat 3: climax o cambio]
- [Beat N: chiusura o freeze frame]

Dialogue:         ← OMETTI se senza dialogo
- Personaggio A: "frase breve, naturale"
- Personaggio B: "risposta"

Background Sound:
[ambient 1]; [ambient 2]; [SFX specifici]. [istruzioni musica o "No score."]

Constraints:
[negation layer: cosa il modello NON deve fare]
```

---

## 🎨 BLOCCO 1 — STILE VISIVO

### Stili predefiniti (trigger)

| Categoria | Stile | Trigger consigliato |
|---|---|---|
| **Cinema** | Hollywood drammatico | `Cinematic 4K, anamorphic 2.0x lens, teal-orange grade` |
| **Cinema** | Film IMAX | `IMAX aerial, sharp horizon, epic scale, digital clarity` |
| **Cinema** | Indie bassa luce | `35mm handheld, natural grain, low-key lighting, muted palette` |
| **Vintage** | Anni '70 | `1970s film, 35mm, natural lens flares, warm halation, gate weave` |
| **Vintage** | Anni '90 | `1990s handheld camcorder, VHS grain, oversaturated colors` |
| **Vintage** | 16mm doc | `16mm black-and-white documentary, high contrast, raw grain` |
| **Documentario** | Reportage moderno | `Documentary handheld, ENG camera, natural light, no grade` |
| **Social/Viral** | Short-form mobile | `iPhone shot, vertical format, social media aesthetic, warm filter` |
| **Social/Viral** | Reels style | `TikTok-style, fast cuts implied, bright saturated, quick zoom` |
| **Animation** | 2D/3D ibrido | `Hand-painted 2D/3D hybrid, soft brush textures, warm tungsten` |
| **Animation** | Stop-motion | `Stop-motion feel, tactile textures, storybook aesthetic` |
| **Commerciale** | Product ad | `Commercial clean, white key, sharp product focus, minimal BG` |
| **Musicale** | Music video | `Music video aesthetic, bold color contrast, stylized motion` |
| **YouTube** | Tutorial/Vlog | `Natural vlog style, 50mm lens, soft window light, warm and approachable` |
| **YouTube** | Cinematic long-form | `Cinematic YouTube, 85mm, shallow DOF, professional grade` |
| **Natura** | Wildlife/Natura | `National Geographic, ultra HD nature, golden hour, aerial tracking` |
| **UGC/Ads** | User Generated Content | `UGC style, handheld selfie cam, authentic, slightly imperfect, natural` |

---

## 📷 CINEMATOGRAFIA COMPLETA

### Shot Types

| Codice | Descrizione | Uso tipico |
|---|---|---|
| `ELS` | Paesaggio dominante, soggetto minuscolo | Natura, aperture sceniche |
| `WS` | Contesto e setting, soggetto visibile | Apertura di scena |
| `MS` | Dalla vita in su | Conversazioni, YouTube |
| `MCU` | Spalle e sopra | Emozione, narrativa |
| `CU` | Solo viso | Dramma, reazione |
| `ECU` | Dettaglio singolo (occhi, mani) | Tensione, dettaglio |
| `OTS` | Da dietro spalla del soggetto | Dialogo, punto di vista |
| `POV` | Soggettiva del personaggio | Immersione |
| `Two-shot` | Due soggetti nel frame | Interazione |
| `Aerial wide` | Dall'alto, drone-like | Ambientazione epica |
| `Bird's eye` | Zenitale, 90° verso il basso | Geometria, pattern |
| `Worm's eye` | Dal basso verso l'alto | Potere, grandiosità |

### Camera Angles

```
eye level          → neutro, quotidiano, identificativo
low angle          → potere, grandiosità, minaccia
high angle         → vulnerabilità, contesto, sorveglianza
Dutch tilt         → instabilità, disagio psicologico
slight angle from behind → tensione narrativa, distanza emotiva
```

### Camera Movements

| Movimento | Descrizione | Effetto emotivo |
|---|---|---|
| `dolly-in` | Camera si avvicina al soggetto | Intensità, focus emotivo |
| `dolly-out` | Camera si allontana | Rivelazione, isolamento |
| `tracking shot` | Segue il soggetto in movimento | Dinamismo |
| `pan left/right` | Rotazione orizzontale su asse fisso | Rivelazione laterale |
| `tilt up/down` | Rotazione verticale su asse fisso | Grandiosità / intimità |
| `slow arc around subject` | Orbita intorno al soggetto | Esposizione a 360°, epico |
| `slow crane up` | Salita verticale della camera | Rivelazione progressiva |
| `handheld micro-shake` | Tremore minimo | Realismo, documentario |
| `Steadicam` | Fluidità con lievi oscillazioni | Cinema moderno |
| `static / locked-off` | Nessun movimento | Tensione, contemplazione |
| `drone-like ascent` | Salita aerea progressiva | Scala, grandiosità |
| `whip pan` | Pan ultra-rapido con motion blur | Transizione energica |

### Lenti & Filtri

```
# Focali
24mm wide angle          → grande angolo, distorsione prospettica
32mm spherical prime     → wide naturale, ampio contesto
50mm lens aesthetic      → ottica dell'occhio umano, neutro
85mm, shallow DOF        → ritratto, bokeh naturale, elegante
135mm telephoto          → compressione prospettica, sfondo mosso
anamorphic 2.0x          → widescreen cinematografico, flare orizzontali

# Filtri
Black Pro-Mist 1/4       → ammorbidisce gli aloni, tocco cinematografico
Black Pro-Mist 1/2       → più intenso, pelle morbida, vintage
CPL filter               → gestisce riflessi su vetro e acqua
No filtration            → clean, documentaristico, digitale puro
```

---

## 💡 LUCE & COLORE

### Struttura della luce (3 punti)

```
Key light:   [fonte principale — direzione, qualità, colore]
Fill light:  [riduce ombre dure — caldo/freddo, intensità]
Rim/Edge:    [contorno del soggetto — separa da BG]
```

### Fonti di luce

| Fonte | Trigger | Ora/Contesto |
|---|---|---|
| Sole diretto basso | `low angle sunlight, golden hour` | Alba/Tramonto |
| Sole diretto alto | `harsh noon sunlight, overhead` | Mezzogiorno |
| Luce diffusa | `overcast diffused light, no shadows` | Nuvoloso |
| Finestra naturale | `soft window light from camera left` | Interno giorno |
| Luce artificiale calda | `warm tungsten practical, 3200K` | Interno sera |
| Luce fredda neon | `cool neon spill, blue-green cast` | Urbano notturno |
| Backlit | `strong backlight, silhouette effect` | Drammatico |
| Golden hour | `warm golden key, low angle amber` | Romantico, epico |
| Blue hour | `cool blue ambient, twilight` | Malinconico |
| Volumetric | `volumetric light rays, dust particles` | Atmosferico |

### Palette Colore

```
Palette anchors: [colore 1], [colore 2], [colore 3], [colore 4]
Grade: [nome del look]

# Look comuni:
Teal-orange commercial    → teal in ombre, arancio su skin
Warm Kodak               → giallo/ambra su tutto, ombre marroni
Fuji cool                → mids freddi, pelle lievemente desaturata
Desaturated noir         → quasi B&W, alto contrasto
Warm vintage             → sepia lieve, grain, vignette
Clean digital            → neutro, nessun grade evidenziato
Nordic cool              → blu-grigio dominante, luce piatta
```

---

## 🎬 AZIONI & TIMING

> **Una camera move + Una azione soggetto = Un shot**

### Beat per 12 secondi

```
Actions (12s timeline):
- 0-3s:   [Beat 1 — stabilimento della scena o azione iniziale]
- 3-6s:   [Beat 2 — sviluppo, cambio o reazione]
- 6-9s:   [Beat 3 — climax, dialogo o punto di massima tensione]
- 9-12s:  [Beat 4 — risoluzione, chiusura, freeze o cut implicito]
```

### SPECIFICO vs VAGO

| ❌ Vago | ✅ Specifico |
|---|---|
| `Person walks across room` | `Actor takes four steps to the window, pauses, pulls the curtain in the final second` |
| `Car drives fast` | `Sports car accelerates through wet corner, tires spray water at apex` |
| `Person is emotional` | `Her jaw tightens, eyes glisten, she turns away before a tear falls` |
| `Robot malfunctions` | `Robot's left arm jolts twice, steam vents from chest, eyes flicker from blue to red` |

### Verbi efficaci

```
MOVEMENT:   strides, lunges, pivots, drifts, stumbles, glides, freezes
GESTURE:    reaches for, grabs, releases, taps, traces, lifts, drops
REACTION:   flinches, recoils, leans in, tilts head, exhales slowly
GAZE:       eyes flick to, glances over shoulder, stares directly at lens
TRANSITION: turns toward camera, steps into shadow, exits frame right
```

---

## 🔊 AUDIO & DIALOGO

### Regole dialogo per durata

| Durata | Max battute | Note |
|---|---|---|
| 4 secondi | 1-2 battute brevi | Max 8-10 parole totali |
| 8 secondi | 3-4 battute | Frasi naturali |
| 12 secondi | 4-5 battute | Pause incluse, tono specificato |

### Blocco dialogo

```
Dialogue:
- [PersonaggioA]: "[frase breve]" (tono: urgente/calmo/etc.)
- [PersonaggioB]: "[risposta]"

# Voiceover off-screen:
Voice (VO): "[testo]"

# Narrazione documentaristica:
Narrator (VO, calm, authoritative): "[testo]"
```

### Toni vocali

```
whispered / sotto voce     → intimità, segreto
urgent / tense             → conflitto, urgenza
calm / measured            → autorità, controllo
excited / breathless       → gioia, sorpresa
commanding / assertive     → leadership, potere
monotone / flat            → distanza emotiva
broken / trembling         → vulnerabilità, dolore
```

### Background Sound

```
Background Sound:
[ambient principale]; [suono secondario];
[SFX specifico]; ["No score." o indicazione musicale]

# Intensità:
faint / distant    → appena percettibile
crisp / sharp      → primo piano, definito
muffled            → filtrato, da lontano
low hum            → continuo, atmosferico

# LUFS:
ambient at -20 LUFS, no score
```

---

## ⚡ EFFETTI VISIVI & TEXTURE

```
# Grana film
fine grain overlay / 35mm film grain / 16mm grain high contrast

# Ottica
subtle halation on speculars / lens flare / anamorphic flares
soft vignette / barrel distortion

# Atmosfera
volumetric light rays / dust particles in sunlight
heat shimmer / fog layer / rain droplets on lens
steam / exhaust drift

# Movimento
motion blur on fast movement
slow motion (specifica quale azione)
ramping speed (slow to fast)
```

---

## 🛠️ PHYSICS CONSTRAINTS LAYER

Sora 2 rispetta la fisica se la descrivi esplicitamente:

```
# Specifica materiali e proprietà fisiche:
"a rubber basketball, medium inflation, glossy hardwood court"

# Guardrail fisici obbligatori per scene complesse:
"consistent object size; no morphing; no teleporting;
object permanence maintained throughout"

# Per veicoli:
"realistic tire deformation under load at apex;
no clipping through geometry; consistent vehicle proportions"

# Per liquidi:
"water surface tension breaks realistically on impact;
natural splash physics"
```

---

## ⛔ NEGATION LAYER (Constraints)

Aggiungi sempre in coda al prompt:

```
Constraints:
- No melting textures
- No geometry warping
- No sudden lighting changes between beats
- No costume changes mid-clip
- Keep character proportions consistent throughout
- No teleporting objects
- No text overlays
- No unnatural camera jumps
- No facial morphing
```

---

## 🔁 STRATEGIA REMIX

```
Principio: cambia UNA sola cosa alla volta.

Esempi:
"Same shot, switch lens to 85mm"
"Same lighting, new color palette: teal, sand, rust"
"Same scene, change car color to matte black"
"Same framing, add second character entering from left at 8s"
"Same location. Only change: weather from sunny to overcast."

Se il shot continua a fallire:
1. Rimuovi il movimento camera (locked-off)
2. Semplifica a una sola azione
3. Svuota il background
4. Una volta che funziona → aggiungi elementi uno alla volta
```

---

## 🏆 TEMPLATE CINEMATIC ULTRA-DETTAGLIATO

```
Format & Look
Duration [Xs]; 180° shutter; digital capture emulating 65mm photochemical contrast;
fine grain; subtle halation on speculars; no gate weave.

Lenses & Filtration
[focale principale] / [focale secondaria] spherical primes; Black Pro-Mist 1/4;

Grade / Palette
Highlights: [tono]
Mids:       [tono + cast colore]
Blacks:     [neri + lift]

Lighting & Atmosphere
[Fonte key]: [direzione], [angolo], [ora]
Bounce:      [tipo + posizione]
Negative fill: [posizione]
Practical:   [luci in scena]
Atmos:       [nebbia, polvere, vapore]

Location & Framing
[Setting + ora del giorno]
Foreground:  [elemento]
Midground:   [soggetto]
Background:  [elemento]

Wardrobe / Props
Main subject: [età, abbigliamento completo, accessori]
Props:        [oggetti rilevanti]

Sound
Diegetic only / Mixed / Score
[ambient + LUFS]; [SFX]

Optimized Shot List
0.00–[T1]s — "[Shot Name]" ([focale], [movimento])
[descrizione visiva + azione]
Purpose: [obiettivo]

[T1]–[T2]s — "[Shot Name]" ([focale], [movimento])
[descrizione + azione]
Purpose: [obiettivo]

[T2]–[Xs] — "[Shot Name]" ([focale], [movimento])
[descrizione + azione]
Purpose: [chiusura]

Constraints:
[negation layer specifico]

Finishing
Grade: [grain + halation + LUT]
Audio mix: [priorità suoni]
Poster frame: [descrizione frame thumbnail]
```

---

## 📱 TEMPLATE VIRALE (Short-form 4-12s)

```
Style: [mobile-native / TikTok / Reels], [warm filter], [bright and punchy].

[Prosa 2-3 righe. Hook visivo immediato.]

Cinematography:
Camera shot: [vertical / medium / close-up]
Camera movement: [quick zoom / handheld / static]
Mood: [exciting / funny / satisfying / wholesome]

Actions:
- 0-2s:  [Hook — cattura attenzione]
- 2-8s:  [Sviluppo — azione o reveal]
- 8-12s: [Payoff — fine soddisfacente]

Constraints:
No morphing; consistent subject proportions.

Background Sound:
[satisfying SFX / upbeat ambient]. No dialogue.
```

---

## 📺 TEMPLATE YOUTUBE LONG-FORM

```
Style: [YouTube cinematic / vlog / tutorial], [warm approachable],
[50-85mm lens], [clean non-aggressive grade].

Core Prompt (solo testo): [se non usi I2V — incollare identico in ogni clip]

[Prosa 4-6 righe. Contesto. Presentatore definito.]

Cinematography:
Camera shot: medium / MCU, eye level
Camera movement: slow dolly-in / static / gentle handheld
Lens: 50mm / 85mm shallow DOF
Mood: educational, engaging, trustworthy

Lighting:
Key: soft window light / softbox diffused, camera left
Fill: natural bounce / warm fill right
Palette anchors: [3 colori caldi]
Grade: warm natural / clean neutral

Actions:
- 0-4s:   [Establish]
- 4-8s:   [Punto chiave]
- 8-12s:  [Transition hint]

VO (se presente):
Voice (VO, calm, engaging): "[testo]"

Background Sound:
Soft ambient; no music over speech; room tone at -30 LUFS.
```

---

## 🚗 TEMPLATE AUTOMOTIVE / ACTION

```
Style: Cinematic automotive commercial, anamorphic 2.0x lens,
teal-orange grade, filmic motion blur, 4K quality.

[Veicolo: colore, stato, strada, meteo, ora.]

Cinematography:
Camera shot: low angle tracking / aerial / side profile
Camera movement: smooth tracking matching speed / arc
DOF: deep focus — car sharp, BG slightly blurred
Lens: anamorphic 2.0x / 85mm telephoto
Mood: powerful, adrenaline / sleek, luxury

Lighting:
Key: golden hour low angle / hard midday / track lighting
Rim: edge light on body panels
Palette: teal, burnt orange, matte black
Grade: teal-orange commercial

Actions (12s):
- 0-3s:   [Ingresso frame + dettaglio fisico]
- 3-7s:   [Manovra specifica + fisica realistica]
- 7-10s:  [Camera rise/arc + dettaglio meccanico]
- 10-12s: [Exit frame o freeze su elemento iconico]

Effects:
motion blur on wheels; water spray if wet;
heat shimmer from exhaust; lens flare on chrome.

Constraints:
Realistic tire deformation; no geometry clipping;
consistent vehicle proportions; no morphing.

Background Sound:
Engine roar crescendo; tire + wind; ambient setting. No music.
```

---

## ❌ ANTI-PATTERN

| Errore | Perché fallisce | Soluzione |
|---|---|---|
| Credere che il solo testo mantenga il personaggio | Ogni gen è stocastica e indipendente | Usa I2V o Cameo per consistenza reale |
| `"Beautiful cinematic video"` | Vago | Specifica stile, shot, luce, azione |
| Cambiare descrizione personaggio tra shot | Deriva visiva garantita | Core prompt IDENTICO + I2V quando possibile |
| Testo scritto a schermo | Sora gestisce male il testo | Evita o usa come prop decorativo |
| Multipli camera move per shot | Confonde il modello | Una sola move per shot |
| Dialogo lungo in 4s | Troppo poco tempo | Max 1-2 battute in 4s |
| `nice`, `amazing`, `good` | Non descrivono nulla | Sostantivi e verbi concreti |
| Più di 2 personaggi distinti | Consistenza degrada rapidamente | Max 2 soggetti per clip, extras generici |
| Clip > 20s con stesso personaggio | Deriva anche con Cameo | Stitching in clip da 8-12s |

---

## 🛠️ TROUBLESHOOTING

| Problema | Causa | Fix |
|---|---|---|
| Personaggio diverso da clip a clip | Solo testo, stocastico | Passa a I2V o Cameo |
| Movimento innaturale | Azione troppo complessa | 1 move + 1 azione |
| Edit non fluisce | Luce/palette diverse | Stessa light logic + palette anchors |
| Audio fuori sync | Dialogo troppo lungo | Max 8 parole/battuta |
| Artefatti fisici | Fisica non specificata | Physics Constraints Layer |
| Oggetti teletrasportati | Nessun guardrail | `object permanence maintained` |
| Atmosfera sbagliata | Stile non dichiarato | Stile in apertura |
| Deriva dopo 4-5 clip | Accumulo drift I2V | Rigenera anchor image ogni 4-5 clip |

---

## 📖 VOCABOLARIO RAPIDO

```
SHOT:      EWS, WS, MS, MCU, CU, ECU, OTS, POV, two-shot, aerial, bird's eye, worm's eye
ANGOLI:    eye level, low angle, high angle, Dutch tilt
MOVIMENTI: dolly-in/out, tracking, pan, tilt, arc, crane, handheld, Steadicam, static, whip pan
LENTI:     24mm, 32mm, 50mm, 85mm, 135mm, anamorphic 2.0x, Pro-Mist 1/4, CPL
LUCE:      key, fill, rim, practical, backlight, volumetric, golden hour, blue hour
EFFETTI:   35mm grain, halation, vignette, flare, motion blur, slow-mo, volumetric rays
AUDIO:     whispered, urgent, calm, commanding, faint, crisp, muffled, diegetic, no score
```

---

## ✅ CHECKLIST PRE-GENERAZIONE

- [ ] Stile visivo dichiarato in apertura?
- [ ] Scena con elementi concreti e visibili?
- [ ] Core Prompt personaggio incollato identico (se solo testo)?
- [ ] Hai considerato I2V se la consistenza è critica?
- [ ] Shot (tipo + angolo) specificato?
- [ ] UNA sola camera move?
- [ ] DOF specificato?
- [ ] Luce: fonte + direzione + qualità?
- [ ] Palette anchors (min 3 colori)?
- [ ] Azioni in beats con verbi concreti?
- [ ] Physics Constraints se fisica complessa?
- [ ] Negation Layer (Constraints) in coda?
- [ ] Dialogo breve e nel blocco separato?
- [ ] Background sound specificato?
- [ ] Nessun termine vago?
- [ ] Max 2 personaggi distinti per clip?
- [ ] Clip pianificate < 20s se stesso personaggio?

---

*Guida basata su: OpenAI Cookbook — Sora 2 Prompting Guide (Robin Koenig & Joanne Shin, Oct 2025)*
*+ aifreeapi.com Character Consistency Guide (Jan 2026)*
*+ skywork.ai Sora 2 Hacks (2025) + createxflow.com Advanced Reference*
*Versione corretta | Febbraio 2026*
