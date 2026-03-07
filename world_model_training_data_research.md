# World Model Training Data: Comprehensive Research Report
## Video Decomposition, Structured Data, Human-as-Sensor, and Scene Graphs

**Date:** 2026-03-07
**Classification:** EXISTS / PROPOSED / THEORETICAL for each finding

---

## QUESTION 1: Has Anyone Built a Pipeline That Decomposes Video into STRUCTURED World Model Training Data?

### Executive Summary

**YES -- pipelines exist that decompose video into structured representations (scene graphs, causal graphs, physics relationships). BUT: No major world model (Cosmos, Genie, Sora, Runway) actually uses these structured representations for training. They all train on raw pixels/latent tokens + text captions. The structured decomposition pipelines exist in parallel research tracks that have NOT been integrated into mainstream world model training.**

This is the single most important finding: there is a gap between video scene graph research and world model training research. They are two communities that have barely connected.

---

### What EXISTS (Built, Running, Published Code)

#### 1. Synthetic Visual Genome 2 (SVG2) -- February 2026
**Status: EXISTS -- Fully automated pipeline with code and dataset**

The closest thing to what you described. A fully automated pipeline that:
- Takes raw video as input
- Runs multi-scale panoptic segmentation (SAM2)
- Tracks objects across frames with online-offline tracking
- Generates per-trajectory textual descriptions (DAM-3B-Video)
- Extracts object names, attributes via GPT-4-nano
- Infers spatio-temporal relations via GPT-5
- Outputs structured scene graphs with entities, attributes, and relations

**Scale:** 636K videos, 6.6M objects, 52M attributes, 6.7M relations

**Relation taxonomy includes:**
- Spatial relations (3D/depth-aware reasoning)
- Functional contact and manipulation (physical interactions)
- Stateful attachment (persistent physical association)
- Motion relations (relative movement across time)
- Social interactions (between animate entities)
- Attentional relations (gaze/visual focus)
- Event-level relations (temporally extended, goal-directed, CAUSAL dynamics)

**Output format:** Structured autoregressive text format aligned with scene-graph schema (triplet: subject-relation-object with temporal localization)

**Trained model:** TraSeR -- converts raw video + panoptic trajectories into spatio-temporal scene graphs in a single forward pass.

**Critical caveat:** SVG2 is used for video question-answering benchmarks, NOT for training world models. Nobody has taken SVG2 data and used it to train a world model.

Sources:
- https://arxiv.org/abs/2602.23543
- https://arxiv.org/html/2602.23543

#### 2. Action Genome -- CVPR 2020
**Status: EXISTS -- Dataset and benchmark with code**

- 10K videos, 0.4M objects, 1.7M visual relationships
- Frame-level scene graph labels: 234K frames, 476K bounding boxes
- 35 object classes, 25 relationship classes (Attention, Spatial, Contacting)
- Decomposes actions into spatio-temporal scene graphs capturing changes between objects

Sources:
- https://arxiv.org/abs/1912.06992

#### 3. Panoptic Video Scene Graph Generation (PVSG) -- CVPR 2023
**Status: EXISTS -- Dataset and benchmark**

- 400 videos, 150K frames
- Pixel-accurate segmentation masks + temporal scene graphs
- 126 object classes, 57 relation classes
- First long-video dataset with panoptic segmentation + scene graphs

Sources:
- https://arxiv.org/abs/2311.17058
- https://jingkang50.github.io/PVSG/

#### 4. PSG-4D -- NeurIPS 2023 Spotlight
**Status: EXISTS -- Dataset and model (PSG4DFormer)**

- 3K RGB-D videos, 1M frames
- 4D panoptic segmentation masks + dynamic scene graphs
- Nodes = entities with location/status; Edges = temporal relations
- Includes integration with LLM for scene understanding

Sources:
- https://github.com/Jingkang50/PSG4D

#### 5. Visual Causal Discovery Network (V-CDN) -- NeurIPS 2020
**Status: EXISTS -- Code and pretrained models available**

