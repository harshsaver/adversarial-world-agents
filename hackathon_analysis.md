# YC x Google DeepMind Multimodal Frontier Hackathon -- Deep Analysis

**Date:** March 7, 2026 | **Build window:** 6.5 hours (10:30 AM - 5:00 PM)
**Team:** 2 people | **Track record:** 2nd at TreeHacks (YC track), 2nd at Browser Use hackathon
**Goal:** Win a YC interview

**Available tools:**
- **Gemini 3.1** -- 1M context window, agentic vision (Think-Act-Observe loop with code execution), structured JSON output, video understanding (up to 1 hour per call at 1 FPS), real-time video analysis
- **Lyria / Lyria RealTime** -- text-to-music, image-to-music, WebSocket streaming at 48kHz stereo, 2-second latency, latent-space steering with weighted text prompts
- **NanoBanana 2** -- sub-second 4K image generation, character consistency across up to 5 characters and 14 objects, storyboard-native

---

## EXECUTIVE VERDICT (Read This First)

**Recommended: IDEA 2 (Git for Video) with modifications.**

Idea 1 is too research-y and has a direct competitor (Versos AI) that launched 2 weeks ago. Idea 3 is too infrastructure-heavy for 6.5 hours. Idea 2 hits the sweet spot: it is demoable, uses all three APIs naturally, has a clear business case, and the "world model data format" angle gives it intellectual depth without being a research paper.

But read the full analysis -- the devil is in the details and there are specific modifications that make or break each idea.

---

## IDEA 1: World Data Factory

### What the thesis claims
World models (Genie 3, Cosmos, Sora) train on raw pixels + text captions. Research exists to decompose video into structured scene graphs (SVG2, Action Genome, V-CDN). Nobody has connected these two worlds. This project builds the bridge.

### Is the thesis true?

**Partially.** The gap is real but narrowing fast.

The data problem in world models IS the acknowledged bottleneck. NVIDIA's Cosmos platform literally calls out the 5-step pipeline: splitting, filtering, annotation, deduplication, sharding. They process 20M hours of video with VLM-based annotation. The Cosmos Transfer WFMs accept structured inputs: segmentation maps, depth maps, LiDAR scans, trajectories, HD maps, 3D bounding boxes.

SVG2 (published February 26, 2026 -- literally 9 days ago) demonstrates that fully automated video scene graph generation at scale is possible: 636K videos, 6.6M objects, 52M attributes, 6.7M relations. Their TRaSER model uses a VLM backbone to produce scene graphs in a single forward pass.

**But here is the problem: Versos AI launched on February 23, 2026.** They explicitly position as "the first end-to-end solution for preparing and licensing video training data for AI." They turn video archives into structured, searchable, AI-ready datasets at the frame level. They already have a commercial partnership with CuriosityStream. They raised $1.85M.

So the thesis is true but the "nobody has connected these" part is becoming false in real time.

### What would the demo look like? (3 minutes)

**The honest version:**
1. (30s) Show a raw video clip -- maybe a kitchen scene, someone cooking
2. (60s) Feed it to your pipeline: Gemini 3.1 decomposes it into a structured scene graph JSON: objects (person, knife, tomato, cutting_board), attributes (red, sharp, wooden), relationships (person HOLDS knife, knife ON cutting_board, person CUTS tomato), physics annotations (gravity: down, contact: knife-tomato, force: cutting)
3. (30s) Show the scene graph visualization -- nodes and edges, maybe animated over time
4. (30s) Show the output format side-by-side with what Cosmos/Genie expects as input
5. (30s) Pitch: "Every world model company needs this data. We're the data layer."

**The problem with this demo:** It is fundamentally "I called an API and got JSON back." The visual wow factor is low. Judges see: video in, JSON out. That is not a "whoa" moment.

### Concrete output data format

