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

## 🧱 ARCHITETTURA UNIVERSALE DEL PROMPT

```
[BLOCCO 1 — STILE VISIVO]
(prima riga: definisce l'estetica dominante dell'intero video)

[BLOCCO 2 — PROSA DESCRITTIVA]
(scena, personaggi, ambiente, atmosfera — 3-8 righe specifiche)

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
```

---

## 🎨 BLOCCO 1 — STILE VISIVO

Il **livello di stile è la leva più potente** per guidare il modello. Va dichiarato PRIMA di qualsiasi altra cosa. Definisce lens, luce e grade automaticamente.

### Stili predefiniti (usali come trigger)

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

## 📷 BLOCCO — CINEMATOGRAFIA COMPLETA

### Shot Types (Tipo di inquadratura)

| Codice | Descrizione | Uso tipico |
|---|---|---|
| `ELS` / `extreme wide shot` | Paesaggio dominante, soggetto minuscolo | Natura, aperture sceniche |
| `WS` / `wide establishing shot` | Contesto e setting, soggetto visibile | Apertura di scena |
| `MS` / `medium shot` | Dalla vita in su | Conversazioni, YouTube |
| `MCU` / `medium close-up` | Spalle e sopra | Emozione, narrativa |
| `CU` / `close-up` | Solo viso | Dramma, reazione |
| `ECU` / `extreme close-up` | Dettaglio singolo (occhi, mani) | Tensione, dettaglio |
| `OTS` / `over-the-shoulder` | Da dietro spalla del soggetto | Dialogo, punto di vista |
| `POV` | Soggettiva del personaggio | Immersione |
| `Two-shot` | Due soggetti nel frame | Interazione |
| `Aerial wide` | Dall'alto, drone-like | Ambientazione epica |
| `Bird's eye` | Zenitale, 90° verso il basso | Geometria, pattern |
| `Worm's eye` | Dal basso verso l'alto | Potere, grandiosità |

### Camera Angles (Angoli)

```
eye level          → neutro, quotidiano, identificativo
low angle          → potere, grandiosità, minaccia
high angle         → vulnerabilità, contesto, sorveglianza
Dutch tilt         → instabilità, disagio psicologico
slight angle from behind → tensione narrativa, distanza emotiva
```

### Camera Movements (Movimenti)

| Movimento | Descrizione | Effetto emotivo |
|---|---|---|
| `dolly-in` / `push-in` | Camera si avvicina al soggetto | Intensità, focus emotivo |
| `dolly-out` / `pull-back` | Camera si allontana | Rivelazione, isolamento |
| `tracking shot` | Segue il soggetto in movimento | Dinamismo, accompagnamento |
| `pan left/right` | Rotazione orizzontale su asse fisso | Rivelazione laterale |
| `tilt up/down` | Rotazione verticale su asse fisso | Grandiosità / intimità |
| `slow arc around subject` | Orbita intorno al soggetto | Esposizione a 360°, epico |
| `slow crane up` | Salita verticale della camera | Rivelazione progressiva |
| `handheld micro-shake` | Tremore minimo portato a mano | Realismo, documentario |
| `Steadicam` | Fluidità con lievi oscillazioni naturali | Cinema moderno, seguire |
| `static / locked-off` | Nessun movimento | Tensione, contemplazione |
| `drone-like ascent` | Salita aerea progressiva | Scala, grandiosità |
| `whip pan` | Pan ultra-rapido con motion blur | Transizione energica |

### Lenti & Filtri

```
# Focali
24mm wide angle          → grande angolo, distorsione prospettica
32mm spherical prime     → wide naturale, ampio contesto
50mm lens aesthetic      → ottica "dell'occhio umano", neutro
85mm, shallow DOF        → ritratto, bokeh naturale, elegante
135mm telephoto          → compressione prospettica, sfondo mosso
anamorphic 2.0x          → widescreen cinematografico, lens flare orizz.

# Filtri
Black Pro-Mist 1/4       → ammorbidisce gli aloni, tocco cinematografico
Black Pro-Mist 1/2       → più intenso, pelle morbida, vintage
CPL filter               → gestisce riflessi su vetro e acqua
No filtration            → clean, documentaristico, digitale puro
```

