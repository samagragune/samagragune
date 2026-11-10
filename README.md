<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://capsule-render.vercel.app/api?type=waving&height=200&color=0:0d1117,50:0b3d4f,100:00f6ff&text=Samagra%20Gune&fontSize=48&fontColor=ffffff&animation=fadeIn&fontAlignY=36&desc=I%20build%20AI%20agents%20%E2%80%94%20and%20the%20systems%20that%20keep%20them%20honest&descAlignY=58&descSize=17">
  <source media="(prefers-color-scheme: light)" srcset="https://capsule-render.vercel.app/api?type=waving&height=200&color=0:e0fbff,50:6ee7f9,100:0b3d4f&text=Samagra%20Gune&fontSize=48&fontColor=0d1117&animation=fadeIn&fontAlignY=36&desc=I%20build%20AI%20agents%20%E2%80%94%20and%20the%20systems%20that%20keep%20them%20honest&descAlignY=58&descSize=17">
  <img alt="Samagra Gune" src="https://capsule-render.vercel.app/api?type=waving&height=200&color=0:0d1117,50:0b3d4f,100:00f6ff&text=Samagra%20Gune&fontSize=48&fontColor=ffffff&animation=fadeIn&fontAlignY=36&desc=I%20build%20AI%20agents%20%E2%80%94%20and%20the%20systems%20that%20keep%20them%20honest&descAlignY=58&descSize=17" width="100%">
</picture>

<a href="https://github.com/samagragune">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=24&duration=2800&pause=900&color=00F6FF&center=true&vCenter=true&width=720&lines=Building+a+control+plane+for+autonomous+AI+agents;Terminal-native+research+agents+with+cited+answers;Vision-language+reasoning+for+robotic+arms;Python+%E2%80%A2+TypeScript+%E2%80%A2+FastAPI+%E2%80%A2+Next.js" alt="What I build" />
</a>