```json
{
  "video_id": "cooking_001",
  "fps": 1,
  "frames": [
    {
      "timestamp": 0.0,
      "objects": [
        {"id": "obj_1", "label": "person", "bbox": [0.1, 0.2, 0.5, 0.9],
         "attributes": ["standing", "adult", "wearing_apron"]},
        {"id": "obj_2", "label": "knife", "bbox": [0.4, 0.5, 0.5, 0.55],
         "attributes": ["metal", "sharp", "chef_knife"]},
        {"id": "obj_3", "label": "tomato", "bbox": [0.45, 0.6, 0.5, 0.65],
         "attributes": ["red", "whole", "ripe"]}
      ],
      "relationships": [
        {"subject": "obj_1", "predicate": "holds", "object": "obj_2"},
        {"subject": "obj_2", "predicate": "above", "object": "obj_3"},
        {"subject": "obj_1", "predicate": "looking_at", "object": "obj_3"}
      ],
      "physics": {
        "gravity_direction": [0, -1, 0],
        "contact_pairs": [["obj_1", "obj_2"], ["obj_3", "surface"]],
        "forces": [
          {"type": "gravity", "target": "obj_3", "magnitude": "normal"},
          {"type": "applied", "source": "obj_1", "target": "obj_2", "action": "cutting"}
        ]
      },
      "causal_events": [
        {"cause": "person_cuts_tomato", "effect": "tomato_sliced",
         "confidence": 0.85}
      ]
    }
  ]
}
```

### MVP buildable in 6.5 hours

Yes, technically. The core loop is:
1. Upload video to Gemini 3.1 via File API
2. Prompt with a detailed schema asking for scene graph extraction
3. Parse the structured JSON output
4. Visualize with a simple web frontend (D3.js force-directed graph or similar)

The Gemini API already supports `responseMimeType: 'application/json'` with schema enforcement. You define your Pydantic models and get typed output.

**Time estimate:**
- Schema design and prompt engineering: 1.5 hours
- Backend (Flask/FastAPI + Gemini API calls): 2 hours
- Frontend visualization: 2 hours
- Demo prep and polish: 1 hour

This is feasible but leaves almost no buffer. And the result will feel like a well-prompted API call, not a product.

### Who would pay?

| Customer | Why | Reality Check |
|----------|-----|---------------|
| NVIDIA (Cosmos team) | Need structured training data for WFMs | They already built their own pipeline |
| Runway | Training GWM-1 and successors | They do this internally |
| Robotics companies (1X, Figure, Covariant) | Need world model training data | Most use simulation, not video decomposition |
| Self-driving (Waymo, Cruise) | Structured scene understanding | They have massive internal data teams |
| Scale AI competitors | New data type to offer | Maybe -- but Scale already does video annotation |
| World Labs | Building spatial intelligence | Possible but very early |

**Honest assessment:** The customers who need this most (NVIDIA, Runway, Google DeepMind) already build their own pipelines. The ones who would buy it are smaller robotics companies who cannot afford to build the pipeline internally. Market exists but is narrow.

Versos AI is the closest competitor and they just launched with $1.85M in funding. They are attacking this from the "video library owners want to monetize their archives for AI training" angle, which is arguably a better go-to-market.

### Technical risks

1. **Gemini 3.1 output quality for physics/causality** -- LLMs are notoriously weak at physics reasoning. The "physics" and "causal_events" fields will be the least reliable parts of your output. If judges ask "how accurate is the physics annotation?" you will not have a good answer.
2. **Processing time** -- A 1-minute video at 1 FPS = 60 frames. Gemini 3.1 can handle this but response time may be 30-60 seconds. During a live demo, this is dead air.
3. **Schema hallucination** -- Even with structured output mode, Gemini may hallucinate relationships or miss objects. You have no ground truth to validate against in a hackathon setting.
4. **Visualization complexity** -- A scene graph with 20+ objects and 50+ relationships over 60 frames is visually noisy. Making this look good in 6.5 hours is hard.

### Is this too research-y for YC?

**Yes.** This is the core problem. YC funds companies, not papers. The pitch "we decompose video into scene graphs for world model training" sounds like a research project. The response from a YC partner would be: "Who is your customer? How do you know they will pay? Have you talked to any world model teams?"

You cannot answer those questions with a hackathon demo. And Versos AI just launched doing this commercially, which means you would be pitching into a space where someone already has a product and a customer (CuriosityStream).

### How would you use Lyria and NanoBanana 2?

**Honestly: they do not fit naturally.**