- Extracts causal relationships from video of physical systems
- Perception module: unsupervised keypoint extraction
- Inference module: graph neural networks infer interaction variables
- Dynamics module: predicts future movements
- Tested on multi-body interaction and fabric scenarios
- Supports counterfactual predictions

Sources:
- https://proceedings.neurips.cc/paper/2020/hash/6822951732be44edf818dc5a97d32ca6-Abstract.html
- https://github.com/pairlab/v-cdn

#### 6. ConceptGraphs -- ICRA 2024
**Status: EXISTS -- Open source, used in robotics**

- Builds open-vocabulary 3D scene graphs from RGB-D video
- Uses 2D foundation models (segmentation + CLIP + VLMs)
- Extracts entities, semantic features, inter-object relations
- Output translatable to text for LLM-based task planning
- Demonstrated on robot manipulation tasks

Sources:
- https://concept-graphs.github.io/
- https://arxiv.org/abs/2309.16650

#### 7. Neural Physics Engine -- MIT CSAIL
**Status: EXISTS -- Research prototype**

- Factorizes object dynamics into pairwise interactions
- Models future state as composition of pairwise interactions
- Can infer latent properties like mass
- Generalizes to different numbers of objects

Sources:
- https://www.csail.mit.edu/research/neural-physics-engine

#### 8. Graph Networks as Learnable Physics Engines -- ICML 2018
**Status: EXISTS -- Published and replicated**

- Nodes = physical states of particles
- Message-passing = pairwise interactions between particles
- Neighbor aggregation = total interaction effects
- Used for inference and control in physical systems

Sources:
- http://proceedings.mlr.press/v80/sanchez-gonzalez18a/sanchez-gonzalez18a.pdf

---

### What is PROPOSED (Papers Published, Some Code, Not Production)

#### 1. Generate Any Scene -- Scene Graph Driven Data Synthesis (Dec 2024)
**Status: PROPOSED -- Paper published, concept demonstrated**

- Uses scene graphs as the SOURCE for generating training data (reverse direction)
- Enumerates diverse scene graph structures
- Translates scene graphs into captions for text-to-image/video generation
- Addresses compositional generalization gaps

Sources:
- https://arxiv.org/abs/2412.08221

#### 2. Loci-Looped -- Object Permanence Learning (2024)
**Status: PROPOSED -- Paper published**

- Slot-based autoregressive system that learns object permanence from video
- Tracks objects through occlusions
- Shows "surprise" at implausible object behavior
- Fuses latent imaginations with pixel observations

Sources:
- https://arxiv.org/abs/2310.10372

#### 3. Graph World Model (GWM) -- ICML 2025
**Status: PROPOSED -- Paper and code, but not video-specific**

- World model that operates on graph-structured states
- Two variants: text-based (GWM-T) and embedding-based
- Tested on 6 task types (generation, recommendation, graph prediction, multi-agent, RAG, planning)
- NOT specifically for video -- operates on abstract graph data

Sources:
- https://arxiv.org/abs/2507.10539
- https://github.com/ulab-uiuc/GWM

#### 4. Semantic World Models (Oct 2025)
**Status: PROPOSED -- Paper and code**

- World model as action-conditional VLM answering questions about future
- Based on PaliGemma (3B params)
- Predicts semantic effects of actions rather than pixel reconstructions
- Demonstrated on robotics tasks

Sources:
- https://arxiv.org/abs/2510.19818
- https://weirdlabuw.github.io/swm/

---

### What is THEORETICAL (Discussed But Not Built)

- A unified pipeline that extracts physics, causality, object permanence, 3D structure, AND scene graphs from arbitrary internet video, packaged as world model training data -- **this does not exist**
- A standard data format/schema for "structured world model training data" -- **no standard exists**
- Integration of SVG2-style scene graph extraction into NVIDIA Cosmos or similar training pipelines -- **not done**

---

## QUESTION 2: Has Anyone Built a "Human-as-Sensor" Crowdsourced Data Collection System for World Models?

### Executive Summary

**PARTIAL YES. Several systems exist for crowdsourced egocentric data collection, but NONE are specifically designed to collect structured world model training data (physics, interactions, spatial data) from regular people walking around. The closest systems collect video + sensor data, not structured physics data.**