---

## 💡 BLOCCO — LUCE & COLORE

### Struttura della luce (3 punti)

```
Key light:   [fonte principale — direzione, qualità, colore]
Fill light:  [riduce ombre dure — caldo/freddo, intensità]
Rim/Edge:    [contorno del soggetto — separa da BG]
```

### Fonti di luce per trigger

| Fonte | Trigger | Ora/Contesto |
|---|---|---|
| Sole diretto basso | `low angle sunlight, golden hour` | Alba/Tramonto |
| Sole diretto alto | `harsh noon sunlight, overhead` | Mezzogiorno |
| Luce diffusa | `overcast diffused light, no shadows` | Nuvoloso |
| Finestra naturale | `soft window light from camera left` | Interno giorno |
| Luce artificiale calda | `warm tungsten practical, 3200K` | Interno sera |
| Luce fredda neon | `cool neon spill, blue-green cast` | Urbano notturno |
| Luce backlit | `strong backlight, silhouette effect` | Drammatico |
| Golden hour | `warm golden key, low angle amber` | Romantico, epico |
| Blue hour | `cool blue ambient, twilight` | Malinconico |
| Volumetric | `volumetric light rays, dust particles` | Atmosferico |

### Palette Colore — Template

```
Palette anchors: [colore 1], [colore 2], [colore 3], [colore 4]
Grade: [nome del look]

# Esempi di look comuni:
Teal-orange commercial    → teal in ombre, arancio su skin
Warm Kodak               → giallo/ambra su tutto, ombre marroni
Fuji cool                → mids freddi, pelle lievemente desaturata
Desaturated noir         → quasi B&W, alto contrasto
Warm vintage             → sepia lieve, grain, vignette
Clean digital            → neutro, nessun grade evidenziato
Nordic cool              → blu-grigio dominante, luce piatta
```

---

## 🎬 BLOCCO — AZIONI & TIMING

### Principio fondamentale

> **Una camera move + Una azione soggetto = Un shot**

Non sovraccaricare mai un singolo shot con più movimenti o più azioni complesse.

### Struttura dei Beat (per 12 secondi)

```
Actions (12s timeline):
- 0-3s:   [Beat 1 — stabilimento della scena o azione iniziale]
- 3-6s:   [Beat 2 — sviluppo, cambio o reazione]
- 6-9s:   [Beat 3 — climax, dialogo o punto di massima tensione]
- 9-12s:  [Beat 4 — risoluzione, chiusura, freeze o cut implicito]
```

### Come descrivere le azioni (SPECIFICO vs VAGO)

| ❌ Vago | ✅ Specifico |
|---|---|
| `Person walks across room` | `Actor takes four steps to the window, pauses, pulls the curtain in the final second` |
| `Person moves quickly` | `Cyclist pedals three times, brakes hard, stops at crosswalk` |
| `Car drives fast` | `Sports car accelerates through wet corner, tires spray water at apex` |
| `Person is emotional` | `Her jaw tightens, eyes glisten, she turns away before a tear falls` |
| `Robot malfunctions` | `Robot's left arm jolts twice, steam vents from chest, eyes flicker from blue to red` |

### Verbi di azione efficaci

```
MOVEMENT:   strides, lunges, pivots, drifts, stumbles, glides, freezes
GESTURE:    reaches for, grabs, releases, taps, traces, lifts, drops
REACTION:   flinches, recoils, leans in, tilts head, exhales slowly
GAZE:       eyes flick to, glances over shoulder, stares directly at lens
TRANSITION: turns toward camera, steps into shadow, exits frame right
```

---

## 🔊 BLOCCO — AUDIO & DIALOGO

### Regole dialogo per durata clip

