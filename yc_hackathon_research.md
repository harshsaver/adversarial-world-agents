# YC Hackathon Winners & Projects: Comprehensive Research Report
## 2024 - 2026

---

## EXECUTIVE SUMMARY

Y Combinator has hosted or co-hosted at least 12 distinct hackathons between October 2024 and March 2026, with combined prize pools exceeding $500,000. These events have become a de facto pipeline for YC applications -- multiple winners have received guaranteed YC interviews, and several hackathon projects (Soshi, April, Codapt) have gone on to become funded startups. The dominant themes across all events are AI agents, MCP (Model Context Protocol) infrastructure, voice/multimodal AI, and "vibe coding" (natural language as executable code). Projects that win tend to solve real problems (not toy demos), ship production-ready code in 24 hours, and demonstrate novel use of sponsor technologies.

---

## 1. YC AGENTS HACKATHON (Aug 22-23, 2025)

**Event Details:**
- Location: Y Combinator Office, San Francisco
- Format: Overnight hackathon (6 PM Friday to 9 PM Saturday, 24 hours)
- Prize Pool: $80,000+ total
- Sponsors: OpenAI, Anthropic ($100 API credits), Browser Use ($250 credits), Vercel ($200 credits), Convex (3 months Pro), Vapi ($20 credits)
- Hosted by: Dedalus Labs (YC S25) along with Kernel, Interfere, Nozomio, Browser Use, AgentMail, Autumn
- Keynote Speakers: Jared Friedman (YC Managing Director), James Cowling (Convex CTO, ex-Dropbox), Wayne Sutton (Convex), Dan Goosewin (Vapi)
- Judges: 18 total, including founders from YC S25 companies (Slashy, AgentMail, Nozomio, Interfere, Kernel, Autumn, Browser Use) plus Vercel and YC representatives

### FIVE COMPETITION TRACKS

| Track | Description |
|-------|-------------|
| 1. Tools for Agents | Infra and tools (MCP) that enable agents to act |
| 2. Developer & Code Agents | Agents that write, read, and reason about code |
| 3. Consumer Agents | Lifestyle, shopping, finance, productivity agents |
| 4. Web Agents | Browsing, scraping, automation agents |
| 5. Agents for Enterprise | GTM, legal, hiring, admin, business analytics, marketing, creative |

### CONFIRMED WINNERS

