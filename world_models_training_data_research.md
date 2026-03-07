# Deep Research: How World Models and Video Generation Models Are Trained -- The DATA Side

**Research Date:** March 7, 2026
**Scope:** Training data sources, volumes, preprocessing, controversies, and the data bottleneck for video generation and world models

---

## PART 1: How Video Generation Models Were Actually Trained

### 1.1 OpenAI Sora

**Known Training Data Sources:**
- OpenAI stated they used "publicly available and licensed data"
- Confirmed partnership with **Shutterstock** (six-year agreement announced July 2023) and **Pond5** for licensed video/image content
- CTO Mira Murati told the Wall Street Journal that the company uses "free content from the web and licensed content from Shutterstock"
- OpenAI admitted that it was "impossible" to build the technology without copyrighted data

**Evidence of YouTube and Game Content:**
- The Washington Post investigation found that Sora can generate videos mimicking Netflix shows, TikTok clips, and Twitch streams
- Tests revealed Sora could generate Super Mario Bros. gameplay, first-person shooter footage resembling Call of Duty/Counter-Strike
- A generated video featured the likeness of Twitch streamer Auronplay (Raul Alvarez Genes), including his forearm tattoo
- Over 70% of public video datasets commonly used in AI research contain content scraped from YouTube
- When asked directly by WSJ, Murati grimaced and said she was "not sure" whether Sora was trained on YouTube videos

**Lawsuits and Legal Status:**
- OpenAI has NOT yet faced a copyright suit specifically over Sora's training data
- A group of YouTube creators sued OpenAI after NYT reported it transcribed millions of hours of YouTube audio for ChatGPT
- After launching Sora 2, OpenAI initially allowed copyrighted characters unless rightsholders opted out, then reversed to an opt-in model within 3 days
- Disney invested $1 billion in OpenAI and licensed characters (Mickey Mouse, Cinderella) for Sora use