| Durata | Max battute | Note |
|---|---|---|
| 4 secondi | 1-2 battute brevi | Max 8-10 parole totali |
| 8 secondi | 3-4 battute | Frasi naturali, ritmo conversazionale |
| 12 secondi | 4-5 battute | Pause incluse, tono specificato |

### Struttura del blocco dialogo

```
Dialogue:
- [PersonaggioA]: "[frase breve]" (tono: urgente/calmo/etc.)
- [PersonaggioB]: "[risposta]"
- [PersonaggioA]: "[chiusura]"

# Per voiceover off-screen:
Voice (VO): "[testo del voiceover]"

# Per narrazione documentaristica:
Narrator (VO, calm, authoritative): "[testo]"
```

### Toni vocali (aggiungi tra parentesi)

```
whispered / sotto voce     → intimità, segreto
urgent / tense             → conflitto, urgenza
calm / measured            → autorità, controllo
excited / breathless       → gioia, sorpresa
sarcastic / dry            → umorismo, cinismo
commanding / assertive     → leadership, potere
monotone / flat            → distanza emotiva, freddo
broken / trembling         → vulnerabilità, dolore
```

### Background Sound — Template

```
Background Sound:
[ambient principale, qualità + intensità]; [suono secondario];
[SFX specifico se presente]; [indicazione musica o "No score."]

# Aggettivi di intensità audio
faint / distant            → in sottofondo, appena percettibile
crisp / sharp              → primo piano, definito
muffled / dampened         → filtrato, da lontano o attraverso materiale
low hum / steady drone     → continuo, atmosferico
intermittent               → irregolare, spezzato

# Specificare livello LUFS se vuoi controllo mix:
ambient at -20 LUFS, no score
```

---

## ⚡ EFFETTI VISIVI & TEXTURE

```
Effects:
[lista effetti separati da punto e virgola]
```

### Libreria effetti completa

```
# Grana e texture film
fine grain overlay               → grana fine universale
35mm film grain                  → grana organica classica
16mm grain, high contrast        → documentaristico grezzo
chroma noise                     → noise digitale colorato

# Ottica
subtle halation on speculars     → alone morbido sulle luci
lens flare on highlights         → flare naturale
anamorphic lens flares           → flare orizzontali caratteristici
soft vignette                    → oscuramento bordi
barrel distortion                → distorsione ottica wide

# Atmosfera
volumetric light rays            → raggi di luce nel fumo/nebbia
dust particles in sunlight       → polvere illuminata
heat shimmer                     → effetto caldo su asfalto
fog layer / mist                 → nebbia leggera atmosferica
rain droplets on lens            → gocce di pioggia sull'ottica
steam / exhaust drift            → vapore o gas che deriva

# Movimento
motion blur on fast movement     → sfocatura da velocità
slow motion (specifica azione)   → rallentatore su beat specifico
ramping speed (slow to fast)     → variazione velocità
```

---

## 🆕 TECNICHE AVANZATE (2025-2026)

### 1. JSON Character Anchor Profile (Massima Consistenza Personaggio)

Per mantenere un personaggio identico tra più clip, crea un "anchor block" in formato JSON da incollare in ogni prompt:

```json
{
  "character_id": "ELENA_01",
  "age_range": "early 30s",
  "hair": "short dark brown hair, blunt cut at jaw level",
  "eyes": "dark brown, slightly almond-shaped",
  "skin": "olive Mediterranean complexion",
  "build": "slender, 5'6\"",
  "outfit": {
    "top": "burgundy oversized blazer",
    "bottom": "black wide-leg trousers",
    "shoes": "white low-top sneakers",
    "accessories": "thin silver pendant necklace, small gold hoop earrings"
  },
  "expression_default": "calm, slightly pensive",
  "continuity_note": "same outfit, same hair, silver pendant always visible"
}
```

**Come usarlo:**
Incolla l'intero JSON block prima del prompt descrittivo. Termina ogni clip con `[Continuation] — same character as ELENA_01: burgundy blazer, silver pendant visible.`