#### Codapt AI -- Grand Prize / Multiple Track Winner
- **Prize:** $65,000+ (1st place overall, 1st place Vercel, 1st place Convex)
- **What it does:** AI builder that generates production-ready web apps with the quality of a real engineer. Users describe what they want in natural language, and Codapt builds a complete full-stack application (React frontend, Node.js backend, Postgres DB) with clean, editable code
- **Founders:** Trevor Keith & Eduardo Ortiz de Lanzagorta Gonzalez
- **Tech stack:** React, Node.js, Postgres, Vercel deployment, Convex backend
- **Why it won:** Demonstrated that AI can produce code at professional engineer quality in real-time. The judges were impressed by the production-readiness of generated apps -- not just demos but shippable software. The tool served both technical and non-technical founders
- **Post-hackathon:** Became a funded startup offering "the world's 1st agentic canvas where you can co-create with AI"
- **Source:** [LinkedIn post by Ruben Dominguez Ibar](https://www.linkedin.com/posts/rubendominguezibar_two-founders-walked-into-ycs-first-24-hour-activity-7368696748254334997-L2P7)

#### Oreo -- 1st Place Convex Prize / Vibe Coding Track
- **What it does:** Gives "vibe coders" a new way to prompt LLMs -- exploring human language as executable code. Users express intent in natural language and the system translates it into working code seamlessly
- **Founders:** Riley Shu & Keith Tsai
- **Tech stack:** Convex backend, LLM integration
- **Why it won:** Pioneered the concept of "vibe coding" -- the idea that natural language can be treated as first-class code. The demo effect was strong; it showed something genuinely new rather than incremental improvements
- **Context:** Riley Shu is a serial hackathon winner (1st at YC, 1st at OpenAI awarded by Andrej Karpathy, $64K at Cognition Hackathon for Overeasy)
- **Source:** [Convex announcement](https://x.com/convex_dev/status/1960094665807741076), [Maven profile](https://maven.com/p/41380d/how-i-won-first-places-in-the-yc-and-open-ai-hackathons)

### KEY OBSERVATIONS (from attendee analysis)
- Winning agents shared three traits: **continuous iteration** (UI improvement > A/B testing > improve again), **tool-using capabilities** (integration with code editing tools), and **multi-agent swarm architecture** (larger models as architects, smaller models as junior developers)
- Frameworks used: LangChain, CrewAI, AutoGen
- Notable tools showcased: freestyle.dev (Benjamin Swerdlow), same.new (Aiden Bai), Morph (Tejas Bhakta, YC S23)
- Source: [Faradawn Yang LinkedIn analysis](https://www.linkedin.com/posts/faradawn_ai-agents-will-replace-these-dev-tasks-and-activity-7360746841652531201-ubNK)

### RESEARCH GAPS
The complete list of winners across all 5 tracks has NOT been publicly published in a single announcement. The detailed per-track winners (especially tracks 1, 3, 4, 5) appear to have been announced primarily through the hackathon Discord channel, which is not publicly indexed. Codapt and Oreo are the only confirmed winners with public documentation.

---

## 2. YC x OpenAI o1 HACKATHON (October 2024)

**Event Details:**
- Format: Hackathon giving YC startups early access to OpenAI's o1 reasoning model
- Judges: Sam Altman (OpenAI CEO) and Garry Tan (YC President)
- Context: Results were showcased at OpenAI DevDay 2024

### ALL THREE WINNERS

#### Winner 1: Proxis AI
- **Founders:** Liam Collins (CEO, ex-Columbia, left Wharton MBA) & Jackson Stokes (CTO, ex-Google Gemini team)
- **Company:** Proxis (YC S24) -- the platform for enterprise AI agent automations, starting with email
- **What they built:** Used o1 for LLM distillation and serving -- taking massive models and distilling them into efficient, production-ready models at 1/10th the cost. Their hackathon demo showed o1-powered model optimization that was 5x faster and 10x cheaper than closed-source alternatives
- **Tech stack:** LLM distillation pipeline, Llama 405b base models, custom serving infrastructure
- **Why it won:** Demonstrated a practical, enterprise-ready application of o1's reasoning -- not just a cool demo but a genuine cost-reduction breakthrough for production AI
- **Source:** [YC company page](https://www.ycombinator.com/companies/proxis), [YC Twitter announcement](https://x.com/ycombinator/status/1844522539214832042)

#### Winner 2: Vera Health AI
- **Founders:** Maxime Allouch & Taieb Bennani (Yale & MIT alumni)
- **Company:** Vera Health (YC S24) -- AI-powered clinical decision support for healthcare providers
- **What they built:** A voice-enabled clinical agent that lets doctors hands-free query 60+ million scientific papers in seconds. Used o1's reasoning to provide evidence-graded answers to any medical question, drawing from papers, guidelines, and drug references
- **Tech stack:** OpenAI o1 for reasoning, voice processing pipeline, medical literature RAG system over 60M+ papers
- **Why it won:** The voice agent was recognized as the fastest method for clinicians to access scientific literature. The combination of o1 reasoning with medical literature retrieval produced remarkably accurate clinical answers. Sam Altman and Garry Tan personally presented the award
- **Post-hackathon:** Won additional OpenAI competition in December 2024. Partnered with ACEP (American College of Emergency Physicians) to deliver AI to emergency physicians
- **Source:** [Vera Health blog](https://www.vera-health.ai/blogposts/vera-health-wins-first-place-at-the-openai-competition), [Rippling founder spotlight](https://www.rippling.com/blog/founder-spotlight-vera-health)

#### Winner 3: Camfer Inc
- **Founders:** Arya Bastani & Keaton Elvins
- **Company:** Camfer -- AI-powered engineering design tool
- **What they built:** Plugged o1 into Camfer's design tool, adding prediction-based simulations and multi-part design orchestration. Demo: prompted the system to "design 5 airfoil profiles optimized for 50 mph with a minimum lift-to-drag ratio of 15 at a 5 deg angle of attack." The system iteratively designed spline profiles from first principles, ran simulation tests, and refined designs to meet specifications
- **Tech stack:** OpenAI o1, computational fluid dynamics simulation, spline-based CAD generation, iterative design optimization loop
- **Why it won:** Before o1, their tool used heuristic-based dimensioning that struggled with complex calculations. O1's reasoning enabled the tool to "dive deep, calculate the pitch diameter, root diameter, construct the involute profile" -- expanding capability from simple parts into sophisticated engineering problems. The live demo of iterative airfoil design was technically stunning
- **Post-hackathon:** Featured at OpenAI DevDay 2024
- **Source:** [Camfer blog](https://camfer.dev/blog/winning-o1-hackathon/)

---

## 3. SUPABASE AI HACKATHON AT YC (November 22-23, 2024)

**Event Details:**
- Location: Y Combinator, San Francisco
- Participants: 150+ from globally diverse backgrounds (Greece, Australia, Turkey, New Zealand, South Africa, top US universities)
- Format: Friday evening kickoff, Saturday demos across 47 projects in 3 tracks
- Judges: Jared Friedman (YC Partner), Eli Brown (YC Visiting Partner), Paul Copplestone & Ant Wilson (Supabase co-founders)
- Credits: Anthropic provided Claude credits to all teams

### ALL FOUR WINNERS

#### Overall Winner: Soshi
- **What it does:** AI-powered social media marketing employee -- a Twitter assistant that browses platforms, generates replies based on your niche, and helps grow your following. First version of "Soshi Engage" featured AI agent research capabilities that browse social platforms like humans
- **Team:** Elijah Muraoka, Michael Long, Soumil Rathi, Veer Doshi
- **Tech stack:** Supabase (database, auth, real-time), Anthropic Claude, AI agent browsing framework
- **Why it won:** Team had already conducted market research and validation BEFORE the hackathon. They used the event to build their planned core feature rather than improvise. This strategic preparation combined with rapid execution (24-hour build) impressed judges. Jared Friedman noted "the winning teams were impressive"
- **Post-hackathon:** Became a venture-backed startup with 1,300+ user sign-ups and first sales within months. "What started as a 36-hour sprint has since become a funded company"
- **Source:** [Supabase blog](https://supabase.com/blog/ai-hackathon-at-y-combinator), [Elijah LinkedIn](https://www.linkedin.com/posts/elijahmuraoka_everyones-been-asking-me-how-we-won-the-activity-7268717109218619392-Fegu)

#### Most Entertaining: Dropout
- **What it does:** Application that helps identify college students interested in dropping out to join as cofounders or hires -- matching aspiring founders with talent
- **Team:** David Head, Kevin Fu, Jake Schwartz
- **Why it won:** The concept was both humorous (playing on the YC dropout trope) and genuinely useful as a talent matching tool

#### Most Technically Impressive: Explainstein
- **What it does:** Interactive tutoring platform where users upload homework and conduct video calls with an AI tutor that can see their work and explain concepts in real-time
- **Team:** Finn Metz, Sricharan Guddanti, Sveinung Myhre
- **Why it won:** Combined multiple technical challenges (document processing, real-time video, conversational AI tutoring) into a seamless product

#### Most Novel Use of Supabase: Suparova
- **What it does:** A Supabase-powered physical rover robot that can speak, recognize faces, and dance -- demonstrating IoT + AI + database integration
- **Team:** Kwindla Kramer, Simon Sturmer, Bassim Eledath
- **Why it won:** Pushed the boundaries of what Supabase was designed for, using it as the real-time backbone for a physical robot

---

## 4. AI CODING AGENTS HACKATHON AT YC (August 9, 2025)

**Event Details:**
- Location: Y Combinator Office, San Francisco
- Time: 9 AM - 7:30 PM (single day)
- Participants: ~350-400 (diverse: 16-year-old high schoolers to retired senior developers)
- Hosts: Morph LLM (YC S23), Freestyle, Same.new, Anthropic
- Judge: Diana Hu (YC Partner)
- Prize: 1st Place includes guaranteed Y Combinator interview
- Rule: Must incorporate technology from Morph, Freestyle, or Same.new

### FOUR COMPETITION TRACKS

| Track | Description |
|-------|-------------|
| Web/Mobile | Agents that design, deploy, and manage full-stack websites |
| Game Genesis | AI that produces games from concept through playable demo |
| Autonomous Reactive Agents | Software responding to non-human signals (sensors, APIs, time) |
| Just-in-Time Software | Applications that adapt based on user activity patterns |

### WINNERS
Specific track winners have NOT been publicly announced in indexed sources. Judging was conducted through Google Forms submission followed by real-time Q&A in designated judging rooms, evaluated on problem definition clarity, solution approach creativity, technology stack appropriateness, and overall project completeness.

---

## 5. GEMINI x PIPECAT HACKATHON AT YC (October 11-19, 2025)

**Event Details:**
- Location: In-person at YC Office + Virtual global track
- Hosts: Daily and Google DeepMind
- Focus: Voice, video, and multimodal agents
- Technologies: Gemini 2.5 models + Pipecat real-time orchestration stack

### VIRTUAL TRACK WINNERS

#### 1st Place: Boba Bot (Best Gemini Live API + Pipecat Project)
- **Prize:** $50,000 Gemini credits + $50,000 Pipecat Cloud credits
- **Team:** Joey Wang (Focus Lab founder), Hsuanlin Her (Guardant scientist), You-Yi Jau (AWS Neuron SDE), Charlie Lee (Google SDE)
- **Tech stack:** TypeScript, Gemini Live API, Pipecat
- **Why it won:** Judges noted "the interface seemed snappy and responsive" and liked the character design

#### 2nd: Light to the Noodles (Pipecat Cloud Credits Prize)
- **Prize:** $100,000 Pipecat Cloud Credits
- **Lead:** Maxim Makatchev (CMU PhD, susuROBO founder)
- **Expertise:** C++, ROS, dialogue systems, gstreamer, production voice platforms

#### 3rd: Happyverse VC Pitch Playground (Google Gemini Credits Prize)
- **Prize:** $100,000 Gemini Credits
- **Team:** Happyverse founders/executives (CEO: Stanford MBA/MS, ex-Google Cloud TPU PM)
- **Why it won:** "Cool integration of document upload" for pitch practice

#### Preliminary Finalists
- **Lanturn:** ESP32-CAM voice+vision assistant (hardware + AI)
- **BridgeSpeak:** AI language learning platform

---

## 6. CHATGPT / MCP APPS HACKATHON BY MANUFACT AT YC (February 21, 2026)

**Event Details:**
- Location: Y Combinator Office, San Francisco
- Sponsors: OpenAI, Cloudflare, Manufact (YC), Puzzle
- Format: Full-day hackathon building MCP Apps (servers with UIs for ChatGPT, Claude, VS Code)
- Submissions: 80 projects

### CONFIRMED WINNER

#### Grand Prize: Vital Link
- **Prize:** $120,000 total in prizes + guaranteed YC interview with General Partner
- **What it does:** Integrates health data from different personal devices (wearables, medical devices) onto ChatGPT securely -- creating a unified health data MCP layer
- **Team:** Ayaan Gazali (18 years old -- youngest to place 1st overall at a YC hackathon), Hrishikesh Athreya, Arnav D., Aditi Apoorva Jagalur Raghuvara (Santa Clara University)
- **Tech stack:** OpenAI APIs, Manufact MCP SDK, Cloudflare
- **Why it won:** Solved a real problem (fragmented health data across devices), demonstrated secure data integration with ChatGPT, and the team brought combined experience of 55 hackathon wins
- **Notable quote from winner:** "I've lost 9 YC hackathons before this and only won 2nd (track prize). This one felt different."
- **Source:** [LinkedIn post](https://www.linkedin.com/posts/ayaangazali_we-just-won-120000-at-the-y-combinator-activity-7431861605900111872-c0rS)

### OTHER STANDOUT PROJECTS (per Guillermo Rauch / Vercel CEO)
- **ChimeraX MCP:** MCP server to make cancer researchers more efficient at using ChimeraX for molecular visualization
- **Observee:** Observability platform for MCP calls (became YC S25 company)
- **Source:** [Guillermo Rauch tweet](https://x.com/rauchg/status/1923947958812414086)

---

## 7. ADDITIONAL YC HACKATHONS (2024-2026)

### Full Stack Hackathon (January 24-25, 2026)
- Hosts: Sim + Lovable at YC
- Participants: 250 hackers
- Focus: Full-stack agent applications
- Prize: Guaranteed YC interview + sponsored by Supabase, Stripe, Brex
- **Winners: Not publicly announced in indexed sources**

### Agent Jam by Metorial at YC (August 23, 2025)
- Location: Brex HQ, San Francisco
- Prize Pool: $10,000+ ($5K 1st/Pylon, $3K 2nd/Brex, $2K 3rd/Sixtyfour)
- Focus: Autonomous agents using Brex + YC company APIs
- Judges: 13 from Pylon, Sixtyfour, Able, Docket, Oki, Omnara, Slashy, ContextFort, Infer.so, Momentic, truthsystems
- Judge: Andrew Miklas (YC Partner, PagerDuty co-founder)
- Participants: 13
- **Winners: Project gallery not published**

### AgentMail's HackHalloween (October 2025)
- Hosts: AgentMail (YC S25), Replit (YC W18), Browser Use
- Prize Pool: $100,000+ in cash + credits
- Sponsors: OpenAI, Composio, Moss, Mastra
- **Winners: Not publicly announced in indexed sources**

### Hack the Stackathon (January 9, 2026)
- Hosts: Firecrawl (YC S22), Reducto (YC W24), Resend (YC W23)
- Location: Y Combinator HQ
- Prize: Guaranteed YC interview + $25,000 cash + $1,500,000 in credits
- Sponsors: MongoDB, Open Router, Supabase, ElevenLabs, Lovable
- Focus: Deep research agents, invoice pipelines, competitive intelligence, AI legal tools
- **Winners: Not publicly announced in indexed sources**

### Agentic Payments Hackathon by Locus (November 2025)
- Hosts: Locus (YC F25) at YC HQ
- Sponsors: OpenAI, Anthropic, Replit
- Prize: $25,000 + guaranteed YC interview
- Focus: New ways for agents to pay, even without humans in the loop
- **Winners: Not publicly announced in indexed sources**

### Bio x AI Hackathon (2025-2026, ongoing)
- Prize Pool: $125,000 for agentic biotech
- Format: 2-month global hackathon
- Midpoint Winner: Rare Compute (PDB-MCP Server for AI agents to access protein data)
- Final deadline: June 8 (results pending)

### Browser Use Web Agents Hackathon (Feb 28 - Mar 1, 2026)
- Location: Y Combinator, San Francisco
- Prize Pool: $100,000+
- Prize includes: Guaranteed YC interview + week at Browser Use hackerhouse
- Sponsors: DeepMind, Convex, VibeFlow, AgentMail, Hud, Superset, Vercel, MongoDB, Dedalus Labs, AWS, Anthropic, OpenAI, Minimax
- **Status: Recently completed (results likely pending)**

### YC x Google DeepMind: Multimodal Frontier Hackathon (March 2026)
- Technologies: Gemini 3.1, Lyria, NanoBanana 2
- Focus: Full multimodal stack applications
- **Status: Just occurred (results pending)**

---

## 8. HACKATHON-TO-STARTUP SUCCESS STORIES

| Project | Hackathon | Outcome |
|---------|-----------|---------|
| Soshi | Supabase AI @ YC (Nov 2024) | Venture-backed, 1,300+ users, first sales |
| Codapt | YC Agents (Aug 2025) | Funded AI app builder startup |
| April | Unknown YC hackathon | Accepted to YC S25, voice-first email assistant |
| Observee | MCP Hackathon @ YC | YC S25 company, observability for MCP |
| Vera Health | OpenAI x YC o1 (Oct 2024) | Partnership with ACEP, funded |
| Camfer | OpenAI x YC o1 (Oct 2024) | Featured at OpenAI DevDay |

---

## 9. WHAT MAKES YC HACKATHON WINNERS STAND OUT

Based on analysis of all confirmed winners, consistent patterns emerge:

### 1. Real Problems, Not Demos
Every major winner solved a genuine problem: Codapt (building production apps), Vera Health (clinical decision support), Camfer (engineering design), Soshi (social media marketing), Vital Link (health data integration). Judges consistently reward utility over novelty.

### 2. Production Readiness
Winners ship code that works beyond the demo environment. Codapt generates "production-ready web apps," Vera Health's voice agent was "the fastest method for clinicians," Proxis delivered "10x cheaper" model serving. The bar is not "does it work?" but "could someone use this tomorrow?"

### 3. Demo-First Mindset
Riley Shu (3x hackathon winner) explicitly teaches: "Focus on live demonstrations, avoid slides. Emphasize the wow effect." The winning projects are those that make judges say "I didn't know that was possible."

### 4. Strategic Preparation
Multiple winners (Soshi, Vital Link) did market research and validation BEFORE the hackathon. Ayaan Gazali's team brought "combined experience of 55 hackathon wins." Elijah Muraoka's team "went in with a vision bigger than the hackathon itself."

### 5. Leverage Sponsor Tech Deeply
Winners don't just use sponsor tools superficially. Codapt won both Vercel AND Convex prizes by deeply integrating both. Camfer's o1 integration was architectural, not cosmetic. Suparova won "Most Novel Use of Supabase" by using it for a physical robot.

### 6. Small, Skilled Teams
Most winners are 2-4 people. Riley Shu recommends: "One coder, one generalist, one support member performs best."

---

## 10. CONFIDENCE ASSESSMENT

| Finding | Confidence |
|---------|-----------|
| OpenAI x YC o1 Hackathon winners (Proxis, Vera Health, Camfer) | HIGH -- officially announced by YC |
| Supabase AI Hackathon winners (Soshi, Dropout, Explainstein, Suparova) | HIGH -- published on Supabase blog |
| Codapt winning $65K at YC Agents Hackathon | HIGH -- multiple LinkedIn sources |
| Oreo winning Convex prize at YC Agents Hackathon | HIGH -- Convex official announcement |
| Vital Link winning $120K at Manufact/MCP Hackathon | HIGH -- winner's LinkedIn post |
| Gemini x Pipecat virtual winners (Boba Bot, etc.) | HIGH -- published results page |
| Per-track winners for YC Agents Hackathon 5 tracks | LOW -- not publicly documented |
| AI Coding Agents Hackathon winners | LOW -- not publicly documented |
| Full Stack Hackathon winners | LOW -- not publicly documented |
| Hack the Stackathon winners | LOW -- not publicly documented |

---

## 11. RECOMMENDED FOLLOW-UPS

1. **YC Agents Hackathon Discord:** The per-track winners were announced in the hackathon Discord channel. Someone with access could extract the full winner list for all 5 tracks.
2. **Direct contact with Dedalus Labs:** As hackathon hosts, they would have the complete results.
3. **Trevor Keith / Eduardo Ortiz Twitter:** May have posted about which specific tracks Codapt won beyond Vercel/Convex.
4. **Full Stack Hackathon:** Sim and Lovable may have announced winners on their respective platforms.
5. **Browser Use Hackathon results:** Just completed (Feb 28 - Mar 1, 2026) -- results should be announced soon.
6. **YC x Google DeepMind Multimodal Frontier Hackathon:** Just occurred in March 2026 -- results pending.