<br/><br/>

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/samagragune/)
[![X](https://img.shields.io/badge/@gunesamagra-000000?style=for-the-badge&logo=x&logoColor=white)](https://x.com/gunesamagra)
[![GitHub followers](https://img.shields.io/github/followers/samagragune?style=for-the-badge&logo=github&label=Followers&color=00f6ff&labelColor=0d1117)](https://github.com/samagragune?tab=followers)
[![Stars](https://img.shields.io/github/stars/samagragune?style=for-the-badge&logo=github&label=Stars&color=00f6ff&labelColor=0d1117)](https://github.com/samagragune?tab=repositories)
<img src="https://komarev.com/ghpvc/?username=samagragune&label=Profile%20views&color=00f6ff&style=for-the-badge" alt="Profile views"/>

</div>

---

## ⚡ About me

```python
class Samagra:
    role       = "Software developer"
    builds     = ["AI agents", "agent infrastructure", "developer tools"]
    shipping   = "klaw — a control plane that can actually pause a running AI agent"
    stack      = {"backend": ["Python", "FastAPI", "SQLAlchemy"],
                  "frontend": ["TypeScript", "Next.js", "Tailwind"],
                  "ai": ["Gemini", "Claude", "Qwen2.5-VL", "SAM 2"]}
    principle  = "Never let the UI claim success before the system confirms it."
```

> [!TIP]
> Interested in agent reliability, LLM tooling or robotics? My DMs on [X](https://x.com/gunesamagra) and [LinkedIn](https://www.linkedin.com/in/samagragune/) are open.

---

## 🚀 What I'm building

### 🛡️ [klaw](https://github.com/samagragune/klaw) &nbsp;·&nbsp; the control plane for autonomous AI agents

[![Last commit](https://img.shields.io/github/last-commit/samagragune/klaw?style=flat-square&color=00f6ff&labelColor=0d1117&label=last%20commit)](https://github.com/samagragune/klaw/commits)
[![Top language](https://img.shields.io/github/languages/top/samagragune/klaw?style=flat-square&color=00f6ff&labelColor=0d1117)](https://github.com/samagragune/klaw)
[![Stars](https://img.shields.io/github/stars/samagragune/klaw?style=flat-square&color=00f6ff&labelColor=0d1117)](https://github.com/samagragune/klaw/stargazers)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js%2016-000000?style=flat-square&logo=nextdotjs&logoColor=white)

Most "agent observability" tools stream traces and stop there. **Watching an agent doesn't let you stop it.** klaw's SDK runs *inside* the agent's own coroutine and yields to the control plane at checkpoints: before every tool call, before every model call, and wherever you ask. Pause, resume, cancel and tool refusal are applied for real, and the dashboard only reports success after the runtime confirms it.

```mermaid
flowchart LR
    A["🤖 Your agent<br/>+ reliability SDK"] -- "events at every checkpoint" --> B["⚙️ Control plane<br/>FastAPI · detection"]
    B -- "desired state<br/>(pause · cancel · refuse tool)" --> A
    A -. "applied ✓" .-> B
    B <--> D[("Postgres / SQLite<br/>Redis event bus")]
    C["🖥️ Operator console<br/>Next.js · TypeScript"] -- "intervene" --> B
    B -- "live status" --> C
```

<details>
<summary><b>Integrating it is about ten lines</b></summary>

```python
from reliability import Supervisor

supervisor = Supervisor(agent_id="research-agent")

@supervisor.monitor(task="Research AI startups")
async def research():
    async with supervisor.tool("search", {"q": "AI startups"}) as call:
        call.set_result(await my_search("AI startups"))
    async with supervisor.llm("gpt-4o-mini") as call:
        response = await my_model_call()
        call.record_usage(response.prompt_tokens, response.completion_tokens)
```

Privacy by default: arguments and completions stay in your process. Only a locally computed SHA-256 fingerprint is sent, which is enough for the backend to detect identical repeated calls (loops).
</details>

<br/>

### 🔎 [Fynder](https://github.com/samagragune/Fynder-) &nbsp;·&nbsp; deep research, in your terminal

[![Last commit](https://img.shields.io/github/last-commit/samagragune/Fynder-?style=flat-square&color=00f6ff&labelColor=0d1117&label=last%20commit)](https://github.com/samagragune/Fynder-/commits)
[![Top language](https://img.shields.io/github/languages/top/samagragune/Fynder-?style=flat-square&color=00f6ff&labelColor=0d1117)](https://github.com/samagragune/Fynder-)
[![License](https://img.shields.io/github/license/samagragune/Fynder-?style=flat-square&color=00f6ff&labelColor=0d1117)](https://github.com/samagragune/Fynder-/blob/main/LICENSE)
![Python](https://img.shields.io/badge/python-3.10%2B-3776AB?style=flat-square&logo=python&logoColor=white)
![Gemini](https://img.shields.io/badge/Gemini-8E75B2?style=flat-square&logo=googlegemini&logoColor=white)

A terminal-native AI research agent. Ask a question in plain language and it plans, calls tools (live web search, arXiv, Wikipedia, page scraping, CSV analysis) and returns a **cited** answer. Every tool call is visible step by step with `--verbose`, and you can add your own tool in about five lines with a `@tool` decorator.

<br/>

### 🦾 [Cognitive Autonomy Layer for Robotic Arms](https://github.com/samagragune/Project_Exhibition-Team155-) &nbsp;·&nbsp; v3.0

[![Last commit](https://img.shields.io/github/last-commit/samagragune/Project_Exhibition-Team155-?style=flat-square&color=00f6ff&labelColor=0d1117&label=last%20commit)](https://github.com/samagragune/Project_Exhibition-Team155-/commits)
[![Top language](https://img.shields.io/github/languages/top/samagragune/Project_Exhibition-Team155-?style=flat-square&color=00f6ff&labelColor=0d1117)](https://github.com/samagragune/Project_Exhibition-Team155-)
![PyBullet](https://img.shields.io/badge/PyBullet-3D%20sim-ff6f00?style=flat-square)
![SAM 2.1](https://img.shields.io/badge/SAM%202.1-segmentation-0467DF?style=flat-square&logo=meta&logoColor=white)

This replaces hard-coded state machines and brittle end-to-end VLA models with **hierarchical multimodal reasoning** for low-cost robotic arms. It fuses SAM 2.1 segmentation with a metric depth sensor to get millimetre-accurate 3D grasp points, and the reasoning runs on Qwen2.5-VL, DeepSeek-VL2, Gemini or local models. It ships four simulated worlds (workspace sorting, Mars-rover sample curation, a chemistry lab and electronics QA) and a live web cockpit.

---

## 🛠️ Tech stack

<div align="center">

<picture>
  <source media="(prefers-color-scheme: light)" srcset="https://skillicons.dev/icons?i=py,ts,js,nodejs,fastapi,nextjs,react,tailwind&theme=light&perline=8">
  <img alt="Languages and frameworks" src="https://skillicons.dev/icons?i=py,ts,js,nodejs,fastapi,nextjs,react,tailwind&theme=dark&perline=8">
</picture>
<br/>
<picture>
  <source media="(prefers-color-scheme: light)" srcset="https://skillicons.dev/icons?i=postgres,redis,sqlite,docker,pytorch,linux,git,vscode&theme=light&perline=8">
  <img alt="Data, infra and tools" src="https://skillicons.dev/icons?i=postgres,redis,sqlite,docker,pytorch,linux,git,vscode&theme=dark&perline=8">
</picture>

<br/><br/>

**AI and models**

![Gemini](https://img.shields.io/badge/Google%20Gemini-8E75B2?style=for-the-badge&logo=googlegemini&logoColor=white)
![Claude](https://img.shields.io/badge/Claude-D97757?style=for-the-badge&logo=anthropic&logoColor=white)
![Hugging Face](https://img.shields.io/badge/Hugging%20Face-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white)
![Ollama](https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=ollama&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)

</div>

---

## 🧭 How I like to build

| | |
|---|---|
| 🔍 **Show the work** | Agents should expose every tool call, argument and result. Fynder's `--verbose` and klaw's traces exist for this. |
| ✅ **Confirm, don't assume** | A command is `pending → acknowledged → applied`. Nothing claims success early. |
| 🔒 **Private by default** | Send fingerprints, not payloads, unless the user opts in. |
| 🚢 **Ship, then sharpen** | Get it running end to end first, then make it better. |

---

<div align="center">

<sub>Thanks for stopping by. Always up for interesting conversations and collabs. 🚀</sub>

<img src="https://capsule-render.vercel.app/api?type=waving&height=110&color=0:00f6ff,50:0b3d4f,100:0d1117&section=footer" width="100%" alt=""/>

</div>