---

### What EXISTS

#### 1. Project Aria (Meta) -- Gen 1 and Gen 2
**Status: EXISTS -- Hardware deployed, data collected**

- Wearable glasses with: RGB camera, 6DOF SLAM cameras, eye tracking, spatial microphones, IMUs, barometer, magnetometer, GNSS
- 6DOF tracking via Visual Inertial Odometry
- Used by 200+ academic and corporate partners
- Tens of thousands of egocentric gaze recordings collected
- Data used for Ego-Exo4D dataset

**Key limitation:** Collects raw sensor streams, NOT structured physics/interaction data. The structuring happens post-hoc via annotations.

Sources:
- https://www.projectaria.com/
- https://ai.meta.com/blog/aria-gen-2-research-glasses-under-the-hood-reality-labs/

#### 2. Ego4D -- Meta + 13 Universities
**Status: EXISTS -- 3,670 hours collected**

- 931 participants, global naturalistic settings
- Multimodal: video + audio + IMU + eye gaze + 3D meshes
- Annotations include: object bounding boxes, hand-object state changes, visual query tracks, activity taxonomy (110 classes), future anticipation labels
- Benchmark tasks: episodic memory, forecasting, hand-object interaction

**Key limitation:** Participants are researchers/annotators, not general public "walking around." Annotations are added post-collection, not captured in real-time.

Sources:
- https://ego4d-data.org/
- https://ai.meta.com/blog/ego-exo4d-video-learning-perception/

#### 3. Ego-Exo4D
**Status: EXISTS -- Foundational dataset**

- Combined egocentric (Aria glasses) + exocentric (external cameras) views
- Released Nov 2023, updated March 2024
- Collected by Meta FAIR + 15 university partners

Sources:
- https://ego-exo4d-data.org/

#### 4. EPIC-KITCHENS
**Status: EXISTS -- 55 hours, 32 participants**

- Egocentric video in native kitchen environments
- 10 nationalities, 4 countries
- 39.6K action segments, 454.2K object bounding boxes
- Participants narrated their own videos (reflecting true intention)
- Annotations crowdsourced via Amazon Mechanical Turk

Sources:
- https://epic-kitchens.github.io/

#### 5. DROID -- Distributed Robot Interaction Dataset
**Status: EXISTS -- 76K demonstrations, 350 hours**

- 50 data collectors across 13 institutions
- North America, Asia, Europe
- 18 robots, 564 scenes, 86 tasks
- Teleoperation via Oculus Quest 2
- Crowdsourced language annotations on HuggingFace

Sources:
- https://droid-dataset.github.io/
- https://arxiv.org/abs/2403.12945

#### 6. RoboCrowd (Nov 2024)
**Status: EXISTS -- Research prototype**

- Crowdsourcing in-person demonstrations via ALOHA bimanual platform
- In public environments
- Three incentive mechanisms: material rewards, intrinsic interest, social comparison

Sources:
- https://arxiv.org/abs/2411.01915

#### 7. Sensei (YC Company, Founded 2024)
**Status: EXISTS -- Company operating**

- Low-cost sensorized exoskeleton arm (<$300)
- Network of paid human operators
- Data collection at 1/10th cost, 2x speed vs traditional teleoperation

Sources:
- https://www.ycombinator.com/companies/sensei

#### 8. RoboTurk (Stanford)
**Status: EXISTS -- Research platform**

- 6DOF motion control via smartphone
- Maps phone movement to robot arm movement
- Multiple simultaneous users

Sources:
- https://roboturk.stanford.edu/

---

### What Does NOT Exist

**A system where regular people walk around with phones/wearables specifically designed to collect structured world model training data (physics relationships, interaction data, causal chains, spatial structure) at scale.**

All existing systems either:
1. Collect raw video/sensor streams and structure them later (Ego4D, Project Aria)
2. Require specialized hardware and supervised environments (DROID, RoboCrowd, Sensei)
3. Focus on specific tasks (kitchens, robotics manipulation) not general world understanding

The concept of "human-as-sensor for world models" as you described it -- **does not exist as a built system.**

---