**Sources:**
- [Washington Post Investigation](https://www.washingtonpost.com/technology/interactive/2025/openai-training-data-sora/)
- [TechCrunch: Sora Trained on Game Content](https://techcrunch.com/2024/12/11/it-sure-looks-like-openai-trained-sora-on-game-content-and-legal-experts-say-that-could-be-a-problem/)
- [VentureBeat: Devil in the Data Details](https://venturebeat.com/ai/openais-sora-the-devil-is-in-the-details-of-the-data)
- [YouTube CEO on Terms Violation](https://petapixel.com/2024/04/08/youtube-ceo-says-it-is-a-problem-if-openai-scraped-videos-for-sora/)
- [Sora System Card](https://openai.com/index/sora-system-card/)

---

### 1.2 Google Veo (Veo 1, 2, 3)

**Training Data Sources:**
- Google confirmed using YouTube videos to train Veo 3 and Gemini
- Google's catalog includes **20 billion YouTube videos**; training on just 1% would amount to 2.3 billion minutes of content
- Veo 3 technical report states: trained on **over 20 million hours of video content** and corresponding audio streams from licensed cinema footage, documentaries, sports broadcasts, and user-generated content
- Annotations generated using Gemini models at different levels of detail, with filters for unsafe captions and PII

**Legal/Ethical Issues:**
- Creators were NOT informed their content was being used -- CNBC found that none of the creators they spoke with knew
- YouTube ToS grants Google "a worldwide, non-exclusive, royalty-free, sublicensable and transferable license" to uploaded content
- Legal experts argue ToS agreement may not constitute a valid license for AI training
- Creators cannot opt out of Google using their content for its own AI models (only third-party training)
- Generated content could compete directly with the creators who made the training data

**Sources:**
- [CNBC: Google Using YouTube for Veo 3](https://www.cnbc.com/2025/06/19/google-youtube-ai-training-veo-3.html)
- [Veo 3 Technical Report (PDF)](https://storage.googleapis.com/deepmind-media/veo/Veo-3-Tech-Report.pdf)
- [YouTubers Surprised](https://petapixel.com/2025/06/20/youtubers-surprised-that-google-uses-their-videos-to-train-its-ai-models-veo-3/)
- [YouTube Confirms Without Creator Consent](https://www.netinfluencer.com/youtube-confirms-googles-use-of-platform-videos-for-ai-training-without-creator-consent/)

---

### 1.3 Runway (Gen-2, Gen-3, Gen-4)

**Training Data Controversy:**
- A leaked internal document (obtained by 404 Media) revealed Runway's Gen-3 training data included YouTube channels of thousands of media companies: Pixar, Netflix, Disney, Sony, VICE News, The New Yorker
- Individual YouTubers listed: Casey Neistat, Sam Kolder, Benjamin Hardman, Marques Brownlee (MKBHD)
- Employees were tasked with finding videos/channels related to keywords, then used YouTube video downloader tools via proxy to scrape without being blocked
- A spreadsheet included 14 links to non-YouTube sources, including a website dedicated to streaming pirated cartoons and movies with thousands of copyright complaints
- Estimated **15 million YouTube videos** scraped for Gen-3 training

**Lawsuit:**
- YouTuber **David Gardner** filed a proposed class action (February 24, 2026) in California federal court
- Allegations: Runway bypassed YouTube copyright protections, violated DMCA anti-circumvention provision (Section 1201(a))
- Seeks to represent broader class of rightsholders whose videos were scraped
- This is one of 84+ copyright cases against AI companies as of February 2026

**Sources:**
- [PC Gamer: Leaked Document](https://www.pcgamer.com/software/ai/a-leaked-document-indicates-runways-gen-3-ai-video-generation-tool-may-have-been-trained-on-youtube-videos-and-copyrighted-content-without-permission/)
- [VentureBeat: Runway Backlash](https://venturebeat.com/ai/runway-faces-backlash-after-report-of-copying-ai-video-training-data-from-youtube)
- [Gardner v. Runway AI Lawsuit](https://www.sahmcapital.com/news/content/youtuber-sues-runway-ai-in-latest-copyright-class-action-over-ai-training-2026-02-24)
- [Engadget: Trained on Thousands of YouTube Videos](https://www.engadget.com/ai/ai-video-startup-runway-reportedly-trained-on-thousands-of-youtube-videos-without-permission-182314160.html)

---

### 1.4 Stability AI -- Stable Video Diffusion (SVD)

**Training Data (Publicly Documented):**
- Multi-stage training beginning with Stable Diffusion 2.1 pretraining for visual representations
- Video pretraining on **Large Video Dataset (LVD)**: originally 580 million annotated video pairs
- Systematic curation removed 2/3 of data, resulting in **LVD-F** with 152 million high-quality examples
- Curation used: optical flow (removing static scenes), OCR (filtering excessive text), CLIP/aesthetic scoring
- Fine-tuning on ~250,000 richly captioned, high-fidelity video clips at 576x1024 resolution
- Three synthetic captions per clip: image-only caption model, video caption model, LLM to combine both

**Compute Requirements:**
- ~200,000 A100 80GB GPU-hours for training SVD checkpoints

**Sources:**
- [Hugging Face: SVD Model Card](https://huggingface.co/stabilityai/stable-video-diffusion-img2vid-xt)
- [InfoQ: SVD Open-Source](https://www.infoq.com/news/2023/12/stable-video-diffusion/)

---

### 1.5 Kuaishou Kling

**Training Data:**
- Leverages Kuaishou's proprietary dataset (Kuaishou is China's second-largest short video platform after Douyin/TikTok)
- Trained on "publicly available data across the internet" including images and video sequences
- Exact dataset volume not publicly disclosed
- Careful data curation focused on reducing biases and increasing thematic/stylistic diversity

**Sources:**
- [Kuaishou Press Release](https://ir.kuaishou.com/news-releases/news-release-details/kuaishou-unveils-proprietary-video-generation-model-kling/)

---

### 1.6 Open-Sora 2.0 (Open-Source Reference Point)

Provides transparency into what commercial models hide:

**Training Data Pipeline:**
- Stage 1: ~70 million short video samples at 256x256
- Stage 2: ~10 million high-quality videos at 256x256
- Stage 3: ~5 million high-quality videos at 768px
- Hierarchical data pyramid with progressive quality filtering
- LLaVA-Video used to generate text descriptions for video samples
- Initialized on Flux (11B parameter text-to-image model)

**Preprocessing:**
- Remove short and low-quality videos
- Filter segments that are too fast/slow, contain too much text, are blurry, or have camera jitters
- Scene splitting using ffmpeg, PySceneDetector, OpenCV
- Dense captioning with visual-language models

**Cost:** Trained for approximately $200,000

**Sources:**
- [Open-Sora 2.0 Paper](https://arxiv.org/html/2503.09642v1)
- [Louis Bouchard Explainer](https://www.louisbouchard.ai/open-sora-2/)

---

### 1.7 Data Scale Comparison Table

| Model | Training Data Volume | Data Source | Publicly Documented? |
|-------|---------------------|-------------|---------------------|
| Sora / Sora 2 | Unknown (estimated petabytes) | Shutterstock, Pond5, web video, likely YouTube | Partially |
| Veo 3 | 20M+ hours video | YouTube (20B video catalog), licensed content | Yes (confirmed) |
| Runway Gen-3 | Est. 15M YouTube videos scraped | YouTube, pirated content sites | Leaked documents |
| Stable Video Diffusion | 580M video pairs -> 152M curated | LVD dataset, web video | Yes (paper) |
| Kling | Undisclosed | Kuaishou platform, web video | No |
| Open-Sora 2.0 | 70M -> 10M -> 5M clips | Web video | Yes (open-source) |

### 1.8 Common Video Data Preprocessing Pipeline

All major video generation models follow a similar data preprocessing pipeline:

1. **Raw Collection**: Web scraping, platform partnerships, licensed content
2. **Scene Splitting**: Cut long videos into coherent clips (ffmpeg, PySceneDetect)
3. **Quality Filtering**:
   - Optical flow analysis (remove static/too-fast scenes)
   - OCR detection (filter excessive text overlays)
   - CLIP aesthetic scoring
   - Blur detection, lighting checks
   - Resolution and aspect ratio filtering
4. **Deduplication**: Remove near-duplicate clips using perceptual hashing
5. **Captioning**: Multi-level text descriptions using VLMs (Gemini, LLaVA, CogVLM2-Video)
6. **Caption Quality Filtering**: Train classifier on manually reviewed subset, auto-discard poor captions
7. **Safety Filtering**: Remove explicit, violent, or PII-containing content

**Sources:**
- [InfoQ: Training Data Preprocessing for Text-to-Video Models](https://www.infoq.com/articles/training-data-preprocessing-for-text-to-video-models/)
- [VidGen-1M Paper](https://arxiv.org/html/2408.02629v1)

### 1.9 Key Public Video Datasets Used in Research

| Dataset | Scale | Description |
|---------|-------|-------------|
| WebVid-10M | 10.7M clips, 52K hours | Low-quality, watermarked web videos |
| Panda-70M | 70M clips | High-res but includes static/flickering videos |
| InternVid | 7M videos, 760K hours, 234M clips | Large-scale with 4.1B words of description |
| HD-VILA-100M | 100M videos | Video-language pretraining dataset |
| LVD (Stability) | 580M annotated pairs | Used for SVD training |
| OpenHumanVid | 52.3M clips, 70.6K hours | Human-centric video generation |

---

## PART 2: How World Models Are Specifically Trained

### 2.1 Google DeepMind Genie (1, 2, 3)

**Genie 1 (February 2024):**
- Trained on **30,000 hours of Internet gameplay videos** from hundreds of 2D platformer games
- Learned fine-grained controls exclusively from internet videos without action labels
- Learned which parts of an observation are controllable, inferred diverse latent actions
- Self-supervised: no manual action annotation required

**Genie 2 (December 2024):**
- Autoregressive latent diffusion model
- Latent frames passed through autoencoder to large transformer dynamics model
- Trained with causal mask similar to LLMs
- Emergent capabilities: object interactions, complex character animation, physics, agent behavior modeling

**Genie 3 (August 2025):**
- Foundation world model trained from internet videos
- Generates endless variety of playable worlds from images, photographs, sketches
- Powers the **Waymo World Model** (announced February 2026)
- Specific training data volumes not disclosed

**Sources:**
- [Genie 3 Blog](https://deepmind.google/blog/genie-3-a-new-frontier-for-world-models/)
- [Genie 1 Paper](https://arxiv.org/html/2402.15391v1)
- [Genie 2 Blog](https://deepmind.google/blog/genie-2-a-large-scale-foundation-world-model/)

---

### 2.2 Runway GWM-1

**Architecture:**
- Autoregressive model built on top of Gen-4.5
- Generates one frame at a time based on past frames and control inputs
- Responds to control input in real time

**Training:**
- Post-trained Gen-4.5 on domain-specific data for three variants:
  - **GWM Worlds**: Video data for physics, lighting, geometry understanding
  - **GWM Robotics**: Robotics data for scene-change prediction from robot POV
  - **GWM Avatars**: Conversational character and speech data
- Working toward unifying domains under single base world model
- Exact datasets and scale not disclosed

**Sources:**
- [Runway Research: GWM-1](https://runwayml.com/research/introducing-runway-gwm-1)
- [TechCrunch: Runway World Model](https://techcrunch.com/2025/12/11/runway-releases-its-first-world-model-adds-native-audio-to-latest-video-model/)

---

### 2.3 Google UniSim

**Training Data:**
- Trained on diverse datasets from multiple sources:
  - Simulation engines (Habitat object navigation with HM3D)
  - Real-world robot data (Language Table Data)
  - Human activity videos
  - Image-description pairs
- Different datasets serve different dimensions: abundant objects (images), densely sampled actions (robotics), diverse movements (navigation)

**Architecture:**
- Video diffusion model predicting next variable-length observation frames
- Video U-Net with interleaved temporal and spatial attention
- Unified action space: all disparate datasets converted to common format
- Transformer embeddings from text descriptions and non-visual modalities (motor controls, camera angles)

**Key Innovation:** Careful orchestration of diverse datasets, each serving a different piece -- human instructions ("open the drawer") AND low-level controls ("move to x, y")

**Sources:**
- [UniSim Paper](https://arxiv.org/abs/2310.06114)
- [UniSim Project Page](https://universal-simulator.github.io/unisim/)
- [VentureBeat: UniSim](https://venturebeat.com/ai/deepmind-unisim-simulates-reality-to-train-robots-game-characters)

---

### 2.4 Self-Driving World Models

#### Tesla FSD

**Training Data:**
- Billions of miles of anonymous real-world driving data
- Over 100 years equivalent of driving scenarios from fleet of 6M+ vehicles
- 1.5 petabytes of driving data per training cycle
- 70,000 GPU hours per complete training cycle
- 8 cameras per vehicle providing 360-degree coverage

**Architecture:**
- 48 distinct neural networks working in concert
- Bird's Eye View transformations and occupancy networks
- Perception, prediction, and planning network hierarchy

**Data Engine:**
- Identifies scenarios where FSD made mistakes
- Collects targeted real-world examples
- Iterative retraining on failure cases

**Sources:**
- [Arrow: Tesla Data Engine](https://www.arrow.com/en/research-and-events/articles/autonomous-vehicle-training-and-teslas-data-engine-explained)
- [Tesla FSD Technical Details](https://www.fredpope.com/blog/machine-learning/tesla-fsd-12)

#### Wayve GAIA (1, 2, 3)

**GAIA-1:**
- 4,700 hours proprietary driving data from London (2019-2023)
- 9 billion trainable parameters
- Unsupervised sequence modeling: maps inputs to discrete tokens, predicts next token
- Uses video, text, and action inputs

**GAIA-2:**
- Multi-country dataset: UK, US, Germany
- Multiple vehicle platforms (cars and vans)
- Various sensor configurations and frame rates
- Video tokenizer with latent diffusion model (shift from GAIA-1's frame-by-frame approach)

**GAIA-3:**
- 15 billion parameters
- 5x more compute than GAIA-2
- ~10x more data than GAIA-2
- 9 countries across 3 continents
- Emphasis on safety-critical elements: pedestrians, cyclists, signs, traffic infrastructure

**Sources:**
- [Wayve GAIA-1](https://wayve.ai/thinking/scaling-gaia-1/)
- [Wayve GAIA-2](https://wayve.ai/thinking/gaia-2/)
- [Wayve GAIA-3](https://wayve.ai/thinking/gaia-3/)

#### Waymo World Model (February 2026)

- Built on top of DeepMind's Genie 3
- Trained on Waymo's proprietary driving data from 50M+ autonomous miles
- Cities: San Francisco, Phoenix, Los Angeles, Austin
- Produces jointly temporally consistent camera imagery AND lidar point clouds
- Can synthesize conditions never directly observed: snow, floods, fires, animals
- Post-training transfers Genie 3's 2D video knowledge into 3D lidar outputs

**Sources:**
- [Waymo World Model Blog](https://waymo.com/blog/2026/02/the-waymo-world-model-a-new-frontier-for-autonomous-driving-simulation/)

#### NVIDIA DRIVE Sim + Cosmos

**DRIVE Sim:**
- Simulation platform for AV verification/validation at scale
- Transitioned from game engine to simulation engine (Omniverse)
- Two reconstruction methods: virtual (fully synthetic 3D) and neural (augmented real-world data)

**Cosmos World Foundation Models:**
- Trained on **9,000 trillion tokens** from **20 million hours** of data
- Sources: real-world human interactions, environment, industrial, robotics, driving data
- Data processing: NeMo Curator pipeline processes 20M hours in 14 days on Blackwell (vs 3+ years on CPU)
- Cosmos tokenizers: 8x more compression than SOTA, 12x faster processing
- Adopted by: 1X, Agility Robotics, Figure AI, Skild AI, Uber

**Sources:**
- [NVIDIA Cosmos](https://www.nvidia.com/en-us/ai/cosmos/)
- [NVIDIA Cosmos Blog](https://blogs.nvidia.com/blog/cosmos-world-foundation-models/)
- [NVIDIA Cosmos Paper](https://arxiv.org/html/2501.03575v1)

---

### 2.5 Wayve's Simulation Approach (Not GTA)

Clarification on the Wayve/simulation connection:
- Wayve did NOT use GTA5 specifically for their simulation training
- They built their own procedural simulation environments
- Their simulated world is deliberately "cartoon-like" -- they found content fidelity matters more than photorealism
- Used image-to-image translation for domain transfer (sim-to-real)
- Procedural generation systems capture real-world characteristics as parameterized rules
- Multi-agent reinforcement learning creates diverse, performant, realistic agent behaviors

**Sources:**
- [Wayve: Simulation Training, Real Driving](https://wayve.ai/thinking/simulation-training-real-driving/)
- [Wayve: Learning to Drive in a Day](https://wayve.ai/thinking/learning-to-drive-in-a-day/)

---

### 2.6 Training Approaches Compared: Real Video vs Game Engines vs Simulation

| Approach | Pros | Cons | Examples |
|----------|------|------|----------|
| **Real-world video** | Authentic distribution, rich diversity | Expensive, slow, no labels, privacy issues | Wayve GAIA, Tesla FSD |
| **Game engines (GTA, Minecraft)** | Free labels, controllable, diverse weather/lighting | Sim-to-real gap, limited physics fidelity, ToS issues | DeepGTAV, VPT, DIAMOND |
| **Purpose-built simulators** | High control, safety, scalability | Less visual diversity, engineering cost | CARLA, NVIDIA DRIVE Sim, Wayve custom |
| **Internet video (unlabeled)** | Massive scale, diverse, cheap | No action labels, noisy, copyright issues | Genie 1/2/3, Dreamer 4, Cosmos |
| **Hybrid approaches** | Best of multiple worlds | Complexity, domain alignment | UniSim, 1X World Model, Cosmos |

---

## PART 3: The Data Problem for World Models

### 3.1 Why World Model Training Data Is Harder Than LLM Text Data

The fundamental asymmetry (articulated by Joel Jang, NVIDIA):

| Dimension | LLM Text Data | World Model Video/Embodied Data |
|-----------|---------------|--------------------------------|
| **Scale of human contribution** | Billions of people writing for centuries | Robots in controlled lab settings |
| **Nature of data** | "In the wild" from the internet | Collected intentionally, on-demand |
| **Parallelization** | Can scrape trillions of tokens simultaneously | Physical data collection is real-time, serial |
| **Cost per unit** | Essentially free (web scraping) | Hardware, operators, physical space required |
| **Diversity** | Naturally diverse (all of human knowledge) | Inherently constrained (specific embodiment, environment) |
| **Labels** | Text is self-supervised | Action labels are expensive and may not generalize |
| **Distribution** | Covers edge cases through sheer volume | Misses rare scenarios |

**Key Quote from Joel Jang:** "Teleoperation doesn't scale because it requires expensive hardware, skilled operators, physical space, and time that cannot be parallelized beyond the number of robots owned."

**Industry consensus:** Core practitioners believe the key lies in breaking through the data bottleneck. The production of real-world data has three limitations: scale cannot be increased, cost cannot be reduced, and diversity is insufficient. Embodied intelligence requires five years of patience; the data bottleneck awaits breakthroughs through simulation.

**Sources:**
- [Joel Jang: World Models and the Data Problem in Robotics](https://joeljang.github.io/world-models-for-robotics)
- [AI Insider: Remaining Bottlenecks for Humanoid Robotics](https://theaiinsider.tech/2026/01/15/what-are-the-remaining-bottlenecks-for-humanoid-robotics-a-physical-ai-study-finds-the-limits-are-physical-not-cognitive/)

---

### 3.2 The "Internet of Video" Equivalent

Joel Jang's proposal: Use humans as "robots that have already been deployed at scale":
- 8 billion humans x 16 waking hours/day = massive sensorimotor data
- Target: capture 100 million hours of egocentric human video (~150 human lifetimes)
- 1X Technologies already demonstrated this: 900 hours of egocentric human video + 70 hours of robot data

Existing large-scale video datasets serve as a partial equivalent:
- YouTube: 20 billion videos (Google's catalog)
- InternVid: 7 million videos, 760K hours
- Panda-70M: 70 million clips
- HD-VILA-100M: 100 million videos

But these lack **action annotations**, **embodied perspective**, and **physical interaction data**.

---

### 3.3 Synthetic Data Approaches

#### NVIDIA Omniverse and Isaac Sim

- **Isaac Sim**: Robotics simulation + synthetic data generation on Omniverse platform
- **Replicator**: Core extension for domain randomization
  - On-the-fly randomization of textures, lighting, object placement, backgrounds
  - No asset reloading required
- **Example**: Generated 90,000+ images to train DNN for forklift detection in AMR applications
- **Domain Randomization**: Forces models to generalize across broad range of conditions
- **NVIDIA Cosmos**: Bridges simulation and world models -- Omniverse scenes condition Cosmos to generate photoreal synthetic video

**Sources:**
- [NVIDIA Isaac Sim](https://developer.nvidia.com/isaac/sim)
- [NVIDIA Closing Sim2Real Gap](https://developer.nvidia.com/blog/closing-the-sim2real-gap-with-nvidia-isaac-sim-and-nvidia-isaac-replicator/)

#### Game Engine Approaches

- **Unreal Engine**: NDDS (NVIDIA Deep Learning Dataset Synthesizer), photo-realistic rendering
- **Unity**: BlenderProc pipeline, vKitti dataset recreation
- **Procedural Content Generation**: Infinite variation in environments, weather, lighting
- Key advantage: "You can obtain the labels almost for free"

#### How Much Does Synthetic Data Help vs Hurt?

**Benefits:**
- Free, precise annotations
- Infinite variation (weather, lighting, density)
- Safe generation of rare/dangerous scenarios
- Cost-effective and scalable

**The Sim-to-Real Gap:**
- Models overfit to simulation-specific artifacts
- Fail on real-world variations: lighting changes, textures, colors, reflections, sensor noise
- Without adaptation, synthetic-trained models deteriorate in real deployment
- Over 40% improvement achievable through generative diffusion models for domain transfer
- Domain randomization helps but doesn't fully solve the gap

**Sources:**
- [Sim-to-Real Gap Survey](https://link.springer.com/article/10.1007/s10489-022-04148-1)
- [SimWorld Paper](https://arxiv.org/html/2503.13952)

---

### 3.4 Researchers on the Data Bottleneck

**The challenge is fundamentally different from LLMs:**
- Text data is a closed, finite resource (projected exhaustion 2026-2032)
- Video data is theoretically abundant but practically hard to use for world models
- The bottleneck is not volume but **quality, diversity, and action-annotation**

**Emerging solutions:**
1. **Web-scale video pretraining** + small amounts of domain-specific data (1X approach)
2. **Simulation + world model hybrids** (NVIDIA Cosmos + Omniverse)
3. **Human egocentric data** at scale (1X, Generalist)
4. **Self-supervised learning** from unlabeled video (Genie, Dreamer 4)

---

### 3.5 Startups Focused on World Model Training Data

| Company | Focus | Notable Details |
|---------|-------|-----------------|
| **1X Technologies** | Humanoid robot world models | 900h egocentric human video + 70h robot data |
| **Generalist AI** | Embodied foundation models | 270,000+ hours real-world manipulation data, growing 10K hrs/week |
| **Cortex AI** (YC) | Large-scale workplace robot data | Physical world as training/evaluation set |
| **RoboStream** | End-to-end robot data workflows | Capture, annotate, teleoperate |
| **Parallel Domain** | Synthetic data for autonomy | Self-driving synthetic data, object permanence research with Toyota |
| **Applied Intuition** | AV simulation + synthetic data | End-to-end simulation for autonomous vehicles |
| **Waabi** | World foundation model for trucks | Waabi World for autonomous trucking |
| **Skild AI** | General-purpose robot intelligence | Using NVIDIA Cosmos for training data |

**Sources:**
- [1X World Model](https://www.1x.tech/discover/world-model-self-learning)
- [Generalist AI GEN-0](https://generalistai.com/blog/nov-04-2025-GEN-0)
- [Cortex AI (YC)](https://www.ycombinator.com/companies/cortex-ai)

---

### 3.6 Robotics Data, Dashcam Data, Drone Footage

**Robotics Datasets:**
- **Open X-Embodiment Dataset**: 1M+ real robot trajectories, 22 robot embodiments (largest open-source)
- **RH20T**: Comprehensive robotic dataset for diverse one-shot skills
- **Generalist GEN-0**: 270,000+ hours manipulation data

**Dashcam/Driving Data:**
- Tesla: billions of miles from 6M+ vehicles, 1.5 petabytes per training cycle
- Wayve GAIA-3: 9 countries, 3 continents
- Waymo: 50M+ autonomous miles

**Drone Footage:**
- Researchers built drone footage databases from YouTube: 13K videos, 1.5K hours at 1080p
- Used for learning camera movement control

**Egocentric Human Video:**
- 1X Technologies: 900 hours of first-person human activity
- Key insight: ego human data provides transferable prior for manipulation that maps well onto humanoid embodiment

---

## PART 4: The GTA Angle

### 4.1 How GTA5 Has Been Used for ML/AI Training

GTA5 became one of the most important synthetic data sources in computer vision history. Key uses:

**Autonomous Driving:**
- Intel Labs + Darmstadt University developed a software layer intercepting GTA5 graphics pipeline to auto-classify objects
- 480,000+ labeled virtual images generated for highway driving
- Variables extracted: following distance, lane markings, driving angle
- Researchers could freely modify weather, lighting, car density, pedestrian density

**Computer Vision Benchmarks:**
- Domain adaptation for semantic segmentation (GTA5 -> Cityscapes is a canonical benchmark)
- Object detection, depth estimation, SLAM

**Robotics and Navigation:**
- 2025 paper by Scucchia et al. demonstrated GTA V synthetic data is "qualitatively comparable to real-world data" for SLAM and Visual Place Recognition

**Sources:**
- [MIT Technology Review: Self-Driving Cars and GTA](https://www.technologyreview.com/2016/09/12/157605/self-driving-cars-can-learn-a-lot-by-playing-grand-theft-auto/)
- [Beyond GTA V Paper](https://arxiv.org/abs/1712.01397)
- [From Gaming to Research (2025)](https://arxiv.org/abs/2502.12303)

---

### 4.2 Datasets Derived from GTA5

| Dataset | Task | Scale | Year |
|---------|------|-------|------|
| **Playing for Data** | Semantic segmentation | 24,966 images, 19 classes | 2016 |
| **Playing for Benchmarks** | Multi-task vision | Multiple benchmarks | 2017 |
| **SAIL-VOS 3D** | Video object segmentation + mesh | 484 videos, 237,611 frames, 3.5M instances | 2020 |
| **GTASynth** | SLAM point clouds | Multiple sequences with ground truth poses | 2022 |
| **HRSD** | Monocular depth estimation | RGB-D dataset | - |
| **PreSIL** | Object detection | Detection dataset | - |
| **DeepGTAV** | Multi-task ML extraction | Open-source extraction framework | 2017+ |
| **GMVD** | Multi-view detection | GTA V + Unity, WACV 2023 | 2023 |

**Impact of SAIL-VOS:** Pre-training on SAIL-VOS improved IoU by 19%, and VideoMatch performance from 55% to 74% on unseen data.

**Sources:**
- [Playing for Data (2016)](https://arxiv.org/pdf/1608.02192)
- [SAIL-VOS and GTA V](https://www.unite.ai/synthetic-data-sail-vos-gta-v/)
- [DeepGTAV GitHub](https://github.com/David0tt/DeepGTAV)
- [GTA5 Dataset on Papers with Code](https://paperswithcode.com/dataset/gta5)

---

### 4.3 The Sim-to-Real Transfer Gap

**Core challenge:** Models trained on GTA5 visuals learn simulation-specific artifacts:
- GTA5's rendering engine has distinctive lighting, shadow, and texture characteristics
- NPC behavior is scripted, not realistic
- Physics engine approximates but does not match real-world dynamics
- Limited weather variation compared to real world

**Transfer performance:**
- Semantic segmentation models trained on GTA5 achieve reasonable performance on real-world data (Cityscapes) but with a notable domain gap
- Domain adaptation techniques (adversarial training, style transfer) can close much of the gap
- Best results come from mixing synthetic and real data

**Quantified improvements:**
- Over 40% improvement in sim-to-real transfer achievable with generative diffusion models
- SAIL-VOS pretraining: 19% IoU improvement on downstream tasks

---

### 4.4 What Would GTA6 Unlock That GTA5 Cannot?

GTA6 improvements that would matter for AI training:

| Dimension | GTA5 (2013) | GTA6 (Expected) | AI Training Impact |
|-----------|-------------|------------------|-------------------|
| **Resolution/Fidelity** | 1080p era graphics | Next-gen photorealism | Smaller sim-to-real gap |
| **World Size** | San Andreas (~80 sq km) | Expected larger map | More diverse training environments |
| **NPC Behavior** | Scripted, limited | More sophisticated AI | Better behavioral data for world models |
| **Physics** | Approximate | More realistic | Better physical interaction training |
| **Weather/Lighting** | 14 weather patterns | Expected more dynamic | Better environmental variation |
| **Vehicles** | 257 vehicle types | Expected more | More diverse object detection training |
| **Interiors** | Limited | Expected extensive | Indoor scene understanding |
| **Water/Marine** | Basic | Expected advanced | New domain for autonomous systems |

**Critical caveat:** Take-Two Interactive's CEO confirmed GTA6 does not use generative AI -- the game is entirely hand-crafted. Rockstar has historically been protective of their IP and hostile to modding tools that would enable data extraction, so AI researchers may face significant legal barriers.

---

### 4.5 Other Games Used for World Model Training

| Game/Environment | Use Case | Notable Research |
|-----------------|----------|------------------|
| **Minecraft** | World models, RL agents, embodied AI | OpenAI VPT (70K hours), DIAMOND, Dreamer 4, Oasis, MineDojo |
| **Counter-Strike** | Neural game engines | DIAMOND trained on CS:GO gameplay |
| **Atari Games** | RL benchmarks, world model evaluation | DIAMOND achieved 1.46 mean HNS on Atari 100K |
| **Habitat (Meta)** | Indoor navigation, embodied AI | HM3D scenes for UniSim |
| **CARLA** | Autonomous driving simulation | Purpose-built open-source driving simulator |
| **ASKA** | Generalization testing | Viking survival game for SIMA |
| **MuJoCo** | Physics-based control | External world model for robotics |

---

### 4.6 Minecraft as a World Model Training Environment

Minecraft is arguably the most important game for world model research:

**OpenAI VPT (2022):**
- 2,000 hours labeled contractor gameplay + 70,000 hours unlabeled internet videos
- Inverse Dynamics Model to infer actions from video
- First AI to craft diamond pickaxe in Minecraft
- Foundation model for Minecraft gameplay

**DIAMOND (NeurIPS 2024 Spotlight):**
- Diffusion world model for Minecraft and Atari
- Learns environment physics through frame prediction
- Works as standalone neural game engine
- Mean human normalized score of 1.46 on Atari 100K

**Dreamer 4 (2025):**
- 14B parameter autoregressive video diffusion model
- Trained on 2,541 hours of Minecraft gameplay videos (OpenAI VPT dataset)
- First agent to obtain diamonds in Minecraft purely from offline data
- Outperforms VPT offline agent using 100x less data
- Real-time interactive inference on single GPU

**Oasis by Decart:**
- Real-time Minecraft world model at 20 FPS
- Spatial autoencoder + DiT backbone
- Internally simulates physics, game rules, graphics
- Users can move, jump, pick up items, break blocks

**MineDojo (NVIDIA):**
- Research framework for embodied AI in Minecraft
- Dozens of predesigned challenges
- NeurIPS award winner
- Open-source

**Sources:**
- [OpenAI VPT](https://openai.com/index/vpt/)
- [DIAMOND Paper](https://arxiv.org/abs/2405.12399)
- [Dreamer 4 Paper](https://arxiv.org/abs/2509.24527)
- [Oasis Project](https://oasis-model.github.io/)

---

## SYNTHESIS AND KEY FINDINGS

### The Training Data Landscape

1. **Everyone is using YouTube.** Google confirmed it. Runway was caught doing it. OpenAI strongly implied it. YouTube's 20 billion videos represent the largest accessible video corpus on Earth, and it is being used extensively -- with or without permission.

2. **The legal situation is unresolved.** As of March 2026, there are 84+ copyright lawsuits against AI companies. No definitive court ruling on whether AI training constitutes fair use. The $1.5B Bartz v. Anthropic settlement signals that companies face real financial risk. The trend is moving toward licensing deals (Disney-OpenAI) and settlements.

3. **Data quality matters more than quantity.** Stability AI's SVD started with 580M pairs but curated down to 152M. Open-Sora 2.0 went from 70M to 5M clips. The preprocessing pipeline is as important as the raw data.

4. **World models face a fundamentally different data challenge than LLMs.** Text data is abundant and self-supervised. Physical interaction data requires expensive hardware, can't be parallelized, and doesn't cover edge cases naturally. The proposed solution: treat humans as robots and capture egocentric video at scale.

5. **The synthetic data approach is necessary but insufficient.** The sim-to-real gap is real and significant. Domain randomization helps. Generative diffusion models can close 40%+ of the gap. But pure synthetic training still underperforms real data. The best results come from hybrid approaches.

6. **GTA5 was a pioneer but has limitations.** The game enabled foundational work in domain adaptation and synthetic data for driving. But its 2013-era graphics, scripted NPCs, and approximate physics constrain its utility for modern world models. GTA6 could narrow the sim-to-real gap significantly through higher fidelity.

7. **Minecraft is the most important game for world model research.** Its simplicity, modifiability, and massive community-generated video corpus make it the ideal testbed. OpenAI VPT, DIAMOND, Dreamer 4, Oasis, and MineDojo all center on Minecraft.

8. **NVIDIA is building the infrastructure layer.** Cosmos (20M hours, 9T tokens), Omniverse, Isaac Sim, and the NeMo Curator pipeline represent the most comprehensive attempt to solve the training data problem for physical AI. Their data processing can handle 20M hours in 14 days on Blackwell.

9. **The data scale required is staggering.** NVIDIA Cosmos: 20M hours. Tesla: 1.5 petabytes per cycle. Google Veo: 20M+ hours. Compare this to the Open X-Embodiment Dataset (largest open-source robot dataset) at just 1M trajectories across 22 robots. The gap between what we have and what we need for physical AGI is enormous.

10. **The startups solving the data problem are the ones to watch.** Generalist AI (270K hours growing 10K/week), 1X Technologies (egocentric human video approach), Cortex AI (workplace robot data), and companies building on NVIDIA Cosmos will determine who wins the world model race.

---

## CONFIDENCE ASSESSMENT

| Finding | Confidence | Basis |
|---------|------------|-------|
| YouTube is primary training source for video gen models | HIGH | Confirmed by Google, leaked docs from Runway, strong evidence for OpenAI |
| Preprocessing pipeline details | HIGH | Multiple papers, open-source implementations |
| Genie/Dreamer architecture and data | HIGH | Published papers with technical details |
| Runway training data controversy | HIGH | Leaked documents, lawsuit filings |
| OpenAI Sora specific training data | MEDIUM | Circumstantial evidence, no full disclosure |
| GTA5 datasets and impact | HIGH | Published papers with benchmarks |
| World model data bottleneck analysis | HIGH | Multiple researchers and industry sources confirm |
| GTA6 potential for AI training | MEDIUM-LOW | Speculative, based on expected improvements |
| Synthetic data effectiveness quantification | MEDIUM | Varies significantly by domain and method |

---

## RECOMMENDED FOLLOW-UPS

1. **Track the Gardner v. Runway lawsuit** -- this could set precedent for video scraping cases
2. **Monitor Google's YouTube AI training policies** -- creator opt-out mechanisms may change
3. **Watch NVIDIA Cosmos adoption** -- the companies building on this infrastructure will shape the field
4. **Follow 1X Technologies and Generalist AI** -- their data collection approaches may define the winning strategy
5. **Track the Waymo World Model deployment** -- first major commercial application of Genie 3
6. **Monitor GTA6 modding community** -- if data extraction tools emerge, expect rapid AI research applications
7. **Watch for EU AI Act enforcement** -- training data transparency requirements may force disclosure