You could force it:
- NanoBanana 2: "Generate visual reconstructions from the scene graph to verify accuracy" -- but this feels bolted on
- Lyria: "Generate audio descriptions of scene events" -- this is pure gimmick

If the hackathon weights "use of the full multimodal stack" heavily in judging, this is a significant disadvantage.

### Verdict on Idea 1

| Criterion | Score (1-10) | Notes |
|-----------|:---:|-------|
| Demoability | 4 | Video in, JSON out is not visually exciting |
| Buildability in 6.5 hrs | 7 | Core pipeline is straightforward |
| Use of all 3 APIs | 2 | Lyria and NanoBanana have no natural role |
| Business case | 5 | Real but narrow, and Versos AI exists |
| "Whoa" factor | 3 | Intellectually interesting, visually dull |
| YC interview readiness | 4 | Too research-y, hard to pitch as a company |
| **Overall** | **4.2** | |

---

## IDEA 2: Git for Video (with World Model angle)

### What the thesis claims
Video is an opaque binary blob. Decompose it into a structured, diffable, branchable representation: scenes, cuts, overlays as config; audio/visuals as generated assets. Gemini handles decomposition, NanoBanana for visuals, Lyria for audio. The deeper angle: the scene graph IS world model training data.

### Is this a real problem?

**Absolutely yes.** Video editing today is file-based. There is no "git diff" for video. The closest tools:
- **Descript**: Edits video via transcript (text-based), but only for dialogue. Cannot diff visual composition.
- **Turn Around**: Just launched, provides commit/branch/timeline-diff for DaVinci Resolve projects. But it diffs the project file, not the video content itself. It is version control for the editor state, not the video semantics.
- **Runway**: Generates video from prompts, but no structured representation or diffing.
- **CapCut**: Smart cuts with 94% accuracy but no version control or semantic decomposition.

Nobody does semantic decomposition + diffing + regeneration from structured config. This is genuinely novel.

### What would the demo look like?

**This is where Idea 2 shines.** Here is a 3-minute demo script:

**Minute 1: Decompose**
- Upload a 30-second video (e.g., a product commercial)
- System decomposes it into structured representation:
  - Scene 1 (0:00-0:08): "Wide shot, modern kitchen, warm lighting, woman preparing coffee"
  - Scene 2 (0:08-0:15): "Close-up, espresso machine, steam rising, rich browns"
  - Scene 3 (0:15-0:25): "Medium shot, woman sipping coffee, smiling, morning sun through window"
  - Audio track: "Upbeat acoustic, warm feeling, 120 BPM"
  - Transitions: "Scene 1->2: zoom in, 0.5s; Scene 2->3: dissolve, 1.0s"
- Show the config file (clean YAML/JSON)

**Minute 2: Diff and Branch**
- "Let's make an alternate version for a younger audience"
- Change Scene 1 description: "modern loft apartment" instead of "modern kitchen"
- Change Audio: "lo-fi hip hop, chill vibes, 90 BPM"
- Show the diff: green/red like a git diff, but for video scenes
- Hit "regenerate": NanoBanana regenerates Scene 1 with same character but new setting, Lyria generates new background music
- Side-by-side comparison of original vs. branch

**Minute 3: Business + World Model angle**
- "Every video editor deals with 'can you make another version?'"
- "Every version is a full duplicate today. Our diffs are 50 bytes, not 500 MB."
- "And here is the deeper play: this structured representation IS world model training data."
- Show the scene graph view of the decomposed video
- "We are building the file format the AI-native video industry needs."

**This demo has visual punch.** Judges see: side-by-side video comparison, colored diffs, character-consistent regeneration, generated music. It uses all three APIs in ways that feel organic.

### What is the minimum viable diff?

The MVP diff is a text diff of the structured representation. You do NOT need to build actual video-level diffing. Here is the key insight:

```yaml
# Version A (original)
scenes:
  - id: scene_1
    description: "Wide shot, modern kitchen, warm lighting"
    duration: 8.0
    characters: ["woman_01"]
    audio: "upbeat acoustic, warm"

# Version B (branch)
scenes:
  - id: scene_1
-   description: "Wide shot, modern kitchen, warm lighting"
+   description: "Wide shot, modern loft apartment, cool lighting"
    duration: 8.0
    characters: ["woman_01"]
-   audio: "upbeat acoustic, warm"
+   audio: "lo-fi hip hop, chill"
```