## QUESTION 3: How ARE World Models Actually Trained on Video Data?

### Executive Summary

**The universal answer is: video tokenization into latent representations + text captions. NO major world model extracts scene graphs, physics, or structured representations during preprocessing. The "structure" is learned implicitly by the model from raw pixels/tokens.**

---

### The Actual Pipeline (Verified Across Multiple Models)

#### Step 1: Video Collection and Splitting
- Raw internet video collected at massive scale
- Scene detection (TransNetV2, PySceneDetect) splits videos into coherent clips
- Clips typically 2-60 seconds

#### Step 2: Filtering (Quality Control)
Multiple filters remove unsuitable content:
- **Motion filtering:** Remove static videos, classify camera motion types
- **Visual quality filtering:** Remove blurry, noisy, overexposed clips (DOVER model, aesthetic scoring)
- **Text overlay filtering:** Remove videos with post-produced text overlays
- **Content type filtering:** Remove animation, video games, abstract content
- **Optical flow scoring:** Filter by motion dynamics (UniMatch)

#### Step 3: Captioning/Annotation
- VLM generates text description for each clip
- NVIDIA Cosmos: VILA 13B, 8 uniformly sampled frames, ~97 words per caption
- OpenAI Sora: Re-captioning technique from DALL-E 3, GPT expands short prompts
- Open-Sora: LLaVA or GPT-4V for fine-grained captions

#### Step 4: Deduplication
- Semantic deduplication to create diverse but compact training sets

#### Step 5: Tokenization
- Video autoencoder compresses video into latent tokens
- NVIDIA Cosmos: spatial compression 8x8 or 16x16, temporal compression 4x or 8x
- Continuous tokens (16-dimensional vectors) or discrete tokens (64K vocabulary)
- Sora: spacetime patches of video latent codes
- Open-Sora: Video DC-AE with 32x spatial compression, 4x temporal compression

#### Step 6: Model Training
- Diffusion models: learn denoising in latent space
- Autoregressive models: predict next latent token(s) conditioned on past
- Text captions used as conditioning signal
- NO scene graphs, NO physics extraction, NO causal structure mining

---

### Model-Specific Details

#### NVIDIA Cosmos (Verified from arXiv 2501.03575)
- **Input:** 20M hours of internet video
- **Output after preprocessing:** ~100M clips, each with VLM caption
- **Tokenizer:** Causal video tokenizer using wavelet transforms + 3D convolution
- **No structured extraction:** "No explicit physics extraction occurs. The pipeline contains no optical flow analysis for physics inference, no causal structure mining, and no dynamic scene decomposition."
- **Physics learning is IMPLICIT:** Models learn physics from predicting future tokens/denoising

#### Google DeepMind Genie (1, 2, 3)
- **Genie 1:** 200K hours of internet platformer videos, tokenized, latent action model infers actions
- **Genie 2:** Trained on general video, autoregressive transformer with causal mask
- **Genie 3:** Text-to-interactive-world, 24fps at 720p, autoregressive generation
- **No structured extraction:** Physics learned implicitly, no scene graphs

#### OpenAI Sora
- **Training on videos + images of variable durations/resolutions**
- **Spacetime patches** as basic representation unit
- **Re-captioning** via DALL-E 3 technique + GPT expansion
- **No structured extraction**

#### Runway Gen-4.5 / GWM-1
- **Autoregressive-to-Diffusion (A2D) architecture**
- **Block Size Annealing + Noise Level Annealing during training**
- **Latent space learned by pretrained autoencoder**
- **GWM-1 built on top of Gen-4.5 via domain-specific post-training**
- **No structured extraction disclosed**

#### Meta V-JEPA 2
- **Trained on 1M+ hours of video**
- **Predicts masked spatio-temporal regions in LATENT space (not pixels)**
- **Explicitly avoids pixel prediction -- focuses on semantic features**
- **No structured extraction**

---

### Critical Finding: The Physics Understanding Gap

Multiple 2025 benchmarks demonstrate that current video world models have SEVERELY LIMITED physics understanding despite visual realism:

- **Physics-IQ Benchmark:** Tests fluid dynamics, optics, solid mechanics, magnetism, thermodynamics. Current models (Sora, Runway, Pika, etc.) show "severely limited" physical understanding.
- **PhyWorld (ByteDance):** Models fail to abstract general physical rules, exhibit "case-based" generalization (mimicking closest training example). Scaling alone is insufficient.
- **T2VPhysBench:** Tests 12 fundamental physical laws. Prompt engineering and scaling are insufficient.

Sources:
- https://physics-iq.github.io/
- https://phyworld.github.io/
- https://arxiv.org/abs/2501.09038

---

## QUESTION 4: What Does Runway Actually Do With Video Structure?

### Executive Summary

**Runway decomposes video into structure (depth/geometry) and content (appearance/semantics) using separate encoders. They do NOT extract scene graphs or physics relationships. Their internal representations are learned latent spaces, not explicit structured data. They have published very few technical details about their world model internals.**

---

### What Runway Has Published

#### Gen-1 (2023) -- "Structure and Content-Guided Video Synthesis"
**Status: EXISTS -- Published ICCV 2023 paper**

The ONE paper where Runway explicitly describes video decomposition:
- **Structure representation:** Depth maps extracted via MiDaS (geometry, dynamics, shapes, locations, temporal changes)
- **Content representation:** CLIP embedding of a frame (appearance, semantics)
- These are separate encoders feeding into the diffusion model
- Structure is concatenated to the diffused latent; content conditions the process

This is NOT scene graph extraction. It is:
- Monocular depth estimation (MiDaS) for geometry
- CLIP embedding for semantics
- No entity extraction, no relationships, no physics

Sources:
- https://arxiv.org/abs/2302.03011

#### Gen-4.5 (Dec 2025) -- A2D Architecture
- Autoregressive-to-Diffusion architecture
- Maps input to latent space encoding visual patterns
- Physics capabilities described as "weight, inertia, liquids, cloth, physically plausible collisions"
- BUT: these are emergent properties of training, not extracted structure

#### GWM-1 (Dec 2025) -- General World Model
- Autoregressive, frame-by-frame generation
- "Learns an internal simulation" by predicting pixels
- Captures "physical laws, lighting, geometry, and causal relationships directly from video data"
- But "directly from video" means implicitly, NOT through structured extraction
- No technical paper published with architectural details

#### Research Publications
Runway's published research papers include:
- Latent Diffusion Models (LDM, the Stable Diffusion paper)
- Concept Steerers (k-sparse autoencoders for interpretable features)
- Revelio (interpreting semantic information in diffusion model layers)
- 3D Gaussian Splatting work (StochasticSplats)
- Progressive prompt detailing

**Notably absent:** Any paper on scene graphs, physics extraction, causal reasoning, or structured video decomposition.

Sources:
- https://runwayml.com/research/publications
- https://runwayml.com/research/introducing-runway-gwm-1
- https://runwayml.com/research/introducing-runway-gen-4.5

---

## QUESTION 5: Scene Graphs as World Model Training Data -- Real or Theoretical?

### Executive Summary

**Scene graphs exist as a mature technology for video understanding. They are used extensively for video QA, image generation conditioning, and robotics planning. However, they are NOT currently used to train the major world models (Cosmos, Genie, Sora, Runway). The connection between scene graph research and world model training is PROPOSED in several recent papers but has NOT been implemented at scale. This represents a significant research gap.**

---

### What EXISTS

#### Scene Graph Datasets for Video (Built and Available)
| Dataset | Year | Scale | Relations | Code |
|---------|------|-------|-----------|------|
| Visual Genome | 2017 | 108K images, 2.3M relationships | Spatial, descriptive | Yes |
| Action Genome | 2020 | 10K videos, 1.7M relationships | Attention, Spatial, Contacting | Yes |
| PVSG | 2023 | 400 videos, 150K frames | 57 relation classes | Yes |
| PSG-4D | 2023 | 3K RGB-D videos, 1M frames | Dynamic temporal relations | Yes |
| SVG2 | 2026 | 636K videos, 6.7M relations | Spatial, Contact, Motion, Causal, Social | Yes |