---

### 2. Scene Continuity Chain (Stitching Tecnica)

Per video YouTube lunghi (oltre 12s), genera clip da 4-12s in sequenza e montale:

```
Shot 1: Elena stands at the window of her apartment,
looking out at the rain. Burgundy jacket, black turtleneck,
silver pendant visible. Soft interior lighting.

Shot 2: [Continuation] Elena turns from the window
(same burgundy jacket, black turtleneck, silver pendant)
and walks toward the kitchen. Same apartment interior,
rain still visible through windows. Lighting unchanged.
```

**Regole Stitching:**
- Usa il marker `[Continuation]` all'inizio del secondo shot
- Ripeti SEMPRE vestiti + accessori chiave
- Specifica `Lighting unchanged` / `Same setting`
- Esporta l'**ultimo frame** della clip precedente e usalo come I2V reference per il prossimo shot
- Per clip da 25s usa `sora-2-pro` (Pro runtime permette run più lunghi)

---

### 3. Physics Constraints Layer (Realismo Fisico)

Sora 2 rispetta la fisica reale se la descrivi esplicitamente. Utile per sport, veicoli, liquidi:

```
# Specifica materiali e proprietà fisiche:
"a rubber basketball, medium inflation, glossy hardwood court"

# Specifica forze e outcome:
"bank shot that misses, rebounds off backboard, spins clockwise, bounces twice"

# Aggiungi guardrail fisici:
"consistent object size; no morphing; no teleporting; object permanence maintained"

# Per veicoli:
"realistic tire deformation under load at apex; no clipping through geometry"

# Per liquidi:
"water surface tension breaks realistically on impact; natural splash physics"
```

---

### 4. Descriptive Negation Layer (Anti-Artefatti)

Sora 2 risponde bene alle negazioni esplicite. Aggiungile sempre in coda al prompt:

```
Constraints:
- No melting textures
- No geometry warping
- No sudden lighting changes between beats
- No costume changes mid-clip
- Keep character proportions consistent throughout
- No teleporting objects
- Retain [dettaglio specifico] across all frames
- No text overlays
- No unnatural camera jumps
- No facial morphing
```

---

### 5. Storyboard-First Method (Multi-Shot Planning)

Per video YouTube da 2+ minuti, crea scene card prima di generare:

```
=== SCENE CARD SYSTEM ===

Card 01 | Duration: 8s | Purpose: Establish
Setting: [location dettagliata]
Character: [personaggio con anchor]
Action: [beat preciso]
Camera: [shot + movement]
Continuity hook: "[elemento che deve passare alla card 02]"

Card 02 | Duration: 12s | Purpose: Develop
[Continuation from Card 01]
Setting: [stessa location o nuova — specificare]
Character: [stesso anchor — ripetere dettagli chiave]
Action: [evoluzione della card 01]
Camera: [nuovo shot]
Continuity hook: "[elemento che deve passare alla card 03]"

Card 03 | Duration: 8s | Purpose: Resolve/Transition
[Continuation from Card 02]
...
```

---

### 6. Targeted Re-Render (Fix Chirurgico)

Se una clip ha UN elemento sbagliato, usa il Remix con context locking:

```
# Tecnica: isola l'elemento da cambiare, blocca tutto il resto
"Same location, same lighting, same wardrobe, same camera framing.
Only modify: [elemento specifico da cambiare].
All else identical to previous generation."

# Esempi pratici:
"Same shot, same lighting. Only change: the coffee cup label to 'DECAF'."
"Same scene. Only modify: car color from red to matte black."
"Same framing. Remove: background extras. Keep: main character and props."
```

---

### 7. Iterative Variation Protocol (Trovare il Look Perfetto)

Cambia **UNA sola variabile alla volta** e registra il log:

```
v1.0 → prompt base
v1.1 → cambio: lens 50mm → 85mm
v1.2 → cambio: grade neutral → teal-orange
v1.3 → cambio: lighting golden hour → blue hour
v1.4 → cambio: camera static → slow dolly-in
```