The diff is just text. The magic is that each side of the diff maps to a generated visual (NanoBanana) and audio (Lyria). You show the diff AND the before/after renders.

### Existing tools and libraries to accelerate

| Tool | What it does | Integration effort |
|------|-------------|-------------------|
| **PySceneDetect** | Splits video into scenes by detecting cuts | pip install, 5 lines of code, works in seconds |
| **FFmpeg** | Extract frames, audio tracks, metadata | CLI calls, well-documented |
| **Whisper** (or Gemini itself) | Transcribe audio/dialogue | API call |
| **Gemini 3.1** | Describe each scene semantically | Core of the pipeline |
| **NanoBanana 2** | Regenerate scenes from modified descriptions | API call with character refs |
| **Lyria RealTime** | Generate/modify background music | WebSocket API |
| **difflib** (Python stdlib) | Generate unified diffs of text | Zero-dependency |

**Critical acceleration:** PySceneDetect handles the hardest part (scene boundary detection) in seconds. Gemini handles the second hardest part (semantic description). NanoBanana and Lyria handle regeneration. Your job is to wire them together and build the UI.

### Concrete build plan (6.5 hours)

| Time | Person A (Backend) | Person B (Frontend) |
|------|-------------------|---------------------|
| 10:30-11:00 | Set up project, API keys, test Gemini/NanoBanana/Lyria connectivity | Design UI wireframes, set up React/Next.js or Streamlit |
| 11:00-12:00 | Build video decomposition pipeline: PySceneDetect -> frame extraction -> Gemini scene description -> structured YAML output | Build decomposition view: upload video, show scene timeline with thumbnails |
| 12:00-1:00 | Build scene regeneration pipeline: take modified description -> NanoBanana for visuals, Lyria for audio | Build diff view: side-by-side YAML with syntax highlighting, green/red diff |
| 1:00-1:30 | LUNCH (eat while debugging) | LUNCH (eat while debugging) |
| 1:30-2:30 | Build "branch" logic: duplicate config, allow edits, track changes | Build comparison view: original vs. regenerated side-by-side |
| 2:30-3:30 | Integrate NanoBanana character consistency (pass reference images from original scene to maintain character identity) | Build world model data view: show scene graph visualization |
| 3:30-4:30 | End-to-end testing, fix bugs, prepare demo video as backup | Polish UI, add transitions/animations, prepare presentation |
| 4:30-5:00 | Demo rehearsal x3 | Demo rehearsal x3 |

### Who would pay?

| Customer | Problem | Willingness to pay |
|----------|---------|-------------------|
| **Video agencies / post-production** | Managing 20+ versions of a 30s commercial for different markets | HIGH -- they bill $200-500/hr and versioning is pure pain |
| **YouTube creators** | "Make a short version, a vertical version, a different intro" | MEDIUM -- they want it but are price sensitive |
| **Brand marketing teams** | "Same ad but for UK market, different music, different setting" | HIGH -- they pay agencies $50K+ per campaign |
| **Film studios (pre-production)** | Storyboard iteration with consistent characters | MEDIUM-HIGH -- currently done manually |
| **E-learning / corporate training** | Multiple versions of training videos for different departments | MEDIUM |
| **World model companies** (secondary market) | Structured video decomposition as training data | SPECULATIVE but real |

The primary business is B2B SaaS for video teams. The world model angle is the "and it is also useful for..." kicker that makes the TAM story enormous.

### Technical risks

1. **PySceneDetect accuracy** -- Works well for hard cuts, less well for gradual transitions. MITIGATION: For the demo, choose a video with clean cuts.
2. **NanoBanana character consistency across scenes** -- Supports up to 5 characters, but consistency is probabilistic. MITIGATION: Use a simple scene with one character. Pre-test before demo.
3. **Lyria generation matching video mood** -- Generated music may not perfectly match. MITIGATION: Use weighted prompts with specific genre/tempo/mood parameters.
4. **Processing time** -- Scene decomposition + description + regeneration could take 2-3 minutes total. MITIGATION: Pre-process the "before" version; only regenerate the "after" live.
5. **Demo failure** -- The most dangerous risk. MITIGATION: Record a backup video of the demo working. If live demo fails, play the recording and explain what is happening.

