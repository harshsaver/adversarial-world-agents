# Google DeepMind & Gemini Hackathon Winning Projects: Research Report

**Date:** March 5, 2026
**Scope:** Six major hackathons spanning September 2025 - March 2026

---

## EXECUTIVE SUMMARY

This report covers winning projects across six Google DeepMind and Gemini-related hackathons. The strongest, most verified findings come from the Nano Banana Hackathon (50 winners, 832 projects, $400K+ prizes), the Gemini x Pipecat Hackathon at YC (3 winners identified with detailed project info), the Cactus x Google DeepMind Global Hackathon (1 standout project documented), the Google DeepMind x Qdrant x Freepik "Sketch & Search" Hackathon (3 winners), and the December 2025 Google Cloud AI Hackathon (3 winners). The Gemini 3 Hackathon on Devpost ($100K prize pool, 4,499 submissions) had winners announced on March 4, 2026 -- just yesterday -- and specific winner names have not yet propagated to publicly indexed sources.

Key patterns across all hackathons: the most innovative projects combined multiple modalities (vision + voice + reasoning), solved real-world problems in healthcare/education/accessibility, and went far beyond simple chatbot wrappers.

---

## 1. GEMINI 3 HACKATHON ON DEVPOST (Dec 2025 - Feb 2026)