Non riscrivere mai tutto da zero — modifica chirurgicamente una cosa sola.

---

## 🏆 TEMPLATE CINEMATIC ULTRA-DETTAGLIATO (Professional Level)

```
Format & Look
Duration [Xs]; 180° shutter; digital capture emulating 65mm photochemical contrast;
fine grain; subtle halation on speculars; no gate weave.

Lenses & Filtration
[focale principale] / [focale secondaria] spherical primes; Black Pro-Mist 1/4;
[eventuali note su CPL o filtri specifici].

Grade / Palette
Highlights: [descrizione tono highlights]
Mids:       [descrizione mids + cast colore]
Blacks:     [descrizione neri + lift]

Lighting & Atmosphere
[Fonte key]: [direzione], [angolo], [ora equivalente]
Bounce:      [tipo di bounce + posizione]
Negative fill: [posizione]
Practical:   [luci presenti in scena + comportamento]
Atmos:       [nebbia, polvere, vapore, mist — se presenti]

Location & Framing
[Setting principale + ora del giorno]
Foreground:  [elemento in primo piano]
Midground:   [soggetto principale]
Background:  [elemento di sfondo]
[Indicazione di cosa evitare: loghi, branding, etc.]

Wardrobe / Props / Extras
Main subject: [età approssimativa, abbigliamento, accessori, postura]
Extras:       [figure secondarie + abbigliamento]
Props:        [oggetti rilevanti nella scena]

Sound
[tipo: Diegetic only / Mixed / Score]
[descrizione ambient]: [intensità in LUFS]
[SFX specifici]; [no score / indicazione musicale]

Constraints (Negation Layer)
No melting textures; no geometry warping; no costume changes;
object permanence maintained; [altri vincoli specifici].

Optimized Shot List

0.00–[T1]s — "[Nome Shot 1]" ([focale], [movimento camera])
[Descrizione di cosa vede la camera e cosa fa il soggetto.]
Purpose: [obiettivo narrativo/emotivo del shot]

[T1]–[T2]s — "[Nome Shot 2]" ([focale], [movimento camera])
[Descrizione del secondo beat.]
Purpose: [obiettivo]

[T2]–[Xs] — "[Nome Shot 3]" ([focale], [movimento camera])
[Descrizione del beat finale.]
Purpose: [chiusura o suspense]

Camera Notes
[Note tecniche su eyeline, flare, handheld, highlight roll-off, etc.]

Finishing
[Grade overlay: grain, halation, LUT]
[Mix audio: priorità sui suoni]
Poster frame: [descrizione del frame ideale per thumbnail]
```

---

## 📱 TEMPLATE VIDEO VIRALE (Short-form, 4-12s)

```
Style: [mobile-native / TikTok / Reels aesthetic], [warm filter / bold saturation],
[handheld feel], [bright and punchy].

[Prosa: 2-3 righe. Hook visivo immediato. Oggetto o personaggio al centro.]

Cinematography:
Camera shot: [vertical / medium / close-up] shot
Camera movement: [quick zoom / handheld / static lock]
Mood: [exciting / funny / shocking / satisfying / wholesome]

Actions:
- 0-2s:  [Hook — cosa cattura l'attenzione subito]
- 2-8s:  [Sviluppo — azione principale o reveal]
- 8-12s: [Payoff — fine soddisfacente o cliffhanger]

Constraints:
No morphing; no teleporting; consistent subject proportions.

Background Sound:
[trending audio style / satisfying SFX / upbeat ambient]. No dialogue if possible.
```

---

## 📺 TEMPLATE YOUTUBE LONG-FORM (clip da 12s da montare in sequenza)