#### Scene Graphs Used FOR (Not As Training Data):
1. **Image/video generation conditioning:** "Generate Any Scene" uses scene graphs to create training captions for T2I/T2V models
2. **Video question answering:** SVG2 + TraSeR improves VQA accuracy by 1.5-4.6%
3. **Robotics planning:** ConceptGraphs builds 3D scene graphs for robot task planning
4. **Video understanding evaluation:** LLMs evaluated on scene graph understanding via TSG-Bench

#### Scene Graphs Used ADJACENT TO World Models:
1. **NVIDIA Cosmos Transfer:** Accepts structured inputs (segmentation maps, depth maps, trajectory maps) to condition video generation -- this is the closest to "structured input to world model"
2. **3D/4D World Modeling:** Scene graphs used as "semantic conditions" alongside geometric and action-based conditions
3. **Neurosymbolic approaches:** Scene graphs enriched with common sense knowledge for visual reasoning

---

### What is PROPOSED But NOT Built at Scale

#### Graph World Model (ICML 2025)
- Treats states as graphs and tasks as action nodes
- Demonstrates world modeling with graph-structured data
- BUT: operates on abstract graphs, not video scene graphs
- Has NOT been demonstrated with video-derived scene graphs as input

#### Using Scene Graphs as World Model Training Data
**This is the gap.** Multiple groups can:
- Extract scene graphs from video (SVG2, Action Genome, etc.)
- Train world models on video (Cosmos, Genie, Sora, etc.)

**Nobody has combined them:** taking SVG2-style scene graph extraction and using the output as training data for a world model. This is a proposed research direction, not an implemented system.

---

### What Does Training Data Actually Look Like?

Based on verified sources, here is the ACTUAL format of world model training data:

#### NVIDIA Cosmos Training Data Format:
```
For each training sample:
  - Video clip: mp4 file, 2-60 seconds, transcoded to consistent format
  - Caption: ~97 words, generated by VILA 13B VLM
  - Tokenized form: continuous (16-dim vectors) or discrete (64K vocab) latent tokens
  - Category tag: one of 9 categories (Driving 11%, Hand motion 16%, etc.)
```

#### OpenAI Sora Training Data Format:
```
For each training sample:
  - Video clip: variable duration/resolution/aspect ratio
  - Caption: detailed re-caption from DALL-E 3 technique
  - Tokenized form: spacetime patches of video latent codes
```

#### Google Genie Training Data Format:
```
For each training sample:
  - Video clip: 16 frames at 10 FPS
  - Tokenized form: discrete tokens from VQ-VAE video tokenizer
  - Latent actions: inferred from video (no explicit action labels)
  - NO text captions
```

**There is NO standard data format for structured world model training data.** Each system uses its own tokenizer and caption format.

---

### Is There a Standard Data Format?

**No.** The closest things to standards are:
1. **RLDS format** (used by DROID/Open X-Embodiment) -- for robotics trajectories
2. **Scene graph triplets** (subject-relation-object) -- used in VG, AG, SVG2 but no standard schema
3. **NVIDIA Cosmos Curator output** -- proprietary but documented format

---

## SYNTHESIS: The Big Picture

### The Gap You Have Identified Is Real

There is a verified, significant gap between:

1. **Video scene graph extraction** (which EXISTS and works at scale -- SVG2 processes 636K videos automatically)
2. **World model training** (which EXISTS and works at scale -- Cosmos trains on 20M hours)

These two capabilities have NOT been connected. Every major world model trains on:
- Raw video pixels compressed into latent tokens
- Text captions generated by VLMs
- That is it

Nobody is feeding structured scene graph data (entities + relationships + physical properties + causal chains) into world model training pipelines.

### Why This Gap Matters

The 2025 physics benchmarks prove that current world models have "severely limited" physical understanding despite visual realism. PhyWorld shows they use "case-based" generalization (pattern matching) rather than learning abstract physical rules. Scaling alone is insufficient.

### The V-JEPA Alternative

Meta's V-JEPA 2 represents a philosophically different approach:
- Predicts in LATENT/EMBEDDING space, not pixel space
- Explicitly designed to ignore unpredictable pixel details
- Focuses on semantic/structural aspects
- Has demonstrated better physics understanding