### Comparison to existing tools

| Feature | Descript | Turn Around | Runway | **Git for Video (yours)** |
|---------|---------|-------------|--------|--------------------------|
| Semantic decomposition | Text only (transcript) | None (file-level) | None | Full scene semantics |
| Diffing | Transcript diff | Timeline diff | N/A | Semantic diff |
| Regeneration from config | No | No | From prompt only | Yes, with consistency |
| Version control | Basic | Git-like | No | Git-like |
| Audio generation | No | No | No | Yes (Lyria) |
| Image regeneration | No | No | Yes | Yes (NanoBanana) |
| World model data output | No | No | No | Yes |

### The "world model data format" angle -- stretch or genuine?

**Genuine, but secondary.** The structured representation you create (objects, relationships, scene descriptions, temporal flow, audio descriptions) is genuinely useful for world model training. It is similar in spirit to what SVG2 does with automated video scene graph generation, and what NVIDIA Cosmos expects as structured inputs.

However, the primary value proposition is the video editing workflow. If you lead with "world model training data," judges will correctly identify this as Idea 1 wearing a different hat. Lead with the video editing use case; reveal the world model angle as the "10x TAM multiplier" in your pitch.

### Verdict on Idea 2

| Criterion | Score (1-10) | Notes |
|-----------|:---:|-------|
| Demoability | 9 | Side-by-side video diff is visually stunning |
| Buildability in 6.5 hrs | 6 | Tight but feasible with the right shortcuts |
| Use of all 3 APIs | 9 | Gemini for decomposition, NanoBanana for regeneration, Lyria for audio |
| Business case | 8 | Clear pain point, identifiable customers |
| "Whoa" factor | 8 | "You can diff a video?!" is a strong reaction |
| YC interview readiness | 8 | Product-shaped, clear market, big vision |
| **Overall** | **8.0** | |

---

## IDEA 3: Human-as-Sensor Network

### What the thesis claims
Regular people walk around with phones/wearables. AI processes their video/sensor stream into structured spatial/physical data. Output is training-ready world model data. Like Waze but for physical reality understanding.

### What phone sensors are available?

| Sensor | Available on | Data type | Useful for |
|--------|-------------|-----------|-----------|
| Camera (rear) | All phones | RGB video, 4K 60fps | Visual scene understanding |
| Camera (front) | All phones | RGB video | Not useful for this |
| LiDAR | iPhone Pro models only (12 Pro+) | Depth maps, 3D point clouds | Precise spatial understanding |
| IMU (accelerometer + gyroscope) | All phones | 6-axis motion data | Movement, orientation, vibration |
| GPS | All phones | Lat/long/altitude | Geolocation |
| Barometer | Most modern phones | Atmospheric pressure | Altitude, floor detection |
| Magnetometer | Most phones | Magnetic field | Compass heading |
| ARKit/ARCore | iOS/Android | Plane detection, anchors, 6DOF tracking | 3D spatial mapping |

### What could Gemini 3.1 extract from a phone camera stream in real-time?

Using Gemini 3.1's agentic vision with code execution:
- Object detection and classification (people, vehicles, furniture, signs)
- Spatial relationships between objects
- Surface material estimation
- Lighting conditions
- Activity recognition (walking, cooking, driving)
- Text/sign reading (OCR)
- Rough depth estimation (even without LiDAR)
- Scene type classification (kitchen, street, office)
- Weather/environmental conditions

**Real-time constraint:** At 1 FPS sampling, Gemini can handle this but with latency. True real-time (30 FPS) analysis is not possible via the API. You would do frame sampling (1-5 FPS), batch process, and stream results.

### What would the demo look like?

**Option A: Live phone capture**
1. One team member walks around the hackathon venue with a phone
2. The phone streams camera + sensor data to your backend
3. Gemini 3.1 processes frames into structured world data
4. A dashboard shows: objects detected, spatial map building, physics annotations
5. The accumulated data is shown as a growing scene graph of the venue