```
Style: [YouTube cinematic / documentary vlog / tutorial], [warm approachable light],
[50-85mm lens], [clean grade, non aggressive].

Character Anchor:
[JSON o descrizione dettagliata personaggio — vedi sezione JSON Anchor]

[Prosa: 4-6 righe. Contesto di scena. Presentatore o soggetto definito.]

Cinematography:
Camera shot: [medium shot / medium close-up], eye level
Camera movement: [slow dolly-in / static / gentle handheld]
Lens: [50mm / 85mm, shallow DOF]
Mood: [educational, engaging, trustworthy / exciting, aspirational]

Lighting:
Key: [soft window light / softbox-style diffused, from camera left]
Fill: [natural bounce / warm fill from right]
Palette anchors: [3 colori caldi e accoglienti]
Grade: [warm natural / clean neutral]

Actions:
- 0-4s:   [Establish — presentare soggetto o topic]
- 4-8s:   [Development — azione o punto chiave]
- 8-12s:  [Transition hint — suggerisce proseguimento]

Dialogue / VO:
Voice (VO, calm, engaging): "[hook della narrazione o punto chiave]"

Background Sound:
Soft ambient consistent with setting; no music over speech;
room tone natural at -30 LUFS.

Continuity hook: "[cosa passa alla prossima clip]"
```

---

## 🚗 TEMPLATE AUTOMOTIVE / ACTION

```
Style: Cinematic automotive commercial, anamorphic 2.0x lens,
teal-orange color grade, filmic motion blur, 4K quality.

[Descrizione veicolo: colore, modello, condizioni strada, meteo, ora del giorno.
Setting: strada di montagna / circuito / urbano notturno / desert highway / etc.]

Cinematography:
Camera shot: [low angle tracking / wide aerial / extreme low front / side profile]
Camera movement: [smooth tracking matching car speed / slow arc / drone-like ascent]
Depth of field: [deep focus — car sharp, background slightly blurred]
Lens: [anamorphic 2.0x / 85mm telephoto for compression]
Mood: [powerful, cinematic, adrenaline / sleek, luxury, precision]

Lighting:
Key: [golden hour low angle / hard midday / artificial track lighting]
Rim: [edge light on car body panels]
Palette anchors: [teal, burnt orange, matte black] o [silver, charcoal, electric blue]
Grade: teal-orange commercial / cool motorsport

Actions (12s):
- 0-3s:   [Car enters frame from [direzione] at [velocità]; [dettaglio fisico es. spray d'acqua]]
- 3-7s:   [Manovra specifica: curva / accelerazione / frenata con dettaglio fisico realistico]
- 7-10s:  [Camera move: rise / arc; dettaglio meccanico o reazione dinamica]
- 10-12s: [Exit frame o freeze su elemento iconico]

Effects:
[motion blur on wheels]; [water spray particles if wet road];
[heat shimmer from exhaust]; [lens flare on chrome at apex].

Constraints:
Realistic tire deformation under load; no geometry clipping;
consistent vehicle proportions; no morphing of car body.

Background Sound:
Engine roar crescendo; [sound specific al tipo di manovra];
wind rush; [ambient del setting]. No music.
```

---

## 📚 TEMPLATE DOCUMENTARIO / EDUCATIONAL

```
Style: Documentary realism, handheld ENG camera or locked tripod,
natural light only, no artificial grade, authentic texture.

[Prosa: soggetto, contesto storico o geografico, atmosfera reale.]

Cinematography:
Camera shot: [medium / wide], eye level or slight high angle
Camera movement: [handheld micro-shake / static locked / slow push-in]
Lens: [35mm / 50mm spherical, no filtration]
Mood: [authentic, investigative, intimate, authoritative]

Lighting:
Key: Natural only — [window / outdoor / practical room light]
No artificial fill. Embrace realistic shadows.
Palette: Desaturated, neutral, true-to-life.

Actions:
- [Beat 1: soggetto nell'attività documentata]
- [Beat 2: dettaglio o rivelazione]
- [Beat 3: reazione o continuazione]

Narrator (VO, calm, authoritative):
"[frase narrativa breve e informativa]"

Background Sound:
Diegetic only: [suoni dell'ambiente reale specifici];
room ambience at -20 LUFS; no score; no added foley.
```