But even V-JEPA does not use explicit scene graphs or structured representations -- it learns latent structure implicitly.

### What Would Need to Be Built

To connect these two worlds, you would need:
1. An SVG2-like pipeline to extract structured scene graphs from internet video at scale
2. A training framework that can ingest both visual tokens AND structured graph data
3. A way to supervise the model with explicit physics/causal relationships rather than only next-token prediction
4. Evaluation frameworks (which DO exist: Physics-IQ, PhyWorld, T2VPhysBench)

This has NOT been built. It is an open research direction.

---

## Confidence Assessment

| Finding | Confidence | Source Quality |
|---------|-----------|---------------|
| Cosmos trains on raw pixels + captions only | Very High | Verified from arXiv technical paper |
| SVG2 pipeline exists and works at scale | Very High | Published paper + dataset |
| No major world model uses scene graphs for training | High | Verified across all major models |
| Physics understanding of current WMs is limited | Very High | Multiple independent benchmarks |
| V-JEPA 2 predicts in latent space not pixels | Very High | Official Meta publication |
| Runway has not published WM technical details | High | Verified via publications page |
| No standard format for structured WM data | High | No evidence of standard found |
| Human-as-sensor for world models does not exist | High | Exhaustive search found no match |
| Graph World Model (ICML 2025) exists | Very High | Published at top venue with code |

---

## Sources

### Scene Graph Extraction
- [SVG2 - Synthetic Visual Genome 2](https://arxiv.org/abs/2602.23543)
- [Action Genome](https://arxiv.org/abs/1912.06992)
- [PVSG](https://arxiv.org/abs/2311.17058)
- [PSG-4D](https://github.com/Jingkang50/PSG4D)
- [ConceptGraphs](https://concept-graphs.github.io/)
- [V-CDN Causal Discovery](https://github.com/pairlab/v-cdn)

### World Model Training
- [NVIDIA Cosmos Technical Paper](https://arxiv.org/abs/2501.03575)
- [Google Genie](https://arxiv.org/abs/2402.15391)
- [Genie 3](https://deepmind.google/models/genie/)
- [OpenAI Sora](https://openai.com/index/video-generation-models-as-world-simulators/)
- [Open-Sora](https://github.com/hpcaitech/Open-Sora)
- [Runway Gen-4.5](https://runwayml.com/research/introducing-runway-gen-4.5)
- [Runway GWM-1](https://runwayml.com/research/introducing-runway-gwm-1)

### Physics Understanding Benchmarks
- [Physics-IQ](https://physics-iq.github.io/)
- [PhyWorld](https://phyworld.github.io/)
- [T2VPhysBench](https://arxiv.org/abs/2505.00337)

### Structured/Graph World Models
- [Graph World Model (ICML 2025)](https://arxiv.org/abs/2507.10539)
- [Semantic World Models](https://arxiv.org/abs/2510.19818)
- [Generate Any Scene](https://arxiv.org/abs/2412.08221)

### Human-as-Sensor / Crowdsourced Data
- [Project Aria](https://www.projectaria.com/)
- [Ego4D](https://ego4d-data.org/)
- [EPIC-KITCHENS](https://epic-kitchens.github.io/)
- [DROID Dataset](https://droid-dataset.github.io/)
- [RoboCrowd](https://arxiv.org/abs/2411.01915)
- [Sensei (YC)](https://www.ycombinator.com/companies/sensei)

### Alternative Approaches
- [V-JEPA 2](https://ai.meta.com/vjepa/)
- [Latent vs Pixels for World Models](https://medium.com/@m.a.meskarian/world-models-why-i-picked-latent-space-over-pixels-2ec1bdd4a036)
- [NVIDIA Cosmos Reason](https://developer.nvidia.com/blog/curating-synthetic-datasets-to-train-physical-ai-models-with-nvidia-cosmos-reason/)
- [Neural Physics Engine](https://www.csail.mit.edu/research/neural-physics-engine)
- [Structured World Models from Human Videos](https://arxiv.org/abs/2308.10901)