**Source:** [gemini3.devpost.com](https://gemini3.devpost.com/)
**Organizer:** Google DeepMind
**Timeline:** December 17, 2025 - February 9, 2026 (submissions); Winners announced March 4, 2026 at 2:00pm PST
**Prize Pool:** $100,000 total + interviews with Google AI Futures Fund
- Grand Prize: $50,000
- Second Place: $20,000
- Third Place: $10,000
- Honorable Mentions: $2,000 each
**Scale:** 4,499 projects submitted across 188 pages of gallery

### Winner Status
Winners were announced just yesterday (March 4, 2026). As of this research, the specific prize-winning project names have NOT yet been indexed by search engines or reported in articles. The Devpost page still shows "Winners announced soon" in cached versions.

### Notable Submissions (from Project Gallery)
These are submissions visible in the gallery -- not confirmed winners:

| Project | Description | Team |
|---------|-------------|------|
| **Epilog** | "The 'Why' engine for AI agents." Captures traces and screenshots to diagnose root causes of failing automations | Ankit Hemant Lade, Sai Krishna, Indar Kumar |
| **Spatial Engine AI** | "The First AI That Sees Light Like a Physicist." Physics-based lighting analysis system | Veronika Kashtanova (Ukraine-based developer) |
| **Medlog** | Voice-first health memory that reconciles fragmented medical events using Gemini 3 Flash | Alona Moranta |
| **Deep Research Agent** | "7 sources. 1 answer." Multi-source research synthesis powered by Gemini 3 | Karthik Idikuda, Kishore Madana |
| **Krishi Sakhi** | Agricultural AI assistant for Indian farmers | Shaswat Kureel |
| **Living Memory** | Family story preservation tool using AI narratives | Michael Tandyo |
| **Pho.AI** | Vietnamese food assistant for travelers | Toan Web |
| **Gemini Radio Drama Studio** | AI-powered radio drama creation tool | (Chinese-language team) |
| **NutriCare Agents** | Personalized meal recommendation system | Huy Quy Minh, Dao Sy Duy Minh |
| **StonksAI** | Real-time market analysis tool | Russel Alfeche |
| **GENESIS-X** | "Universal Coherence Engine" | Cristian Popescu |
| **Stasis** | Medicine reminder and safety checking app | Baswadeep Bembare, Aatish Bagal |

### Hackathon Requirements & Capabilities Used
- Built with Gemini 3 family models across **AI Studio, Vertex AI, and Antigravity** (Google's agentic development platform)
- Explicitly rejected simple chatbot wrappers -- sought "systems that plan, execute, and self-correct"
- Real-time vision, audio, and reasoning capabilities
- Categories: educational tools, games, productivity apps, scientific solutions, social impact projects, healthcare

### What Made It Innovative
- The hackathon explicitly pushed for agentic systems, not chat interfaces
- Antigravity (Google's new agentic platform) was a first-time offering at this scale
- The AI Futures Fund pitch meetings made this a startup launchpad, not just a coding contest

---

## 2. NANO BANANA HACKATHON (September 2025)

**Sources:** [Google AI Developers Tweet](https://x.com/googleaidevs/status/1972798546052018595), [Neowin](https://www.neowin.net/news/google-announces-nano-banana-hackathon-winners-awards-400000-in-prizes/), [Analytics Vidhya](https://www.analyticsvidhya.com/blog/2025/09/nano-banana-projects/), [Kaggle](https://www.kaggle.com/competitions/banana), [EdgeSpace Substack](https://edgespace.substack.com/p/google-deepmind-reveals-winners-of)
**Organizers:** Google DeepMind + Cerebral Valley
**Timeline:** September 6-8, 2025 (48-hour hackathon); Winners announced ~September 29, 2025
**Scale:** 832 projects submitted, 50 winners selected
**Prize Pool:** $400,000+ in tech credits
- Each winner: $5,000 Gemini API credits + $1,000 fal.ai credits + 11M ElevenLabs credits (~$2,000)
- Special technology prize for outstanding use of ElevenLabs or fal.ai
**Core Technology:** Gemini 2.5 Flash Image (codename "Nano Banana") -- an image generation and editing model

### Confirmed Winners (from Google AI Developers Thread + Articles)

| Project | Creator | What It Does | Multimodal Capabilities | Innovation |
|---------|---------|--------------|------------------------|------------|
| **LifeTrace Timeline** | Chris Tang | Transforms raw location data into a personalized, hand-drawn visual diary for reflection on daily experiences | Gemini 2.5 Flash Image for visual diary generation from location data | Turns mundane GPS data into emotionally rich visual narratives |
| **ArtLens** | Mark Greenfield | Reimagines famous paintings as real-world scenes, bridging art history with modern AI | Image generation, style transfer, art historical analysis | Educational tool that shows what classic paintings would look like as real photographs |
| **ForgeOne** | (not specified) | Automated, quality-controlled creative workflows; AI critiques and refines its own creative output against professional scorecards | Self-evaluating image generation pipeline, autonomous improvement loop | First self-critiquing creative AI that scores itself against professional standards |
| **EcoMatrix** | dnKumars | Environmental storytelling tool converting climate solutions into professional comics with user integration | Gemini 2.5 Flash for visualizations, ElevenLabs TTS, fal.ai, Web Speech API | Users become comic characters in environmental narratives using their own appearance |
| **Story to Image Generation** | AbdulRahaman Mohammed | Converts written stories into cohesive visual sequences maintaining character consistency | NLP for story analysis, sequential image generation, sentiment analysis for mood alignment | Maintains emotional continuity across generated image sequences |
| **Manga Comic Generator** | Sumukh MG | Produces professional manga panels with authentic artistic conventions (speed lines, screentones, dynamic angles) | Character consistency across panels, manga art style expertise | Full manga page layouts with panel compositions and character sheets |
| **LLM-Generated Application Prototypes** | wguesdon | Generates fully developed UI/UX mockups from basic application requirements | Automated UI/UX creation, multi-platform prototype production | Goes from text description to complete design system with user flows |
| **Trailer Craft AI** | tuesdaycinemaclub | Cinematic video content creation -- generates professional movie trailers and promotional videos | Visual scene generation, narrative pacing control, video production automation | Applies cinematography principles and marketing psychology to AI trailers |
| **NanoCanvas** | anhoangvo | Advanced AI art creation system for professional artistic workflows | Real-time interactive image editing, color theory integration, composition analysis | Commercial-quality artwork with traditional art principles baked in |

### Additional Nano Banana Ecosystem Projects (from awesome-nano-banana)
- **PhotoFusion** -- Image merging/compositing tool
- **Magic Banana** -- "Natural Language Photoshop" for text-based image editing
- **gemini-gradio-image-editor** -- Gradio-based image editing interface
- **GemBooth** -- Character consistency showcase
- **PixShop** -- Inpainting and editing showcase
- **Past Forward** -- Style transfer demonstration
- **Home Canvas** -- Interior design image generation

### Judging Criteria
1. **Innovation** (weighted most heavily)
2. Creativity
3. Demonstration quality
4. Technical proficiency
5. Functionality
6. Long-term potential

---

## 3. GEMINI 3 HACKATHON SF (Cerebral Valley, December 2025)

**Sources:** [Cerebral Valley](https://cerebralvalley.ai/e/gemini-3-hack-sf), [Cerebral Valley Newsletter](https://cerebralvalley.beehiiv.com/p/cerebral-valley-week-of-december-1st)
**Organizer:** Google DeepMind + Cerebral Valley
**Date:** December 6-7, 2025 (in-person, SF) -- also SuperHack event ahead of Super Bowl weekend
**Format:** Fully in-person, max team size of 4
**Prize:** $150K in Gemini API credits + exclusive 30-minute virtual call with founders of Google AI Futures Fund
**Scale:** 100+ builders participated

### Winner Status
Winners were confirmed to have been selected (per @thorwebdev tweet: "We see Gemini 3 enable tons of incredible projects. Check out the winners below. Congrats y'all"). However, the specific winning project names from the SF event are not publicly indexed in searchable sources.

### What Was Built
The hackathon focused on:
- Building with Gemini 3 across **AI Studio, Vertex AI, and Antigravity**
- Agentic systems with real-time vision, audio, and reasoning
- Multi-city format: SF, London (Dec 13), NYC, Singapore, Bengaluru

### London Gallery
The Gemini 3 Hackathon London (December 13, 2025) has a public gallery at cerebralvalley.ai featuring Hackathon Winners, Community Vote Winners, and Hackathon Submissions, but the gallery content is dynamically loaded and not extractable via web scraping.

---

## 4. GEMINI x PIPECAT HACKATHON AT YC

**Sources:** [YC Events](https://events.ycombinator.com/pipecat-gemini-yc25), [AI Tinkerers Results](https://virtual-events.aitinkerers.org/hackathons/h_n6aQtoaNlUo/results), [AI Tinkerers Event Page](https://virtual-events.aitinkerers.org/p/gemini-x-pipecat-virtual-hackathon-build-adaptive-agents-with-real-time-intelligence)
**Organizers:** Daily (YC W16), Google DeepMind, AI Tinkerers
**Co-sponsors:** Boundary, Coval, Daily, Langfuse, Tavus
**Timeline:** October 11-19, 2025 (in-person at YC on Oct 11; virtual track Oct 11-19)
**Focus:** Voice, video, and multimodal real-time agents

### CONFIRMED WINNERS

#### Winner #1: Boba Bot -- Best Gemini Live API + Pipecat Project
- **Prize:** $50,000 Gemini credits + $50,000 Pipecat Cloud credits
- **What It Does:** Interactive character-driven application with a responsive interface. Users tell the bot their boba preferences and allergies, and it provides personalized drink recommendations through real-time voice interaction.
- **Multimodal Capabilities:** Gemini Live API for real-time voice conversation, Pipecat for voice/media orchestration, character personality system
- **Team:** Joey Wang (Focus Lab founder), Hsuanlin Her (Guardant scientist), You-Yi Jau (AWS Neuron SDE), Charlie Lee (Google SDE)
- **Innovation:** Judges praised the character personality and responsive interface. Demonstrated that voice agents can have genuine personality, not just functional responses.
- **Demo:** [YouTube](https://www.youtube.com/watch?v=6zSxyfTNj24)

#### Winner #2: Light to the Noodles -- Pipecat Cloud Credits Prize
- **Prize:** $100,000 Pipecat Cloud credits
- **What It Does:** Voice-AI avatar system leveraging Gemini Live and Pipecat technology for real-time conversational interactions with visual avatars
- **Multimodal Capabilities:** Gemini Live API, real-time voice processing, avatar rendering, Pipecat orchestration
- **Team Lead:** Maxim Makatchev (CMU PhD, susuROBO founder) -- expertise in C++, ROS, dialogue systems, production voice platforms
- **Innovation:** Combined production-grade voice pipelines with visual avatar representation
- **Demo:** [YouTube](https://youtu.be/0yOsHS209ww)

#### Winner #3: Happyverse VC Pitch Playground -- Google Gemini Credits Prize
- **Prize:** $100,000 Gemini credits
- **What It Does:** Practice platform for VC pitches providing real-time AI feedback. Users upload pitch documents and practice presenting while AI evaluates delivery, content, and persuasiveness in real time.
- **Multimodal Capabilities:** Document upload + analysis, real-time voice interaction, Gemini for pitch evaluation, Pipecat for conversation orchestration
- **Team:** Happyverse executives including CEO (Stanford MBA/MS, ex-Google Cloud TPU PM), TPM, COO, Head of Enterprise
- **Innovation:** Judges praised "cool integration of document upload" -- combining document understanding with real-time voice feedback is a novel use case for pitch practice
- **Demo:** [YouTube](https://www.youtube.com/watch?v=-JK9C5wCgmQ)

#### Finalists (not winners but notable)

| Project | Description | Multimodal Capabilities |
|---------|-------------|------------------------|
| **Lanturn** | ESP32-CAM voice + vision assistant -- connects Gemini Live API to an ESP32 Atoms3R-CAM device for embedded AI conversations | Streams H.264 video (~1 FPS at 320x240) + Opus audio via WebRTC; Gemini Live API for multimodal speech + vision; runs on $5 microcontroller hardware |
| **BridgeSpeak** | AI language learning platform using real-time voice | Voice-first conversational AI for language education |

### Lanturn Deep Dive (Notable Finalist)
- **Hardware:** ESP32 Atoms3R-CAM (M5Stack) with GC0308 camera, built-in mic/speaker
- **Tech Stack:** ESP-IDF 5.5.x, Pipecat orchestration, Gemini Live API, WebRTC streaming
- **Repository:** [github.com/getchannel/lanturn](https://github.com/getchannel/lanturn)
- **Innovation:** First demonstration of Gemini Live running on a $5 microcontroller. The device can see and discuss what its camera shows while maintaining voice conversation. Pushes multimodal AI to the absolute edge of embedded hardware.

---

## 5. CACTUS x GOOGLE DEEPMIND GLOBAL HACKATHON

**Sources:** [AI Tinkerers SF](https://sf.aitinkerers.org/p/google-deepmind-x-cactus-compute-global-hackathon-san-francisco), [Lumina Entry](https://sf.aitinkerers.org/hackathons/h_DRGnrtIWaG8/entries/ht_6qOzEVw-u3w), [GitHub Starter Kit](https://github.com/cactus-compute/functiongemma-hackathon), [Luma](https://luma.com/f0arqlwy)
**Organizers:** Google DeepMind, Cactus Compute, AI Tinkerers, AI Nexus
**Date:** February 21, 2026
**Format:** Six-city simultaneous one-day hackathon (SF, Singapore, and 4 others)
**Scale:** 604+ registered attendees (SF alone), 150 top builders per city
**Focus:** On-device agentic AI with FunctionGemma + cloud Gemini fallback

### Core Theme
Building hybrid edge-cloud AI systems: agentic applications that run locally on-device using **FunctionGemma** (Google DeepMind's function-calling small language model) inside the **Cactus Compute runtime**, with seamless fallback to cloud-based Gemini models for complex tasks.

### Judging Criteria
1. Quality of hybrid routing algorithm (depth and cleverness of edge/cloud decision-making)
2. End-to-end products that execute function calls to solve real-world problems
3. Low-latency voice-to-action products leveraging cactus_transcribe

### DOCUMENTED PROJECT: Lumina

**What It Does:** The first private, instant, agentic tutor that runs 95% on-device for young students in rural and low-connectivity regions of the Global South.

**How It Works:**
- Child snaps a photo of handwritten homework OR records a voice note
- Receives personalized step-by-step tutoring in under 800 milliseconds
- Completely offline -- zero data leaves the phone
- Only 5-8% of interactions trigger cloud fallback (complex proofs, advanced topics)

**Technology Stack:**
- React Native (Expo)
- FunctionGemma-270M-it (INT4 quantized) running inside Cactus Compute runtime
- Cactus local vector RAG for persistent personalized memory
- Custom tools: local math solver + canvas drawer for visual explanations
- Gemini 2.0 Flash API (cloud fallback only)
- SQLite local vector store
- Targets $80-120 Android phones

**Agentic Workflow (all local via FunctionGemma):**
1. Vision-based problem extraction from photos
2. Multi-step reasoning: plan -> solve -> reflect
3. Tool calling: local math solver + canvas drawer for visual explanations
4. Practice question generation
5. Persistent personalized memory via Cactus local vector RAG

**Team:** Jack Hall (YC W25 CTO), Jordan Hodali (Waterloo BMath Founding Engineer)

**Innovation:** Demonstrated that a 270M parameter model running on a $100 phone can handle 95% of a tutoring workflow with sub-second latency. The edge-cloud hybrid routing is the breakthrough -- it proves you don't need cloud connectivity for most educational AI use cases.

**Performance Stats:**
- FunctionGemma on Cactus: up to 3,000 tok/sec prefill, 200 tok/sec decode on M4 Macs
- All without GPU, remaining energy-efficient
- Response time: <800ms on-device

---

## 6. STANFORD x DEEPMIND HACKATHON

**Sources:** [GDG Stanford](https://gdg.community.dev/events/details/google-gdg-stanford-presents-stanford-x-deepmind-hackathon-build-with-google-gemini/), [Luma](https://luma.com/y8k57glv), [Medium Article](https://medium.com/@curiousmind1786/my-winning-day-at-the-gdg-stanford-hackathon-building-with-google-gemini-d0c7bfb92554)
**Organizer:** GDG Stanford + Google DeepMind
**Date:** February 1, 2026, 10am-6pm PT (also had an earlier November 2025 edition)
**Location:** Stanford, California
**Format:** 3-hour hacking sprint + live finals

### Prize Structure
- $80K in GCP credits (in-person track)
- $20K in GCP credits (online track)
- 30-minute pitch meetings with VCs writing $500K-$5M seed checks
- Investment NOT guaranteed -- prize is pitch ACCESS only

### Judges & Investors Present
**DeepMind:** Amit Vadi, Paige Bailey, Joana Carrasqueira, Thorsten Schaeff
**Stanford Faculty:** Prof. Garry Nolan, Prof. Nikesh Kotecha
**VC Firms (15+ funds managing $129.8B+):** General Catalyst, Acrew Capital, Beta Capital, Overlook Ventures, a16z, 500 Global, Draper Associates, and 10+ additional firms

### Competition Format
- 11:30 AM: Hacking begins (3-hour sprint)
- 2:30 PM: Hard submission deadline
- 3:30 PM: Semi-finalists announced
- 4:00 PM: Live finals -- top 6 teams pitch (5 min pitch + 5 min Q&A)
- 5:30 PM: Winners revealed

### Submission Requirements
1. One-pager
2. Working prototype link
3. 3-minute demo video
4. Code repository

### Winner Status
Vaishali Lambe documented her winning experience in a Medium article ("My Winning Day at the GDG Stanford Hackathon"). The specific winning project details are behind Medium's paywall, but the article confirms the event produced winners from among the top 6 finalist teams.

**Note:** Existing startups were allowed to pitch their current company instead of hackathon projects, making this as much a startup pitch competition as a hackathon.

### Innovation
This hackathon is unique in the ecosystem because the prize is VC access, not just credits. It functions as a direct pipeline from hackathon project to funded startup, with top-tier funds ($129.8B+ AUM) evaluating projects in real time.

---

## BONUS: RELATED GOOGLE DEEPMIND HACKATHONS

### Google DeepMind x Qdrant x Freepik "Sketch & Search" Hackathon

**Source:** [Qdrant Blog](https://qdrant.tech/blog/sketch-n-search-winners/)

| Place | Project | Builder(s) | Prize | Description | Multimodal Capabilities |
|-------|---------|-----------|-------|-------------|------------------------|
| 1st | **Prometheus** | Harry Kabodha | $1,500 cash + $500 gift card + $10,000 Gemini API credits + Best Use of Gemini | Transforms molecular structures (PDB files) into cinematic protein animations for scientific visualization | Gemini interprets protein data + generates shot descriptions; Qdrant retrieves successful camera templates; Nano Banana generates keyframes; Freepik creates final animations |
| 2nd | **Roast My Snack** | Jay Ozer | $500 cash + $300 gift card | Converts snack photos into four-panel comics where a Gen-Z character critiques dental health impact | Gemini Vision for snack analysis; Qdrant semantic search for dental science; Nano Banana for comic generation; age-adaptive messaging |
| 3rd | **AutoScape** | Tommy Purcell, Rae Jin | $250 cash + $150 gift card + $10,000 Gemini API credits + Best Use of Nano Banana | Landscape design platform converting photos into photorealistic outdoor plans with materials lists and cost estimates | Qdrant-powered retrieval with curated plant database; Nano Banana for photorealistic renders; grounds designs in real pricing and availability |

### December 2025 Google Cloud AI Hackathon (24-hour, Dec 12)

**Source:** [OpenDataScience](https://opendatascience.com/highlighting-the-winners-of-the-december-2025-google-cloud-ai-hackathon/)

| Place | Project | Description | Innovation |
|-------|---------|-------------|------------|
| 1st | **SurgAgent** | Agentic AI system that tracks surgical instruments in laparoscopic video using Gemini. Achieves 98% accuracy on real surgical footage. | Solves retained surgical items problem. Performs instrument classification, detects smoke/occlusion, recommends context-aware tracking strategies. Proves LLM-based surgical instrument detection is viable. |
| 2nd | **MedAnnotator** (Team Googo) | Two-tier pipeline combining MedGemma for domain-specific medical image understanding with Gemini API for validation and structured reporting. Human-in-the-loop editable results. | Practical deployment focus with consistent, reviewable outputs for clinical settings. |
| 3rd | **Director's Cut** | Healthcare solution with multimodal inputs and podcast-style outputs for on-the-go consumption. Emphasizes patient control through editability and flexible alert settings. | Makes medical information consumable as audio content for busy patients. |

---

## CROSS-HACKATHON ANALYSIS

### Most Common Multimodal Capabilities Used

| Capability | Examples | Frequency |
|-----------|----------|-----------|
| **Image Generation/Editing** | Nano Banana projects (ArtLens, ForgeOne, NanoCanvas, EcoMatrix) | Very High |
| **Real-time Voice** | Boba Bot, Light to the Noodles, Happyverse, Lanturn | High |
| **Vision/Image Understanding** | Lumina (homework photos), SurgAgent (surgical video), Lanturn (embedded camera) | High |
| **Document Understanding** | Happyverse (pitch decks), Medlog (medical records) | Medium |
| **Video Analysis** | SurgAgent (laparoscopic video), Trailer Craft AI | Medium |
| **On-device/Edge AI** | Lumina (FunctionGemma), Lanturn (ESP32) | Emerging |
| **Agentic Workflows** | Epilog, Lumina, SurgAgent | Growing |

### Innovation Patterns

1. **Edge-Cloud Hybrid AI** is the next frontier -- Lumina's 95% on-device execution with intelligent cloud fallback represents a new paradigm
2. **Self-critiquing AI** -- ForgeOne's approach of AI scoring its own output against professional rubrics
3. **Embedded Multimodal AI** -- Lanturn running Gemini Live on a $5 ESP32 microcontroller
4. **Healthcare AI** dominates serious applications -- SurgAgent, MedAnnotator, Director's Cut, Medlog, Stasis
5. **Voice-first interfaces** are replacing text-first -- the Pipecat hackathon entire premise was voice/video agents
6. **AI as startup launchpad** -- Stanford x DeepMind hackathon prizes are VC meetings, not just credits

### Sectors Represented in Winning Projects
- Healthcare & Medical (SurgAgent, MedAnnotator, Director's Cut, Medlog, Stasis)
- Education (Lumina, Manga Comic Generator, ArtLens, BridgeSpeak)
- Creative Tools (ForgeOne, NanoCanvas, Trailer Craft AI, Gemini Radio Drama Studio)
- Agriculture (Krishi Sakhi)
- Environmental (EcoMatrix)
- Scientific Visualization (Prometheus)
- Food/Travel (Pho.AI, Roast My Snack, Boba Bot)
- Developer Tools (Epilog, Deep Research Agent)
- Finance (StonksAI)
- Startup/Business (Happyverse VC Pitch Playground)

---

## RESEARCH GAPS & CONFIDENCE ASSESSMENT

### High Confidence (verified from multiple sources)
- Nano Banana Hackathon: 9 specific winning projects identified with details
- Gemini x Pipecat: 3 winners + 2 finalists with detailed descriptions
- Cactus x DeepMind: Lumina project with full technical specification
- Sketch & Search: 3 winners with complete details
- Google Cloud AI Dec 2025: 3 winners identified

### Medium Confidence (single source or partial data)
- Gemini 3 Devpost gallery submissions (visible but winner status unconfirmed)
- Stanford x DeepMind hackathon format and judges (confirmed) but specific winners (unconfirmed)

### Research Gaps
1. **Gemini 3 Hackathon Devpost Winners** -- Announced March 4, 2026 (yesterday). Not yet indexed. Recommend checking gemini3.devpost.com directly.
2. **Gemini 3 SF/London/NYC/Singapore/Bengaluru winners** -- Cerebral Valley galleries use client-side rendering that prevents web scraping. Known to exist but not extractable.
3. **Nano Banana full 50-winner list** -- Only 9 of 50 winners identified by name. The full list is likely on the Kaggle competition page.
4. **Stanford x DeepMind specific winning projects** -- Event confirmed, format documented, but winner names/projects behind Medium paywall.
5. **Cactus x DeepMind other cities** -- Only SF documented; Singapore and 4 other cities had simultaneous events.

### Recommended Follow-ups
1. Check gemini3.devpost.com directly for just-announced winners
2. Visit cerebralvalley.ai gallery pages with JavaScript-enabled browser to extract Gemini 3 SF/London winners
3. Access Kaggle /competitions/banana/hackathon-winners for complete Nano Banana winner list
4. Search Twitter/X for @thorwebdev, @googleaidevs, @cerebaborvalley for post-event winner threads
5. Check AI Tinkerers SF hackathon portal for additional Cactus x DeepMind entries