---

## 🎭 TEMPLATE NARRATIVO / CORTOMETRAGGIO

```
Style: [genere cinematografico specifico], [stile visivo], [tono emotivo].

Character Anchor:
[Descrizione fisica precisa — ripeti identica in ogni shot]

[Prosa: 5-8 righe ricche. Personaggi con caratterizzazione fisica precisa.
Ambiente descritto nei dettagli sensoriali. Tensione o stato emotivo implicito.]

Cinematography:
Camera shot: [inquadratura che serve la narrativa]
Camera movement: [movimento che amplifica l'emozione]
Depth of field: [shallow per isolare emozione / deep per contesto]
Lens: [35mm per vicinanza, 85mm per dramma]
Mood: [emozione dominante della scena]

Lighting:
Key: [fonte che costruisce il mood]
Fill: [bilancia o rinforza il contrasto]
Rim: [separa personaggio dal BG]
Palette anchors: [3-4 colori coerenti con il tono emotivo]

Actions:
- [Beat 1: stato iniziale del personaggio]
- [Beat 2: innesco — cosa disturba lo status quo]
- [Beat 3: reazione fisica ed emotiva]
- [Beat 4: nuova situazione o open ending]

Dialogue:
- [Personaggio A]: "[battuta rivelante del carattere]"
- [Personaggio B]: "[risposta che crea tensione o contrasto]"

Constraints:
No costume changes; consistent facial features throughout; object permanence maintained.

Background Sound:
[Ambiente che riflette la tensione narrativa];
[SFX diegetici coerenti]; [musica: assente o "subtle ambient pad, no melody"].
```

---

## ❌ ANTI-PATTERN — Cosa NON fare

| Errore | Perché fallisce | Soluzione |
|---|---|---|
| `"Beautiful cinematic video"` | Vago, il modello improvvisa tutto | Specifica stile, shot, luce, azione |
| `"Make a 30 second video"` | La durata si imposta via API | Imposta `seconds` nell'API call |
| Cambiare nome/descrizione personaggio tra shot | Rompe la continuità | Usa JSON anchor + IDENTICO phrasing |
| Testo scritto a schermo nella scena | Sora gestisce male il testo | Evita o usalo come prop decorativo |
| Azioni fisicamente impossibili senza note | Genera artefatti e glitch | Specifica "special effect" se vuoi surreale |
| Multipli camera move nello stesso shot | Confonde il modello | Una sola camera move per shot |
| Dialogo lungo in clip da 4s | Non c'è abbastanza tempo | Max 1-2 battute brevi in 4s |
| Aggettivi vaghi: `nice`, `amazing`, `good` | Non descrivono nulla di visibile | Usa sostantivi e verbi concreti |
| Chiedere loghi o brand reali | Policy + instabilità del modello | Usa `generic branding` o `no signage` |
| Ignorare il Negation Layer | Artefatti non richiesti appaiono | Aggiungi sempre i Constraints in coda |
| Saltare il Character Anchor | Deriva visiva tra shot | JSON profile obbligatorio per personaggi ricorrenti |

---

## 🔁 STRATEGIA REMIX

```
Principio: cambia UNA sola cosa alla volta e DI' cosa stai cambiando.

Esempi efficaci:
"Same shot, switch lens to 85mm"
"Same lighting, new color palette: teal, sand, rust"
"Same scene, change monster color to orange"
"Same framing, add a second character entering from left at 8s"
"Same everything, remove the background music"
"Same location, same character. Only change: weather from sunny to overcast."

Se il shot continua a fallire:
1. Rimuovi il movimento camera (locked-off)
2. Semplifica l'azione a una sola
3. Svuota il background (plain wall / fog / white)
4. Una volta che funziona → aggiungi elementi uno alla volta
```

---

## 🛠️ TROUBLESHOOTING COMPLETO

