# Making Agents Reliable With NeMo Agent Toolkit

> Production-ready reference implementation for building, deploying, and scaling reliable AI agents using the NVIDIA NeMo Agent Toolkit.

## Overview
This repository offers a comprehensive reference implementation for constructing production-grade AI agents, originally developed as part of the DeepLearning.AI short course, "Nvidia’s NeMo Agent Toolkit: Making Agents Reliable". It showcases architectural patterns, deployment configurations, and integration strategies across six progressive levels—ranging from fundamental agent concepts to a full production deployment featuring a full-stack web interface. 

The implementation caters to practitioners aiming to build scalable, observable, and reliable AI systems utilizing the NVIDIA NeMo Agent Toolkit.

### Core Capabilities
*   **Agent Development**: Complete workflow implementation utilizing the NeMo Agent Toolkit.
*   **Tool Integration**: Custom tool creation and capability extension.
*   **Observability & Monitoring**: Distributed tracing powered by Phoenix integration.
*   **Multi-Agent Orchestration**: Complex workflow management using LangGraph.
*   **Evaluation & Quality Assurance**: Testing frameworks alongside evaluation loops.
*   **Production Deployment**: Containerization, REST API, WebSocket support, and a responsive web UI.

---

## Repository Structure
The repository follows a progressive learning path consisting of 6 levels plus a production UI:

```text
MakingAgentsReliableWithNeMoAgentToolKit/
│
├── 📁 YourFirstNATWorkflow/          [Level 1] Start Here
│   ├── 01_Your_First_NAT_Workflow.ipynb
│   └── config.yml
│
├── 📁 AddingIntelligenceWithTools/   [Level 2] Build Custom Tools
│   ├── 02_Adding_Intelligence_with_Tools.ipynb
│   ├── simple_tool_demo/
│   └── climate_analyzer/
│
├── 📁 ObservabilityWithPhoenixTracing/[Level 3] Monitor Your Agents
│   ├── 03_Observability_with_Phoenix_Tracing.ipynb
│   └── climate_analyzer/
│
├── 📁 MultiAgentIntegrationAddingMath/[Level 4] Multi-Agent Systems
│   ├── 04_Multi_Agent_Integration_Adding_Math.ipynb
│   ├── climate_analyzer/
│   └── calculator_agent/
│
├── 📁 EvaluationFindingAndFixingBugs/ [Level 5] Evaluation & Testing
│   ├── 05_Evaluation_Finding_and_Fixing_Bugs.ipynb
│   └── climate_analyzer/
│
├── 📁 ProductionDeploymentWithNATUI/  [Level 6] Production Ready
│   ├── 06_Production_Deployment_with_NAT_UI.ipynb
│   ├── climate_analyzer/
│   └── NeMo-Agent-Toolkit-UI/           [Submodule → NVIDIA Official UI]
│
├── 📄 README.md                         This file
└── 📄 requirements.txt                  Python dependencies
```

### Implementation Levels
| Level | Component | Technical Focus |
|-------|-----------|-----------------|
| **1** | Core Agent Workflow | Configuration, NeMo orchestration patterns, agent initialization |
| **2** | Tool Integration | Custom tool development, capability extension, tool calling |
| **3** | Observability Layer | Distributed tracing, Phoenix integration, performance monitoring |
| **4** | Multi-Agent Systems | LangGraph orchestration, agent composition, complex workflows |
| **5** | Quality Assurance | Evaluation frameworks, testing strategies, debugging methodology |
| **6** | Production System | REST API, WebSocket communication, web UI, containerization, deployment |

---

## Getting Started

### System Requirements
*   **Python**: Version 3.10 or higher.
*   **Node.js**: Version 18 or higher (required for the web UI).
*   **Git**: Must have submodule support.
*   **Memory**: 4GB+ RAM (8GB+ is recommended).

### Installation
```bash
# Clone repository with submodules
git clone --recurse-submodules https://github.com/anubhavdogra1/NeMoAgentToolKitMakingAgentsReliable.git
cd NeMoAgentToolKitMakingAgentsReliable

# If already cloned:
git submodule update --init --recursive

# Install dependencies
pip install -r requirements.txt

# (Optional) Install UI dependencies
cd ProductionDeploymentWithNATUI/NeMo-Agent-Toolkit-UI
npm ci
```

### Basic Setup
```bash
# Start the NeMo Agent server (Level 6)
cd ProductionDeploymentWithNATUI/climate_analyzer
nat serve --config_file src/climate_analyzer/configs/config.yml \
          --host 127.0.0.1 --port 8000

# In another terminal, start the web UI
cd ProductionDeploymentWithNATUI/NeMo-Agent-Toolkit-UI
npm run dev
```
*(Access the interface at `http://localhost:3000`)*

---

## Key Features

*   **Modular Architecture**: Components are independently deployable across the 6 implementation levels. It features a clear separation of concerns (orchestration, tools, observability, QA) and offers reference patterns for standard agent development scenarios.
*   **Observability & Monitoring**: Includes integrated Phoenix tracing for complete operational visibility, distributed tracing across multi-agent systems, and performance metrics hooks at every level.
*   **Production-Ready Deployment**: Equipped with a REST API featuring OpenAI-compatible endpoints, real-time bidirectional WebSocket support, Docker containerization, and a proxy gateway for request routing.
*   **Quality Assurance**: Provides built-in evaluation frameworks to validate agent behavior, targeted testing patterns for multi-agent workflows, and robust debugging infrastructure.
*   **Professional Web Interface**: Offers an MIT-licensed React/Next.js frontend featuring real-time message streaming, execution tracking, tool call visualization, and responsive design elements.