**Option B: Pre-recorded walkthrough**
1. Use a pre-recorded walkthrough video of a space
2. Process it through the pipeline
3. Show the structured output: 3D-ish map, object inventory, relationships
4. Compare to what a robotics company would need for training data

### Can you build a meaningful demo in 6.5 hours?

**This is the critical weakness.** Let me break down what you actually need to build:

1. **Phone capture app** -- Either a native iOS/Android app (NOT buildable in 6.5 hours) or a web app using getUserMedia + DeviceMotion API (buildable but lossy -- no LiDAR, no ARKit)
2. **Data streaming pipeline** -- WebSocket from phone to server (1-2 hours to build reliably)
3. **Gemini processing pipeline** -- Frame sampling + API calls + structured output (2 hours)
4. **Dashboard visualization** -- Map, object list, scene graph (2-3 hours)
5. **"Network" component** -- Multiple phones contributing to one map (adds significant complexity)

**Total estimated time: 7-10 hours.** You are over budget before you start.

**The "network" part is the killer.** One phone sending data is "video analysis." Multiple phones contributing to a shared world model is the actual thesis. But building multi-source data fusion, deduplication, and spatial alignment in 6.5 hours is unrealistic.

You would likely demo with one phone and CLAIM it works as a network, which judges will see through.

### How does this compare to existing players?

| Player | What they do | Scale | Your differentiation |
|--------|-------------|-------|---------------------|
| **Niantic Spatial (Large Geospatial Model)** | 3D mapping from Pokemon Go/Scaniverse data, 50M neural networks, 150T parameters | Massive -- millions of users scanning locations | You cannot compete on scale. They have years of data. |
| **Meta Project Aria** | Ego-centric AR glasses with rich sensors (multiple cameras, IMU, eye tracking, barometer, GPS) | Research-grade hardware, not consumer phones | Your sensors are worse (phone vs. AR glasses) |
| **Ego4D/Ego-Exo4D** | Large-scale egocentric video dataset for understanding human activities | Academic dataset, 3,670 hours of video | You are smaller, but potentially more structured |
| **Mapillary (Meta)** | Street-level imagery from crowdsourced photos | 2B+ images globally | Focused on street mapping, not indoor/general |
| **Scale AI** | Data annotation platform with human-in-the-loop | Enterprise, massive workforce | Different approach (annotation vs. automated extraction) |

**The honest truth:** Niantic has already built this at scale using Pokemon Go player data. They have millions of users contributing spatial data, and they are building the Large Geospatial Model on top of it. Your hackathon demo is a toy version of what Niantic already has in production.

### Who would pay?

| Customer | Why | Reality check |
|----------|-----|---------------|
| Robotics companies | Need diverse environment data for training | They use simulation or their own data collection |
| Self-driving companies | Want more diverse scene understanding | They have fleet data + mapping cars |
| Google/DeepMind | More training data for world models | They have YouTube, Street View, etc. |
| Real estate / construction | Spatial mapping of buildings | Matterport already does this with specialized hardware |
| Insurance companies | Property condition assessment | Maybe, but niche |

**The business case is weak for a startup.** The companies who need world model training data either (a) already have massive datasets, or (b) use simulation to generate synthetic data. The "crowd" in your crowdsourced model does not have a clear incentive to participate. Waze works because drivers get traffic data back. What do your "human sensors" get back?

### Technical risks

1. **Phone camera quality variation** -- Different phones, different lighting, different angles. Data quality will be inconsistent.
2. **Privacy** -- You are recording public/private spaces with people in them. For a hackathon demo this is fine, but as a product this is a legal minefield.
3. **Web camera API limitations** -- getUserMedia gives you camera access but no LiDAR, no IMU (DeviceMotion API exists but is unreliable across browsers), no ARKit.
4. **Network latency** -- Streaming video frames to a backend + Gemini processing + returning results will have 3-10 second latency. Not "real-time."
5. **Data fusion complexity** -- Merging data from multiple phones into a coherent spatial model requires SLAM-like capabilities you cannot build in 6.5 hours.
6. **No clear demo "moment"** -- The demo is gradual (data accumulates over time). There is no single "whoa" screenshot.

