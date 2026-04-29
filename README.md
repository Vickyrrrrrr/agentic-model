# AgentIC — Autonomous AI-Driven Silicon Compiler

> Natural Language → GDSII. Zero human intervention.

AgentIC converts plain English chip descriptions into fabrication-ready GDSII layouts through a fully autonomous 27-stage pipeline with self-healing error recovery.

## Download

| Platform | Binary | SHA-256 |
|----------|--------|---------|
| **Linux** (amd64) | [agentic-linux-amd64](https://github.com/VICKYRRRRRR/agentic-releases/releases/latest) | See release |
| **macOS** (amd64) | [agentic-darwin-amd64](https://github.com/VICKYRRRRRR/agentic-releases/releases/latest) | See release |

> 💡 Windows support coming soon. Use WSL2 in the meantime.

## Quick Start

```bash
# 1. Download and make executable
chmod +x agentic-linux-amd64

# 2. Set your LLM API key (any provider works)
export OPENAI_API_KEY=sk-...

# 3. Activate your license
./agentic-linux-amd64 login

# 4. Install a PDK
./agentic-linux-amd64 install-pdk sky130

# 5. Build your first chip
./agentic-linux-amd64 build \
  --name counter \
  --desc "8-bit up counter with synchronous reset and enable"
```

## Requirements

- **OSS CAD Suite** — for RTL synthesis and verification ([download](https://github.com/YosysHQ/oss-cad-suite-build/releases))
- **Docker** — for OpenLane GDSII hardening (optional — use `--skip-openlane` to bypass)
- **LLM API Key** — OpenAI, Anthropic, Groq, ZhipuAI, DeepSeek, Together AI, Ollama, or any OpenAI-compatible endpoint
- **License Key** — purchase from [buildstack.live](https://www.buildstack.live)

## What It Does

```
Your description ("8-bit counter with reset")
        │
        ▼
   Architectural specification (LLM)
        │
        ▼
   RTL generation + lint + CDC analysis (LLM + ReAct loop)
        │
        ▼
   Testbench + simulation + formal verification
        │
        ▼
   Synthesis + DFT + gate-level simulation
        │
        ▼
   Floorplanning + OpenLane hardening → GDSII
        │
        ▼
   DRC + LVS + multi-corner STA signoff
        │
        ▼
   Fabrication-ready chip layout ✅
```

All errors (timing violations, routing congestion, DRC failures) trigger automatic self-healing recovery — clock relaxation, area expansion, utilization adjustment, RTL repair, and LLM-guided root cause analysis.

## Supported PDKs

| PDK | Node | Type |
|-----|------|------|
| **sky130** | 130nm | Open-source, production-ready |
| **gf180mcu** | 180nm | Open-source, automotive-grade |
| asap7 | 7nm | Predictive, academic |
| nangate45 | 45nm | Academic |
| freepdk45 | 45nm | Academic |
| osu018 | 180nm | Educational |
| osu035 | 350nm | Educational |

## License

AgentIC is proprietary software. A valid license key is required to use the binary distribution. Purchase at [buildstack.live](https://www.buildstack.live).

The community edition (source) is available for non-commercial use. See the source repository for details.

---

[Terms of Service](https://buildstack.live/terms) · [Privacy Policy](https://buildstack.live/privacy) · [Refund Policy](https://buildstack.live/refund) · [buildstack.live](https://www.buildstack.live)