---

## Architecture

### System Components (Level 6 Production Deployment)
```text
┌─────────────────────────────────────┐
│      Web Browser                    │
│   (React/Next.js UI)                │
└──────────────┬──────────────────────┘
               │ HTTP/WebSocket
               ↓
┌─────────────────────────────────────┐
│   Proxy Gateway (port 3000)         │
│  • Request transformation           │
│  • Session management               │
│  • WebSocket relay                  │
└──────────────┬──────────────────────┘
               │ HTTP API Calls
               ↓
┌─────────────────────────────────────┐
│   NeMo Agent Toolkit API (port 8000)│
│  • Climate Analysis Agent           │
│  • Calculator Agent (LangGraph)     │
│  • Tool execution                   │
└──────────────┬──────────────────────┘
               │
         ┌─────┴──────────────┐
         ↓                    ↓
    ┌─────────────┐    ┌──────────────┐
    │ Phoenix     │    │ External     │
    │ Tracing     │    │ Services     │
    │ (Obs)       │    │ & Data APIs  │
    └─────────────┘    └──────────────┘
```

---

## Usage Patterns

*   **Deployment Implementation (Level 6)**: Ideal for production environments, focusing on REST API configuration, proxy gateways, WebSocket relay mapping, and containerization patterns.
*   **Multi-Agent Systems (Level 4)**: Recommended for complex orchestration, highlighting LangGraph composition, agent state management, and multi-agent communication.
*   **Observability & Debugging (Level 3)**: Use for maintaining visibility over systems through Phoenix integration, performance profiling, and trace analysis.
*   **Tool Development (Level 2)**: Reference for building custom integrations, defining parameter validation, capability registration, and fallback strategies.
*   **Quality Assurance (Level 5)**: Implement these frameworks for evaluating agent behavior, executing targeted test cases, and benchmarking reliability.

---

## Common Operations

### Deploy Agent Service
```bash
# Start agent server with specified configuration
nat serve --config_file ./config.yml \
          --host 0.0.0.0 \
          --port 8000
```
*Provides an OpenAI-compatible `/v1/chat/completions` endpoint, API documentation at `/docs`, and health checks at `/health`.*

### Configure Web UI
```bash
# Set backend connection
export NAT_BACKEND_URL="https://api.example.com"
export NEXT_PUBLIC_NAT_WORKFLOW="climate-analysis"

# Start UI with proxy gateway
npm run dev
# Proxy runs on port 3000 (public)
# Next.js runs on port 3001 (internal)
```

### Integrate with Monitoring
```bash
# Configure Phoenix tracing endpoint
export OTEL_EXPORTER_OTLP_ENDPOINT="http://phoenix:6006"
```
*Traces are automatically collected and made available in the Phoenix UI for analysis.*

### Deploy Container
```bash
docker build -t agent-service .
docker run --env-file .env \
           -p 8000:8000 \
           agent-service
```

---

## Implementation Components
*   **Agent Services**: Features a climate analysis agent, configuration-driven setup, a LangGraph-based multi-agent example, and custom tool integrations.
*   **Web Interface**: Uses a React/Next.js frontend (via submodule), request routing proxies, session management middleware, and an OpenAI API compatibility layer.
*   **Observability Integration**: Packs Phoenix distributed tracing instrumentation alongside performance monitoring and error logging collection points.
*   **Development Resources**: Includes Jupyter notebooks loaded with full reference implementations, detailed configuration templates, and automated Docker setups.

---

## Resources & References
| Component | Documentation |
|-----------|---|
| **NeMo Agent Toolkit** | [github.com/NVIDIA/NeMo-Agent-Toolkit](https://github.com/NVIDIA/NeMo-Agent-Toolkit) |
| **Web UI (Submodule)** | [github.com/NVIDIA/NeMo-Agent-Toolkit-UI](https://github.com/NVIDIA/NeMo-Agent-Toolkit-UI) |
| **LangGraph Orchestration** | [langchain-ai.github.io/langgraph](https://langchain-ai.github.io/langgraph) |
| **Phoenix Observability** | [arize.com/phoenix](https://arize.com/phoenix) |

**License**: The `NeMo-Agent-Toolkit-UI` submodule tracks the upstream NVIDIA repository, operating under its own license terms.

---

## Support
*   **Course Materials**: This implementation is integrated within the DeepLearning.AI short course on building reliable AI agents.
*   **Questions & Issues**: Use this repository's issue tracker for implementation-specific questions, or visit the respective NVIDIA repositories for framework or web UI support.

---

## Accomplishment
*   **Anubhav Dogra** 
    *   [NeMo Agent Toolkit Certificate](https://www.deeplearning.ai/accomplishments/5dabc08b-99e6-4695-8fc2-22a86c500f35?accomplishmentId=5dabc08b-99e6-4695-8fc2-22a86c500f35&usp=sharing)

**Acknowledgments**:
*   Built using the [NeMo Agent Toolkit](https://github.com/NVIDIA/NeMo-Agent-Toolkit) by NVIDIA.
*   Web UI is based on the [NeMo Agent Toolkit UI](https://github.com/NVIDIA/NeMo-Agent-Toolkit-UI).
*   Course development provided by [DeepLearning.AI](https://www.deeplearning.ai).

---

## Contact
**Anubhav Dogra**

anubhavdogra7@gmail.com
