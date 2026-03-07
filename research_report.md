# Deep Research Report: Motion Capture for World Models, AI Film Companies, and Real-Time/Personalized Video

**Date:** 2026-03-07
**Researcher:** Claude Opus 4.6 Deep Research Investigator

---

## EXECUTIVE SUMMARY

This report covers three interconnected research domains. **Topic 1** reveals that motion capture data is actively being used to train world models, primarily in robotics and autonomous driving, with consumer sensor data (phones, watches) emerging as a viable but lower-fidelity alternative to professional mocap suits. **Topic 2** maps a rapidly maturing AI filmmaking ecosystem where companies like Runway, Wonder Dynamics/Autodesk, and Luma AI are building structured 3D representations from video that directly feed into world model architectures. **Topic 3** documents a genuine shift from batch to real-time video generation, with Decart's Lucy 2 and PixVerse R1 achieving sub-100ms latency at 1080p, while personalized video (HeyGen, Synthesia, Tavus) has become a proven enterprise tool rather than hype. Interactive/branching AI-generated video remains early-stage, with full real-time feasibility projected for the early 2030s.

The most significant finding across all three topics is convergence: mocap data feeds into SMPL body models that train world models; AI film companies create structured 3D scenes that become world model training data; and real-time video generation IS world model inference running at interactive speeds. These are not three separate fields -- they are three views of the same underlying technological trajectory.

---

## TOPIC 1: MOTION CAPTURE DATA AS WORLD MODEL TRAINING DATA

### 1.1 How Motion Capture Data Is Currently Used in AI/ML

Motion capture data serves several primary functions in modern AI/ML:

**Human Pose Estimation and Motion Prediction**
- Training models to predict and reconstruct human motion from partial observations
- Enabling physics-based character animation in games and simulation
- Providing ground-truth data for benchmarking pose estimation algorithms