### Use of Lyria and NanoBanana 2

**They do not fit at all.** This is fundamentally a data collection and processing pipeline. There is no creative content generation involved. You could force it:
- NanoBanana 2: "Generate synthetic training scenes to augment the collected data" -- a stretch
- Lyria: Completely irrelevant

This is a major disadvantage in a hackathon that explicitly provides three multimodal tools and presumably wants to see them used.

### Is this too infrastructure-y for a hackathon demo?

**Yes.** Infrastructure products need to demonstrate scale and reliability, both of which are impossible in 6.5 hours. A hackathon demo that says "imagine if millions of people used this" without showing anything beyond one phone camera is unconvincing.

### Verdict on Idea 3

| Criterion | Score (1-10) | Notes |
|-----------|:---:|-------|
| Demoability | 4 | Gradual data accumulation is not exciting |
| Buildability in 6.5 hrs | 3 | Phone capture + streaming + processing + visualization + "network" is too much |
| Use of all 3 APIs | 2 | Only Gemini fits naturally |
| Business case | 3 | Niantic already does this at massive scale |
| "Whoa" factor | 5 | Concept is cool but demo will underwhelm |
| YC interview readiness | 4 | "We're building Niantic's data layer" is a tough pitch |
| **Overall** | **3.5** | |

---

## COMPARATIVE ANALYSIS

### Side-by-side scoring

| Criterion | Weight | Idea 1 | Idea 2 | Idea 3 |
|-----------|:------:|:------:|:------:|:------:|
| Demoability | 25% | 4 | 9 | 4 |
| Buildability in 6.5 hrs | 20% | 7 | 6 | 3 |
| Use of all 3 APIs | 15% | 2 | 9 | 2 |
| Business case clarity | 15% | 5 | 8 | 3 |
| "Whoa" factor for judges | 15% | 3 | 8 | 5 |
| YC interview readiness | 10% | 4 | 8 | 4 |
| **Weighted Score** | | **4.15** | **7.95** | **3.45** |

### What makes judges go "whoa" vs "meh"