| Problema | Causa probabile | Fix |
|---|---|---|
| Risultati troppo casuali | Prompt troppo leggero | Aggiungi shot + DOF + light anchor |
| Movimento innaturale | Azione troppo complessa | Riduci a 1 camera move + 1 azione |
| Edit non fluisce tra clip | Luce e palette diverse | Mantieni stessa light logic + palette anchors |
| Personaggio inconsistente | Phrasing variato tra shot | JSON anchor + `[Continuation]` marker |
| Audio fuori sync | Dialogo troppo lungo | Accorcia le battute, max 8 parole/battuta |
| Artefatti fisici (morphing) | Fisica non specificata | Aggiungi Physics Constraints Layer |
| Oggetti che "teletrasportano" | Nessun guardrail fisico | `object permanence maintained; no teleporting` |
| Testo illeggibile in scena | Limite del modello | Evita o usa come prop decorativo |
| Atmosfera sbagliata | Stile non dichiarato | Aggiungi stile in apertura prompt |
| Continuità rotta tra clip lunghe | Stitching non gestito | Usa tecnica last-frame-as-I2V-reference |
| Vestiti che cambiano | Anchor non ripetuto | Ripeti anchor in OGNI clip separata |

---

## 📖 VOCABOLARIO DI RIFERIMENTO RAPIDO

### Shot
```
EWS, WS, MS, MCU, CU, ECU, OTS, POV, two-shot, aerial, bird's eye, worm's eye
```

### Angoli
```
eye level, low angle, high angle, Dutch tilt, slight angle from behind
```

### Movimenti
```
dolly-in, dolly-out, tracking, pan, tilt, arc, crane, handheld,
Steadicam, static/locked, drone ascent, whip pan
```

### Lenti
```
24mm, 32mm, 50mm, 85mm, 135mm, anamorphic 2.0x,
Black Pro-Mist 1/4, Black Pro-Mist 1/2, CPL
```

### Luce
```
key, fill, rim, practical, backlight, volumetric, golden hour,
blue hour, overcast, noon, window light, tungsten, neon
```

### Grana / Effetti
```
35mm grain, 16mm grain, fine grain overlay, halation, vignette,
lens flare, anamorphic flare, motion blur, slow motion,
volumetric rays, dust particles, heat shimmer, fog layer
```

### Toni Audio
```
whispered, urgent, calm, excited, commanding, monotone, broken,
faint, crisp, muffled, distant, low hum, diegetic only, no score
```

---

## ✅ CHECKLIST PRE-GENERAZIONE

- [ ] **Stile visivo** dichiarato in apertura?
- [ ] **Scena descritta** con elementi concreti e visibili?
- [ ] **JSON Character Anchor** incluso per personaggi ricorrenti?
- [ ] **Shot** (tipo + angolo) specificato?
- [ ] **Movimento camera** specificato (uno solo per shot)?
- [ ] **DOF** specificato?
- [ ] **Luce** con fonte + direzione + qualità?
- [ ] **Palette anchors** (min 3 colori)?
- [ ] **Azioni** descritte in beats con verbi concreti?
- [ ] **Physics Constraints** aggiunti se scene con fisica complessa?
- [ ] **Negation Layer** aggiunto in coda (`Constraints:`)?
- [ ] **Dialogo** nel blocco separato, breve e naturale?
- [ ] **Background sound** specificato?
- [ ] **Continuity hook** aggiunto se parte di una serie di clip?
- [ ] Nessun termine vago (`beautiful`, `nice`, `amazing`)?
- [ ] Una sola camera move per shot?
- [ ] Descrizione personaggio IDENTICA tra clip multiple?

---

*Guida basata su: OpenAI Cookbook — Sora 2 Prompting Guide (Robin Koenig & Joanne Shin, Oct 2025)*
*Integrata con: skywork.ai Sora 2 Hacks (2025), createxflow.com Advanced Reference, aifreeapi.com Character Consistency Guide*
*Versione estesa per content creator | Ultimo aggiornamento: Febbraio 2026*