**Robotics and Embodied AI**
- Teaching humanoid robots natural movement patterns through imitation learning
- Creating simulation environments where virtual humanoids perform learned behaviors
- Xsens launched its Next-Generation Link mocap system alongside "Xsens Humanoid" software to convert human motion into robot-ready kinematics for dataset creation, live teleoperation, and simulation workflows ([source](https://www.roboticstomorrow.com/news/2025/11/12/xsens-launches-next-generation-humanoid-robotics-motion-capture-system/25794))

**Procedural Training Data Generation**
- Meshcapade uses SMPL body models combined with mocap data to generate unlimited synthetic video of people in motion, with diverse body shapes, clothing, scenes, and perfect 3D ground truth ([source](https://medium.com/meshcapade/building-human-foundation-models-with-smpl-a5251bb294fd))
- Protege AI ($65M total funding, backed by a16z) provides curated mocap datasets specifically for AI model training across robotics, embodied agents, and physically grounded simulation ([source](https://www.withprotege.ai/motion-capture))

**AI-Driven Motion Capture Recovery**
- GANs, transformers, and graph neural networks model complex spatial-temporal dependencies for accurate motion reconstruction from degraded or incomplete data ([source](https://www.mdpi.com/1424-8220/25/24/7525))

### 1.2 Is Mocap Data Being Used to Train World Models? YES.

The connection between mocap data and world models operates through several pathways:

**Direct Integration: NVIDIA Cosmos**
- NVIDIA Cosmos is trained on 9,000 trillion tokens from 20 million hours of real-world data including robotics and motion data ([source](https://www.nvidia.com/en-us/ai/cosmos/))
- New Cosmos Predict models enable multi-frame generation, predicting intermediate actions or motion trajectories
- 1X is using Cosmos Predict and Cosmos Transfer to train its humanoid robot NEO Gamma ([source](https://nvidianews.nvidia.com/news/nvidia-announces-major-release-of-cosmos-world-foundation-models-and-physical-ai-data-tools))

**Indirect via SMPL Body Models**
- Motion capture data is unified through SMPL parameterization (AMASS dataset), creating structured body representations
- These SMPL representations become the "language of human behavior" with just 100 parameters, enabling world models to understand human physics ([source](https://meshcapade.com/smpl/))
- Video diffusion models leverage motion priors learned from this data to synthesize diverse, high-fidelity human motion sequences

**Physics-Based World Models**
- MoCapAct (Microsoft) trains humanoid control policies on 3.5 hours of CMU MoCap data in physics simulation, demonstrating that mocap data + RL = physical world understanding ([source](https://github.com/microsoft/MoCapAct))
- Disney Research's VMP (Versatile Motion Priors) uses VAE on mocap windows to extract latent kinematic motion space, then trains control policies in physical simulation
- GWM (Gaussian World Models for Robotic Manipulation, ICCV 2025) uses 3D Gaussian representations to predict future scenes conditioned on robot actions ([source](https://gaussian-world-model.github.io/))

**Meta V-JEPA 2: The Paradigm Example**
- V-JEPA 2 is trained on 1M+ hours of internet video, then fine-tuned on just 62 hours of robot data
- Achieves zero-shot robot control in new environments, demonstrating that video (which captures natural human motion) IS world model training data ([source](https://ai.meta.com/vjepa/))
- 65-80% success rate on pick-and-place tasks in previously unseen environments

### 1.3 Key Datasets

| Dataset | Scale | Format | Key Features |
|---------|-------|--------|-------------|
| **CMU MoCap** | ~2,500 trials | BVH/C3D | Classic optical marker-based dataset, one of the sources unified in AMASS |
| **AMASS** | 40 hours, 344 subjects, 11,265 motions | SMPL | Unifies 15 different mocap datasets into common SMPL framework ([source](https://amass.is.tue.mpg.de/)) |
| **Human3.6M** | 3.6M poses, 11 subjects, 15 activities | 2D+3D joints | 4 viewpoints, high-resolution 3D joint data for 17 key joints ([source](https://vision.imar.ro/human3.6m/pami-h36m.pdf)) |
| **Motion-X** | 15.6M frames, 81.1K sequences | SMPL-X whole-body | Includes face, hands, body; text annotations; NeurIPS 2023 ([source](https://motion-x-dataset.github.io/)) |
| **Motion-X++** | 19.5M frames, 120.5K sequences | SMPL-X + audio | Extends Motion-X with audio, RGB video, more scenes ([source](https://arxiv.org/html/2501.05098)) |
| **MoCapAct** | 3.5 hours | dm_control | Physics-based humanoid control with expert RL policies; Microsoft ([source](https://github.com/microsoft/MoCapAct)) |
| **Ego4D** | 3,025 hours | Egocentric video | 855 wearers, 74 locations, 9 countries; Meta ([source](https://ego4d-data.org/)) |
| **Ego-Exo4D** | Largest ego+exo dataset | Multi-sensor (IMU, audio, grayscale) | Simultaneous first/third-person capture; 15 university partners ([source](https://ego-exo4d-data.org/)) |
| **ARKitScenes** | 5,047 captures, 1,661 scenes | RGB-D (LiDAR) | Largest indoor 3D dataset from consumer LiDAR; Apple ([source](https://github.com/apple/ARKitScenes)) |
| **ARKit LabelMaker** | Full ARKitScenes + dense semantics | RGB-D + semantics | CVPR 2025; 48,000 GPU hours to process; automatic labels at scale ([source](https://arxiv.org/html/2410.13924v1)) |
| **ScanNet++** | 1,000+ scenes | RGB-D + laser scan | Sub-millimeter laser + iPhone RGB-D + DSLR; 1,000 semantic categories ([source](https://scannetpp.mlsg.cit.tum.de/scannetpp/)) |

### 1.4 Could Consumer Sensor Data (Phones/Watches/Wearables) Be Useful for World Model Training?

**The short answer is: YES, but with significant caveats.**

**What exists today:**

*IMUPoser (CHI 2023)*
- Full-body pose estimation using IMUs in phones, watches, and earbuds
- Works with any available subset of consumer device IMUs, potentially just a single device
- Major limitation: "low-fi" pose output is ill-suited for high-fidelity applications ([source](https://dl.acm.org/doi/fullHtml/10.1145/3544548.3581392))

*MobilePoser (April 2025)*
- Real-time full-body pose + global translation from consumer device IMUs
- Multi-stage deep neural network + physics-based motion optimizer ([source](https://arxiv.org/html/2504.12492v1))

*BaroPoser (August 2025)*
- Adds barometer data to IMUs for better height estimation
- Outperforms IMU-only methods with same hardware ([source](https://arxiv.org/html/2508.03313v1))

*IMUCoCo (August 2025)*
- Enables flexible on-body IMU placement for pose estimation
- Users can wear devices as they prefer, not in fixed positions ([source](https://arxiv.org/html/2508.01894v1))

*Group Inertial Poser (October 2025)*
- Multi-person pose estimation using sparse wearable sensors + ultra-wideband ranging
- Uses structured state-space models for fusion ([source](https://arxiv.org/html/2510.21654))

**Consumer sensor data value proposition for world models:**

| Advantage | Limitation |
|-----------|-----------|
| Massive scale (billions of devices) | Lower accuracy than professional mocap |
| Naturalistic in-the-wild motion | Sparse instrumentation (1-3 body points) |
| Continuous long-duration capture | Noisy data from commodity IMUs |
| Diverse demographics and activities | Privacy and consent challenges |
| Already being collected passively | No ground-truth 3D positions |

**Assessment:** Consumer sensor data is COMPLEMENTARY to professional mocap. Its value is in scale and naturalism. The trajectory of research (IMUPoser -> MobilePoser -> BaroPoser -> IMUCoCo) shows rapidly improving quality from sparse consumer sensors. For world models that need to understand how humans move in everyday contexts (not lab settings), this data could be transformative -- but it needs the structured representations (SMPL) that professional mocap datasets provide as a bridge.

### 1.5 Apple Watch, Meta Ray-Bans, Phone IMU Sensors

**Apple Watch**
- Contains accelerometer, gyroscope, optical heart sensor
- Apple's Neural Engine processes sensor data with ML algorithms for gesture recognition (double tap)
- Apple's patented EMG sensor work could enable finer-grained motion sensing ([source](https://www.patentlyapple.com/2025/01/a-new-apple-patent-reveals-that-theyre-working-on-next-gen-emg-sensors-to-assist-apple-watch-gesture-technology.html))
- IMU data sampled at 20-100Hz via CoreMotion
- **No direct evidence of Apple Watch data being used for world model training** -- but the data pipeline exists

**Meta Ray-Bans**
- 12MP camera, 1920x1440 video, 5-microphone array
- AI features enabled by default; footage sent to offshore contractors for data labeling ([source](https://futurism.com/artificial-intelligence/meta-disturbing-smart-glasses-videos))
- Meta's Aria glasses produced the Ego-Exo4D dataset with IMU, audio, and grayscale cameras
- **Meta IS actively using egocentric sensor data for world model training** -- V-JEPA 2 and the Ego4D/Ego-Exo4D datasets are direct evidence
- Meta's "Project Aria" glasses are research devices specifically designed to collect training data ([source](https://ai.meta.com/blog/ego-exo4d-video-learning-perception/))

**Phone IMU Sensors**
- Suite-IN aggregates motion data from Apple device suite for inertial navigation ([source](https://arxiv.org/html/2411.07828))
- MobilePoser achieves real-time full-body pose from phone IMUs alone
- **No direct world model training usage found**, but the research pipeline is clearly headed there

### 1.6 Apple ARKit/LiDAR Data Usage

**ARKitScenes** is a significant contribution: the largest indoor 3D dataset from consumer LiDAR (5,047 captures, 1,661 scenes). It is being used to train 3D understanding models, and the CVPR 2025 "ARKit LabelMaker" paper extended it with dense semantic annotations, processing the entire dataset in 48,000 GPU hours ([source](https://machinelearning.apple.com/research/arkitscenes)).

Apple's RoomPlan API uses LiDAR for real-time 3D floor plan creation, demonstrating practical scene understanding from consumer hardware ([source](https://machinelearning.apple.com/research/roomplan)).

**Key insight:** The LiDAR on iPhones/iPads has opened high-quality RGB-D data to millions of people, and this data IS being used to train 3D scene understanding models. While "world model" was not explicitly used by Apple, the research applications (3D object detection, depth upsampling, scene reconstruction) are core components of what world models need.

---

## TOPIC 2: AI FILM COMPANIES

### 2.1 Comprehensive Landscape

#### Runway (Beyond Just Video Gen)

Runway is positioning itself as a world model company, not just a video generation tool.

**Video Generation Evolution:**
- Gen-3 Alpha (2024): Foundation model for video generation
- Gen-4 (March 2025): Better temporal consistency, natural motion
- Gen-4.5 (early 2026): Latest model; Hollywood-grade quality ([source](https://runwayml.com/research/introducing-gen-3-alpha))

**Beyond Video Gen -- The World Model Play:**
- **GWM-1 (General World Model)**: Autoregressive model built on Gen-4.5 that generates frame-by-frame in real time with interactive control via camera pose, robot commands, and audio ([source](https://runwayml.com/research/introducing-runway-gwm-1))
- Maintains spatial/geometric consistency as objects move in/out of view
- Runway explicitly states: "the next major advancement in AI will come from systems that understand the visual world and its dynamics" ([source](https://runwayml.com/research/introducing-general-world-models))

**Additional Tools:**
- **Act-Two**: Webcam-based performance capture that transfers facial expressions, hand gestures, and body movement to any AI character -- democratizing motion capture ([source](https://runwayml.com/research/introducing-act-one))
- **Motion Brush**: Precise control over motion in generated video
- **Video Inpainting/Removal**: Object removal and replacement
- **Lip Sync**: Character animation synchronized with audio
- **Workflows**: Automated pipelines chaining generation, editing, style transfer, and export

#### Pika

**Core Product:**
- Text-to-video and image-to-video generation (720p-1080p, 5-10 seconds)
- Latest model: Pika 2.5 with sharper visuals and smoother camera motion ([source](https://pika.art/login))

**Distinctive Features:**
- **Pikaframes**: Keyframe transition generation between start/end images (1-10 second duration)
- **Pikaformance**: Voice-to-performance model turning audio into lifelike face animation
- **Pikaswaps/Pikadditions**: Remix real footage by swapping characters, adding objects, changing lighting
- **Pika AI Selves**: Personalized AI avatar creation ([source](https://pika-art.net/))

**Assessment:** Pika is focused on accessible creative tools rather than world model research. Their keyframe and performance capture features are strong but narrower than Runway's ambitions.

#### Wonder Dynamics (now Autodesk Flow Studio)

**Acquisition and Evolution:**
- Acquired by Autodesk in 2024; rebranded as Autodesk Flow Studio in March 2025 ([source](https://www.cgchannel.com/2025/03/wonder-studio-becomes-autodesk-flow-studio/))
- Launched "freemium" access in August 2025

**Core Technology: Video to 3D Scene**
This is Wonder Dynamics' most significant contribution. The technology:
1. Takes multi-cut video (wide, medium, close-up shots) as input
2. Uses AI to reconstruct the scene in 3D space
3. Matches spatial continuity of characters and camera positions across cuts
4. Reconstructs character movement even when actors are partially occluded
5. Outputs fully editable 3D scenes with animation, camera tracking, lighting data
6. Exports to Blender, Maya, Unreal Engine, and USD format ([source](https://adsknews.autodesk.com/en/news/autodesk-launches-wonder-animation-video-to-3d-scene-technology/))

**What It Actually Does (Technical):**
- **Markerless AI Motion Capture**: Extracts 3D motion data from regular single-camera video
- **Camera Tracking**: Reconstructs camera trajectory in 3D space
- **Scene Reconstruction**: Creates virtual 3D representation of the filmed environment
- **Clean Plate Generation**: Removes actors to create background-only plates
- **Advanced Motion Prediction**: Handles occlusion and partial visibility

**2026 Update: Wonder 3D**
- Text-to-3D generation of characters, creatures, and props
- Integrates generative asset creation into the pipeline ([source](https://digitalproduction.com/2026/03/05/autodesk-adds-generative-3d-to-flow-studio/))

**World Model Relevance:** Wonder Dynamics/Flow Studio creates exactly the kind of structured 3D representations that world models need -- decomposed scenes with tracked cameras, character animations, and spatial relationships. This is inverse rendering in production form.

#### Luma AI

**Dual Product Lines:**

*3D Capture (NeRF/Gaussian Splatting):*
- iOS app for capturing Gaussian splats and NeRFs from phone camera
- Interactive Scenes: Browser/phone-friendly 3D renders (8-20MB streaming files)
- Unreal Engine plugin for importing captures
- WebGL library for three.js integration ([source](https://lumalabs.ai/interactive-scenes))

*Video Generation (Dream Machine / Ray):*
- Ray2 (March 2025): 10x compute of Ray1, up to 60-second videos, 1080p with 4K upscale
- Keyframes feature: Frame-by-frame control over generation
- Ray3 Modify (2026): Modify existing footage while preserving performance ([source](https://lumalabs.ai/ray2))

**World Model Relevance:** Luma AI sits at the intersection of 3D scene understanding and video generation. Their Gaussian splatting captures are structured 3D representations that can feed directly into world model training pipelines.

#### Stability AI Video Efforts

**Products:**
- **Stable Video Diffusion (SVD)**: Open-source video generation, 14 or 25 frames, 3-30 FPS
- **Stable Video 3D (SV3D)**: Novel view synthesis and 3D mesh generation from single image ($20/month)
- **Stable Video 4D (SV4D 2.0)**: Video-to-4D diffusion model for novel-view video synthesis and 4D asset generation ([source](https://stability.ai/stable-video))
- 231,198 monthly downloads on Hugging Face as of 2025

**Assessment:** Stability AI's video efforts are more research-oriented and open-source-focused. Their SV3D and SV4D models are directly relevant to world model training as they create structured 3D/4D representations from video.

### 2.2 Companies Decomposing Video into Editable 3D Scenes

| Company/Tool | Approach | Output |
|-------------|----------|--------|
| **Wonder Dynamics/Flow Studio** | AI video-to-3D scene | Editable 3D scene with animation, cameras, lighting |
| **NVIDIA DiffusionRenderer** | Inverse rendering via diffusion | G-buffers (normals, albedo, depth) from video for relighting and editing (CVPR 2025, open-source) ([source](https://stc-mditr.org/nvidias-diffusionrenderer/)) |
| **Google DeepMind D4RT** | 4D reconstruction | Dynamic 3D scene tracking, 300x more efficient than prior methods ([source](https://deepmind.google/blog/d4rt-teaching-ai-to-see-the-world-in-four-dimensions/)) |
| **IDSplat** | Instance-decomposed 3D Gaussian splatting | Separate Gaussian representations for each dynamic object in driving scenes |
| **DrivingGaussian** | Composite Gaussian splatting | Driving scene decomposition with static backgrounds + dynamic objects |
| **Editable-4DGS** | 4D Gaussian splatting with UV decomposition | Separates appearance from motion; enables video editing of 4D content |

### 2.3 NeRF/3D Gaussian Splatting Companies

| Company | Technology | Key Product |
|---------|-----------|-------------|
| **Luma AI** | NeRF + Gaussian splatting | iOS capture app, Interactive Scenes, UE plugin ([source](https://lumalabs.ai/interactive-scenes)) |
| **Polycam** | Gaussian splatting + photogrammetry + LiDAR | Cross-platform scanning app, PLY export, Blender/UE/Unity plugins ([source](https://poly.cam/tools/gaussian-splatting)) |
| **Niantic/Scaniverse** | On-device Gaussian splatting | Mobile scanning, SPZ compressed format (open-sourced), Large Geospatial Model ([source](https://nianticlabs.com/news/splats-change-everything?hl=en)) |
| **Nerfstudio** | NeRF + 3DGS research framework | Open-source research toolkit with CUDA-accelerated rasterizer |
| **Rodin/Hyper3D** | AI 3D generation | 10B parameter Gen-2 model with "BANG" architecture (ByteDance/Deemos) |
| **Meshy** | AI text/image to 3D | Rapid prototyping, generous free tier |
| **Kaedim** | AI + human-in-the-loop | High-fidelity 3D asset production for studios |

### 2.4 Are These Creating Structured Representations for World Models?

**YES.** The evidence is strong and growing:

1. **GWM (ICCV 2025)**: Gaussian World Models explicitly use 3D Gaussian representations to predict future states for robotic manipulation ([source](https://gaussian-world-model.github.io/))

2. **DriveDreamer4D (CVPR 2025)**: First framework leveraging world model priors for 4D scene reconstruction in autonomous driving ([source](https://cvpr.thecvf.com/virtual/2025/poster/34218))

3. **Physically Embodied Gaussians**: 3D Gaussians that anticipate physically plausible future states and generate "visual forces" to correct particle positions ([source](https://embodied-gaussians.github.io/))

4. **AutoSplat, SplatAD, DrivingGaussian**: Constrained Gaussian splatting specifically for autonomous driving scene reconstruction and training

5. **WorldForge**: Unlocking emergent 3D/4D generation in video diffusion models

6. **3D and 4D World Modeling Survey**: A comprehensive 2025 survey establishes taxonomy spanning video-based (VideoGen), occupancy-based (OccGen), and LiDAR-based (LiDARGen) approaches to world modeling ([source](https://arxiv.org/html/2509.07996v2))

The trend is clear: NeRF and Gaussian splatting representations are becoming the preferred structured format for world models because they bridge the gap between raw video and physics-based understanding.

### 2.5 Twelve Labs (Video Understanding API)

**What They Do:**
- Video understanding platform with search, analysis, and embedding capabilities
- Natural language search through video content ("show me the first touchdown")
- Auto-generation of titles, summaries, chapters, highlights ([source](https://www.twelvelabs.io/))

**Latest Model: Marengo 3.0 (December 2025)**
- 4-hour video support (2x increase over 2.7)
- 36-language multilingual support
- 50% reduction in storage costs, 2x faster indexing
- Available on Amazon Bedrock and directly through TwelveLabs ([source](https://www.hpcwire.com/aiwire/2025/12/01/twelvelabs-launches-marengo-3-0-video-understanding-model-on-twelvelabs-and-amazon-bedrock/))

**World Model Relevance:** Twelve Labs creates semantic understanding of video content that is complementary to spatial/3D understanding. Their embeddings could serve as conditioning signals for world models, enabling them to understand "what is happening" in addition to "where things are."

---

## TOPIC 3: "BATCH TO REAL-TIME" AND "ONE VIDEO TO PERSONALIZED VIDEO"

### 3.1 Real-Time Video Generation: What Exists

The field has moved from concept to production in 2025-2026:

#### Decart AI -- Lucy 2 and MirageLSD

**MirageLSD:**
- First system to achieve infinite, real-time video generation with zero latency
- Live-Stream Diffusion (LSD) architecture: frame-by-frame generation preserving temporal coherence
- Sub-40ms response time, smooth 24 FPS output
- Custom CUDA mega kernels + shortcut distillation + model pruning = 16x improvement over prior models ([source](https://decart.ai/publications/mirage))

**Lucy 2.0:**
- Real-time world transformation model at 30fps 1080p with near-zero latency
- Pure diffusion model (no depth maps, meshes, or 3D pipelines)
- Smart History Augmentation: model penalized during training for quality drift
- Custom WebRTC pipeline for bidirectional video streaming
- Use cases: character swaps, motion control, product placement, clothing changes, environment transformation -- all during live streaming ([source](https://decart.ai/publications/lucy-2-introducing-sota-video-generation-in-realtime))

#### PixVerse R1

- Native multimodal foundation model: text, image, video, audio unified as continuous token stream
- Real-time generation up to 1080p with integrated audio synthesis
- Streaming architecture: frames generated in order, video grows indefinitely
- Keyboard/mouse interactive control with physics simulation
- Continuous generation up to 300 seconds ([source](https://pixverse.ai/en/blog/pixverse-r1-next-generation-real-time-world-model))

#### NVIDIA LongLive (ICLR 2026)

- Frame-level autoregressive framework
- 20.7 FPS on single H100; up to 240-second videos
- KV-recache mechanism for smooth prompt switching
- Train-long-test-long alignment via streaming long tuning
- 1.3B parameters, fine-tuned in just 32 GPU-days ([source](https://arxiv.org/abs/2509.22622))

#### Google DeepMind -- Genie 2 and Genie 3

- Genie 2: Interactive 3D world generation from single image, consistent for ~1 minute, 720p
- Genie 3: General-purpose world model generating navigable environments at 24 FPS, 720p, consistent for several minutes ([source](https://deepmind.google/blog/genie-2-a-large-scale-foundation-world-model/))

#### Oasis / GameNGen

- Oasis: First playable AI-generated game (Minecraft), 360p at 20 FPS, 100x faster than text-to-video models ([source](https://oasis-model.github.io/))
- GameNGen (Google): Neural game engine simulating Doom at 20+ FPS

#### Summary of Real-Time Systems

| System | Latency | Resolution | Duration | FPS | Status |
|--------|---------|-----------|----------|-----|--------|
| **Decart MirageLSD** | <40ms | Varies | Infinite | 24 | Available (Crusoe Cloud) |
| **Decart Lucy 2** | <100ms | 1080p | Infinite | 30 | API Available |
| **PixVerse R1** | Real-time | Up to 1080p | 300s | Real-time | Available |
| **NVIDIA LongLive** | Real-time | Standard | 240s | 20.7 | Research/Open-source |
| **Google Genie 3** | Real-time | 720p | Minutes | 24 | Limited access |
| **Oasis** | Real-time | 360p | Infinite | 20 | Demo available |

### 3.2 Personalized Video: Companies and Assessment

#### Category 1: Avatar-Based Personalization (Proven Enterprise Market)

**HeyGen** ($95M ARR)
- Avatar IV: Micro-expressions and emotional intelligence
- LiveAvatar: Real-time interactive conversations
- 175+ languages, voice cloning
- Unlimited video generation on paid plans ([source](https://www.heygen.com/))

**Synthesia** (Enterprise leader)
- 230+ AI avatars, 140+ languages
- SOC 2 Type II compliance
- Custom avatar creation from short recording
- Used by Fortune 500 for training, onboarding ([source](https://www.synthesia.io/))

**D-ID** (Pivoted to conversational AI)
- AI Agents 2.0: Real-time face-to-face conversations with digital assistants
- Photo-to-talking-avatar technology
- CES 2026 Innovation Award ([source](https://aloa.co/ai/comparisons/ai-video-comparison/heygen-vs-d-id))

**Tavus** (1-to-many personalization)
- Record once, generate millions of personalized variants
- Variables for names, companies, products, dates
- 16x higher click-to-open rates vs generic video
- Sales prospecting, onboarding, follow-ups ([source](https://www.tavus.io/personalized-video-at-scale))

**Assessment: NOT hype.** The avatar-based personalized video market is $0.8B in 2025, projected to reach $5.93B by 2032 (33.1% CAGR). HeyGen's $95M ARR is real revenue. These tools are being used daily by sales teams, HR departments, and marketing organizations. The technology is proven for:
- Sales outreach at scale (500% conversion boost claimed by Tavus)
- Employee training and onboarding
- Multilingual content localization
- Customer support and product demos

**Limitation:** Most current "personalization" is template-based (swap name/company variables in an avatar video), not truly generative personalization where the content itself changes based on the viewer.

#### Category 2: Generative Personalization (Emerging)

This is more speculative but gaining traction:
- **Pika AI Selves**: Create a personalized AI version of yourself for video generation
- **Luma AI Ray3 Modify**: Modify existing footage with character reference images
- **Runway Act-Two**: Transfer your performance to any AI character

These tools are moving toward true generative personalization where the CONTENT (not just the avatar) adapts to individual viewers or contexts.

### 3.3 Interactive/Branching Video with AI Generation

**Current State: Very Early**

**Academic Research:**
- An October 2025 preprint "From Kinoautomat to AI Cinema: Interactive Films and the Prospect of Their Real-Time Generation" explicitly addresses Bandersnatch-style AI generation ([source](https://www.preprints.org/manuscript/202510.0158))
- The paper projects that real-time interactive AI video generation on a single GPU becomes realistic in the mid-2030s for mass adoption, with the early 2030s being optimistically feasible

**Closest Current Implementations:**

1. **PixVerse R1** is the closest thing to interactive branching video:
   - Real-time scene manipulation
   - Branching narrative support
   - Users interact via keyboard/mouse
   - System models physics and responds to user decisions
   - Natural language prompt steering during generation ([source](https://pixverse.ai/en/blog/pixverse-r1-next-generation-real-time-world-model))

2. **Decart Lucy 2**: Real-time video transformation with prompt control, but more focused on restyling than narrative branching

3. **Google Genie 2/3**: Interactive 3D world generation with user control, but limited to game-like environments

4. **Runway GWM-1**: Real-time frame generation with interactive control (camera pose, actions), but not narrative branching specifically

**Gap Analysis:**
- No system today can generate Bandersnatch-quality narrative video in real time
- The closest systems (PixVerse R1, Genie 3) operate at lower fidelity than pre-rendered content
- Branching narrative requires coherent long-term story understanding, which current models lack
- Audio + dialogue generation synchronized with branching remains unsolved at production quality

**The 2026 trajectory** (per industry analysis): Sub-second generation emerging, interactive video editing during playback, conversational video creation ("make it more dramatic"), but full narrative branching with production quality remains years away.

---

## CROSS-CUTTING ANALYSIS: THE CONVERGENCE THESIS

The three topics researched are deeply interconnected through a single underlying trend:

```
Motion Capture Data ---> SMPL/Structured Body Models ---> World Model Training Data
       |                                                          |
       v                                                          v
AI Film Tools (Wonder Dynamics, Runway) ---> Structured 3D Scenes ---> World Models
       |                                                          |
       v                                                          v
Real-Time Video Generation <---- World Model Inference at Interactive Speed
```

**Key connections:**
1. **Mocap -> World Models**: Professional and consumer mocap data trains physics-aware body models (SMPL), which become training data for world models that understand human motion
2. **AI Film Tools -> World Models**: Wonder Dynamics, Luma AI, and Polycam create structured 3D representations (Gaussian splats, NeRFs, decomposed scenes) that are exactly what world models need as training data
3. **World Models -> Real-Time Video**: Real-time video generation (Runway GWM-1, PixVerse R1, Decart Lucy 2) IS world model inference -- these systems generate video by simulating plausible physical futures
4. **The cycle**: Better world models enable better AI film tools, which create better training data for world models

---

## CONFIDENCE ASSESSMENT

| Finding | Confidence |
|---------|-----------|
| Mocap data is used for world model training | **High** -- Multiple direct examples (Cosmos, V-JEPA 2, MoCapAct) |
| Consumer sensor data can supplement professional mocap | **High** -- Multiple 2025 papers demonstrate improving quality |
| Consumer sensor data is actively used for world model training | **Medium** -- Meta's Ego4D is closest; most consumer sensor research is still in pose estimation, not world models |
| Apple Watch/phone IMU data specifically used for world models | **Low** -- No direct evidence found; pipeline exists but connection not yet made |
| ARKit/LiDAR data used for 3D scene understanding | **High** -- ARKitScenes, ARKit LabelMaker at CVPR 2025 |
| AI film companies creating world model training data | **High** -- GWM paper, DriveDreamer4D, Runway GWM-1 all confirm |
| Real-time video generation is production-ready | **Medium-High** -- Lucy 2 and PixVerse R1 are available; quality still below pre-rendered |
| Personalized video is a real market | **High** -- $95M ARR (HeyGen), $0.8B market size, Fortune 500 adoption |
| Interactive branching AI video exists | **Low** -- PixVerse R1 is closest, but nothing at Bandersnatch narrative quality |

---

## RESEARCH GAPS

1. **No public information** on whether Apple is internally using Apple Watch sensor data for world model research
2. **Limited detail** on how exactly NVIDIA Cosmos incorporates motion capture data in its 9,000 trillion token training set
3. **No clear data** on whether Twelve Labs' video understanding is being used to generate world model training data (plausible but unconfirmed)
4. **Unclear** whether any company is combining consumer wearable data with video for joint world model training (the obvious next step)
5. **No public benchmarks** comparing consumer-sensor-derived motion data vs professional mocap for world model training quality

---

## RECOMMENDED FOLLOW-UPS

1. **Deep dive on Runway GWM-1**: Their world model architecture and training data pipeline would reveal the clearest connection between all three topics
2. **Interview Protege AI (Bobby Samuels)**: As the mocap-for-AI-training company with $65M funding, they would have direct insight on the mocap-to-world-model pipeline
3. **Investigate NVIDIA Cosmos training data pipeline**: Understanding exactly what motion/sensor data goes in would clarify the consumer sensor opportunity
4. **Track PixVerse R1 interactive cinema demos**: This is the closest system to AI-generated Bandersnatch and the most likely to achieve it first
5. **Monitor Meta's Project Aria**: Their egocentric data collection effort is the largest consumer-sensor-to-world-model pipeline in existence

---

## SOURCES

### Topic 1: Motion Capture and World Models
- [Xsens Humanoid Robotics MoCap System](https://www.roboticstomorrow.com/news/2025/11/12/xsens-launches-next-generation-humanoid-robotics-motion-capture-system/25794)
- [Protege AI Motion Capture Data](https://www.withprotege.ai/motion-capture)
- [AMASS Dataset](https://amass.is.tue.mpg.de/)
- [Human3.6M Dataset](https://vision.imar.ro/human3.6m/pami-h36m.pdf)
- [Motion-X Dataset (NeurIPS 2023)](https://motion-x-dataset.github.io/)
- [MoCapAct (Microsoft)](https://github.com/microsoft/MoCapAct)
- [NVIDIA Cosmos](https://www.nvidia.com/en-us/ai/cosmos/)
- [V-JEPA 2 (Meta)](https://ai.meta.com/vjepa/)
- [IMUPoser (CHI 2023)](https://dl.acm.org/doi/fullHtml/10.1145/3544548.3581392)
- [MobilePoser (2025)](https://arxiv.org/html/2504.12492v1)
- [BaroPoser (2025)](https://arxiv.org/html/2508.03313v1)
- [Ego4D](https://ego4d-data.org/)
- [Ego-Exo4D](https://ego-exo4d-data.org/)
- [ARKitScenes](https://github.com/apple/ARKitScenes)
- [ARKit LabelMaker (CVPR 2025)](https://arxiv.org/html/2410.13924v1)
- [SMPL Body Model](https://meshcapade.com/smpl/)
- [ScanNet++](https://scannetpp.mlsg.cit.tum.de/scannetpp/)
- [GWM: Gaussian World Models (ICCV 2025)](https://gaussian-world-model.github.io/)
- [Protege Raises $30M (a16z)](https://www.alleywatch.com/2026/01/protege-ai-training-data-licensing-real-world-data-bobby-samuels/)

### Topic 2: AI Film Companies
- [Runway Gen-3 Alpha](https://runwayml.com/research/introducing-gen-3-alpha)
- [Runway GWM-1](https://runwayml.com/research/introducing-runway-gwm-1)
- [Runway General World Models](https://runwayml.com/research/introducing-general-world-models)
- [Runway Act-One](https://runwayml.com/research/introducing-act-one)
- [Pika AI](https://pika-art.net/)
- [Wonder Dynamics / Flow Studio](https://wonderdynamics.com/)
- [Wonder Animation Launch](https://adsknews.autodesk.com/en/news/autodesk-launches-wonder-animation-video-to-3d-scene-technology/)
- [Luma AI Interactive Scenes](https://lumalabs.ai/interactive-scenes)
- [Luma AI Ray2](https://lumalabs.ai/ray2)
- [Stability AI Stable Video](https://stability.ai/stable-video)
- [Polycam Gaussian Splatting](https://poly.cam/tools/gaussian-splatting)
- [Niantic Scaniverse / Gaussian Splats](https://nianticlabs.com/news/splats-change-everything?hl=en)
- [Twelve Labs](https://www.twelvelabs.io/)
- [Twelve Labs Marengo 3.0](https://www.hpcwire.com/aiwire/2025/12/01/twelvelabs-launches-marengo-3-0-video-understanding-model-on-twelvelabs-and-amazon-bedrock/)
- [NVIDIA DiffusionRenderer](https://stc-mditr.org/nvidias-diffusionrenderer/)
- [DriveDreamer4D (CVPR 2025)](https://cvpr.thecvf.com/virtual/2025/poster/34218)
- [3D and 4D World Modeling Survey](https://arxiv.org/html/2509.07996v2)
- [Physically Embodied Gaussians](https://embodied-gaussians.github.io/)

### Topic 3: Real-Time and Personalized Video
- [Decart AI / Lucy 2](https://decart.ai/publications/lucy-2-introducing-sota-video-generation-in-realtime)
- [MirageLSD](https://decart.ai/publications/mirage)
- [PixVerse R1](https://pixverse.ai/en/blog/pixverse-r1-next-generation-real-time-world-model)
- [NVIDIA LongLive (ICLR 2026)](https://arxiv.org/abs/2509.22622)
- [Google Genie 2](https://deepmind.google/blog/genie-2-a-large-scale-foundation-world-model/)
- [Google Genie 3](https://deepmind.google/blog/genie-3-a-new-frontier-for-world-models/)
- [Oasis AI](https://oasis-model.github.io/)
- [HeyGen](https://www.heygen.com/)
- [Synthesia](https://www.synthesia.io/)
- [D-ID](https://aloa.co/ai/comparisons/ai-video-comparison/heygen-vs-d-id)
- [Tavus Personalized Video](https://www.tavus.io/personalized-video-at-scale)
- [Interactive Films and Real-Time Generation (preprint)](https://www.preprints.org/manuscript/202510.0158)
- [StreamDiffusion](https://arxiv.org/html/2312.12491v2)