**"Whoa" triggers:**
- Visual before/after comparisons (Idea 2 has this)
- Using all three APIs in a way that feels natural, not forced (Idea 2 has this)
- A clear "I would pay for this" moment (Idea 2 has this)
- Live interaction where the audience can see something happen in real-time
- Character consistency across regenerated scenes (NanoBanana's strength)
- Music that matches the visual mood shift (Lyria's strength)

**"Meh" triggers:**
- JSON output displayed on screen (Idea 1)
- "Imagine if millions of people used this" without showing it (Idea 3)
- API wrapper that adds a thin UI layer
- Data pipeline demos without visual transformation
- "This is useful for training" claims without demonstration

### Adjacent YC-backed companies

| Company | Relation | Batch |
|---------|----------|-------|
| **Runway** | World models, video generation | Not YC-backed (VC funded, $5.3B valuation) |
| **Descript** | Text-based video editing | Not YC-backed but adjacent |
| **Scale AI** | Data annotation/labeling | YC S16 |
| **Versos AI** | Video data for AI training | Not YC (raised $1.85M independently) |
| **One Robot** | World model simulation for robotics | Recent, possibly YC-backed |
| **Congruent** | World model radar simulator | Recent, possibly YC-backed |
| Various robotics cos | Would consume world model data | YC has 100+ robotics companies |

---

## RECOMMENDED STRATEGY: IDEA 2 (Git for Video) -- Optimized Build Plan

### Key modifications to maximize impact

1. **Lead with the product, not the tech.** Your opening line should be: "Have you ever tried to make five versions of the same video? Today that means five copies of a 2GB file." NOT: "We decompose video into structured scene graphs."

2. **Pre-process the "before" version.** Before the hackathon starts, have your demo video already decomposed. During the demo, show the decomposition as if it is live (or actually run it live if timing works). The "diff and regenerate" step is the money shot -- make sure it works flawlessly.

3. **Choose your demo video carefully.** Use a simple 15-20 second video with:
   - 2-3 clean scenes (PySceneDetect-friendly hard cuts)
   - One consistent character (NanoBanana sweet spot)
   - A clear mood/setting that can be meaningfully changed
   - Best option: a product commercial or a short narrative clip

4. **The diff should be visually dramatic.** Do not change something subtle. Change the setting from "beach" to "mountain." Change the music from "upbeat pop" to "cinematic orchestral." Judges need to SEE the difference instantly.

5. **Show the config file briefly.** Judges love seeing clean data structures. Flash the YAML config for 3-5 seconds. It signals technical depth without being boring.

6. **End with the big vision.** "This config file is also a structured scene graph. It is exactly what NVIDIA Cosmos, Runway GWM-1, and Google DeepMind's world models need as training data. We are building the file format for the AI-native video industry." One sentence, massive TAM expansion, move on.

### Risk mitigation

- **Record a backup demo video** at 3:30 PM even if the product is not polished. If something breaks at 4:45, you have a recording.
- **Pre-generate NanoBanana images** for the "after" version. If live generation fails, swap in pre-generated images and explain "we pre-cached this for demo speed."
- **Pre-generate Lyria audio** for both versions. Audio generation latency is the biggest risk. Have backup audio files ready.
- **Have a fallback "simplified demo"** that skips the regeneration step and just shows decomposition + diff.

### Pitch structure (3 minutes)

| Time | Content |
|------|---------|
| 0:00-0:20 | **Hook:** "Making 5 versions of a video means 5 copies of 5 GB. That's insane." |
| 0:20-0:50 | **Decomposition demo:** Upload video, show structured breakdown (scenes, audio, transitions) |
| 0:50-1:20 | **The diff:** Change 2 things in the config (setting + music). Show colored text diff. |
| 1:20-2:00 | **Regeneration:** NanoBanana regenerates visuals with same character in new setting. Lyria generates new audio. Side-by-side comparison. |
| 2:00-2:30 | **Business:** "Video agencies spend $200/hr managing versions. Our diff is 50 bytes, not 500 MB. Every brand, every studio, every creator needs this." |
| 2:30-3:00 | **Vision:** "And here is the kicker -- this structured representation is exactly what world models need as training data. We are not just building a video tool. We are building the file format for the AI-native video era." |

---

## THINGS THAT COULD GO WRONG (ALL IDEAS)

1. **API rate limits / quota exhaustion** -- At a hackathon with 100+ teams all hitting the same APIs, there may be throttling. Have error handling and fallbacks.
2. **API key issues** -- Double-check that your keys work for Gemini 3.1, NanoBanana 2, and Lyria before the hackathon starts.
3. **WiFi instability** -- Hackathon WiFi is notoriously unreliable. Consider using a phone hotspot as backup. Pre-download any models or libraries you need.
4. **Scope creep** -- The biggest killer. Define your MVP at 10:30 AM and stick to it. Resist the urge to add features.
5. **Demo day timing** -- If demos are at 5:00 PM sharp, you need to stop coding at 4:00 PM and spend the last hour on demo prep and rehearsal. Most teams code until 4:55 PM and stumble through the demo.

---

## FINAL RECOMMENDATION

**Build Idea 2: Git for Video.**

It is the only idea that:
- Uses all three APIs (Gemini + NanoBanana + Lyria) in a way that feels natural
- Has a visual "whoa" moment (side-by-side video diff + regeneration)
- Has a clear, immediate business case (video versioning is a real pain point)
- Can be pitched as a product, not a research project
- Has the world model angle as a TAM expander without leading with it
- Is buildable (though tight) in 6.5 hours by two people

The main risk is time. You are building a complete pipeline (decomposition + diff + regeneration + UI) in 6.5 hours. Every minute counts. Pre-work everything you legally can (repo setup, boilerplate, API wrappers, demo video selection) before 10:30 AM.

Your track record (2nd at TreeHacks, 2nd at Browser Use) suggests you can execute under time pressure. This idea rewards execution speed because the individual components (PySceneDetect, Gemini structured output, NanoBanana regeneration, Lyria music) are all API calls -- the value is in the integration and the vision, not in any single technical breakthrough.

Win this one.
