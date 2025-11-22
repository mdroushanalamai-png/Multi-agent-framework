<div align="center" id="top">
  <a href="https://bharatmatrix.ai">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://bharatmatrix.ai/assets/logo-dark.svg">
      <source media="(prefers-color-scheme: light)" srcset="https://bharatmatrix.ai/assets/logo-light.svg">
      <img src="https://bharatmatrix.ai/assets/logo-light.svg" alt="BharatMatrix">
    </picture>
  </a>
</div>

<div align="center">
  <a href="https://docs.bharatmatrix.ai">Documentation</a>
  <span>&nbsp;&nbsp;•&nbsp;&nbsp;</span>
  <a href="https://docs.bharatmatrix.ai/examples/introduction">Examples</a>
  <span>&nbsp;&nbsp;•&nbsp;&nbsp;</span>
  <a href="https://www.bharatmatrix.ai/?utm_source=github&utm_medium=readme&utm_campaign=bharatmatrix-github">Website</a>
  <br />
</div>

## What is BharatMatrix?

BharatMatrix is a multi-agent framework, runtime and control plane. Built for speed, privacy, and scale.

It provides a rich set of tools for building:

- **Agents** with memory, knowledge, session management, and advanced features like human-in-the-loop, guardrails, dynamic context management and best-in-class MCP support.
- **Multi-Agent Teams** that operate autonomously under a team leader that maintains shared state and context. Perfect for use cases where the scope exceeds beyond a single agent.
- **Step-based Workflows** for controlled, deterministic execution. Steps can be Agents, Teams, or regular python functions that run sequentially, in parallel, in loops, branches, or conditionally.

BharatMatrix also provides a ready-to-use FastAPI app (called the AgentOS) for serving your agents, teams and workflows in production. Stateless, horizontally scalable and designed for scale, the AgentOS gives you major head start in building your AI product.

## Getting started

If you're new to BharatMatrix, follow our [quickstart](https://docs.bharatmatrix.ai/introduction/quickstart) to build your first Agent and chat with it using the AgentOS UI.

After that, checkout the [examples gallery](https://docs.bharatmatrix.ai/examples/introduction) and build real-world applications with BharatMatrix.

## Example

Here's an example of an Agent that connects to an MCP server, manages conversation state in a database, is served using a FastAPI application that you can chat with using the [Bhartmatrix.ai Agent Os](https://os.bharatmatrix.ai).

```python bharatmatrix_agent.py
from bharatmatrix.agent import Agent
from bharatmatrix.db.sqlite import SqliteDb
from bharatmatrix.models.anthropic import Claude
from bharatmatrix.os import AgentOS
from bharatmatrix.tools.mcp import MCPTools

# ************* Create Agent *************
bharatmatrix_agent = Agent(
    name="BharatMatrix Agent",
    model=Claude(id="claude-sonnet-4-5"),
    # Add a database to the Agent
    db=SqliteDb(db_file="bharatmatrix.db"),
    # Add the BharatMatrix MCP server to the Agent
    tools=[MCPTools(transport="streamable-http", url="https://docs.bharatmatrix.ai/mcp")],
    # Add the previous session history to the context
    add_history_to_context=True,
    markdown=True,
)


# ************* Create AgentOS *************
agent_os = AgentOS(agents=[bharatmatrix_agent])
# Get the FastAPI app for the AgentOS
app = agent_os.get_app()

# ************* Run AgentOS *************
if __name__ == "__main__":
    agent_os.serve(app="bharatmatrix_agent:app", reload=True)
```

## AgentOS - Production Runtime for Multi-Agent Systems

Building Agents is easy, running them is hard, and that's where the AgentOS comes in. AgentOS is a high-performance runtime for serving multi-agent systems in production. Key features include:

1. **Pre-built FastAPI app**: AgentOS ships with a ready-to-use FastAPI app for orchestrating your agents, teams, and workflows. This gives you a major head start in building your AI product.

2. **Integrated Control Plane**: The [AgentOS UI](https://os.bharatmatrix.ai) connects directly to your runtime, letting you test, monitor, and manage your system in real time, giving you unmatched control over your system.

3. **Private by Design**: AgentOS runs entirely in your cloud, ensuring complete data privacy. No data ever leaves your system. This is ideal for security-conscious enterprises.

## The Complete Agentic Solution

For companies building agents, BharatMatrix provides the complete agentic solution:

- The fastest framework for building agents, multi-agent teams and agentic workflows.
- A ready-to-use FastAPI app that gets you building AI products on day one.
- A control plane for testing, monitoring and managing your system.

BharatMatrix brings a novel architecture that no other framework provides, your AgentOS runs securely in your cloud, and the control plane connects directly to it from your browser. You don't need to send data to any external services or pay retention costs, you get complete privacy and control.

## Designed for Agent Engineering

BharatMatrix is an incredibly feature-rich framework, designed for Agent Engineering. Here are some key features:

| **Category** | **Feature** | **Description** |
|---------------|-------------|-----------------|
| **Core Intelligence** | **Model Agnostic** | Works with any model provider so you can use your favorite LLMs. |
|  | **Type Safe** | Enforce structured I/O through `input_schema` and `output_schema` for predictable, composable behavior. |
|  | **Dynamic Context Engineering** | Inject variables, state, and retrieved data on the fly into context. Perfect for dependency-driven agents. |
| **Memory, Knowledge, and Persistence** | **Persistent Storage** | Give your Agents, Teams, and Workflows a database to persist session history, state, and messages. |
|  | **User Memory** | Built-in memory system that allows Agents to recall user-specific context across sessions. |
|  | **Agentic RAG** | Connect to 20+ vector stores (called **Knowledge** in BharatMatrix) with hybrid search + reranking out of the box. |
|  | **Culture (Collective Memory)** | Shared knowledge that compounds across agents and time. |
| **Execution & Control** | **Human-in-the-Loop** | Native support for confirmations, manual overrides, and external tool execution. |
|  | **Guardrails** | Built-in safeguards for validation, security, and prompt protection. |
|  | **Agent Lifecycle Hooks** | Pre- and post-hooks to validate or transform inputs and outputs. |
|  | **MCP Integration** | First-class support for the Model Context Protocol (MCP) to connect Agents with external systems. |
|  | **Toolkits** | 100+ built-in toolkits with thousands of tools, ready for use across data, code, web, and enterprise APIs. |
| **Runtime & Evaluation** | **Runtime** | Pre-built FastAPI based runtime with SSE compatible endpoints, ready for production on day 1. |
|  | **Control Plane (UI)** | Integrated interface to visualize, monitor, and debug agent activity in real time. |
|  | **Natively Multimodal** | Agents can process and generate text, images, audio, video, and files. |
|  | **Evals** | Measure your Agents' Accuracy, Performance, and Reliability. |
| **Security & Privacy** | **Private by Design** | Runs entirely in your cloud. The UI connects directly to your AgentOS from your browser, no data is ever sent externally. |
|  | **Data Governance** | Your data lives securely in your Agent database, no external data sharing or vendor lock-in. |
|  | **Access Control** | Role-based access (RBAC) and per-agent permissions to protect sensitive contexts and tools. |

Every part of BharatMatrix is built for real-world deployment — where developer experience meets production performance.

## Setup Your Coding Agent to Use BharatMatrix

For LLMs and AI assistants to understand and navigate BharatMatrix's documentation, we provide an [llms.txt](https://docs.bharatmatrix.ai/llms.txt) or [llms-full.txt](https://docs.bharatmatrix.ai/llms-full.txt) file. This file is built for AI systems to efficiently parse and reference our documentation.

### IDE Integration

When building BharatMatrix agents, using BharatMatrix documentation as a source in your IDE is a great way to speed up your development. Here's how to integrate with Cursor:

1. In Cursor, go to the "Cursor Settings" menu.
2. Find the "Indexing & Docs" section.
3. Add `https://docs.bharatmatrix.ai/llms-full.txt` to the list of documentation URLs.
4. Save the changes.

Now, Cursor will have access to the BharatMatrix documentation. You can do the same with other IDEs like VSCode, Windsurf etc.

## Performance

If you're building with BharatMatrix, you're guaranteed best-in-class performance by default. Our obsession with performance is necessary because even simple AI workflows can spawn hundreds of Agents and because many tasks are long-running -- stateless, horizontal scalability is key for success.

At BharatMatrix, we optimize performance across 3 dimensions:

1. **Agent performance:** We optimize static operations (instantiation, memory footprint) and runtime operations (tool calls, memory updates, history management).
2. **System performance:** The AgentOS API is async by default and has a minimal memory footprint. The system is stateless and horizontally scalable, with a focus on preventing memory leaks. It handles parallel and batch embedding generation during knowledge ingestion, metrics collection in background tasks, and other system-level optimizations.
3. **Agent reliability and accuracy:** Monitored through evals, which we'll explore later.

### Agent Performance

Let's measure the time it takes to instantiate an Agent and the memory footprint of an Agent. Here are the numbers (last measured in Oct 2025, on an Apple M4 MacBook Pro):

- **Agent instantiation:** ~3μs on average
- **Memory footprint:** ~6.6Kib on average

We'll show below that BharatMatrix Agents instantiate **529× faster than Langgraph**, **57× faster than PydanticAI**, and **70× faster than CrewAI**. BharatMatrix Agents also use **24× lower memory than Langgraph**, **4× lower than PydanticAI**, and **10× lower than CrewAI**.

> [!NOTE]
> Run time performance is bottlenecked by inference and hard to benchmark accurately, so we focus on minimizing overhead, reducing memory usage, and parallelizing tool calls.

### Instantiation Time

Let's measure instantiation time for an Agent with 1 tool. We'll run the evaluation 1000 times to get a baseline measurement. We'll compare BharatMatrix to LangGraph, CrewAI and Pydantic AI.

> [!NOTE]
> The code for this benchmark is available [here](https://github.com/bharatmatrix/bharatmatrix/tree/main/cookbook/evals/performance). You should run the evaluation yourself on your own machine, please, do not take these results at face value.

```shell
# Setup virtual environment
./scripts/perf_setup.sh
source .venvs/perfenv/bin/activate

# BharatMatrix
python cookbook/evals/performance/instantiate_agent_with_tool.py

# LangGraph
python cookbook/evals/performance/comparison/langgraph_instantiation.py
# CrewAI
python cookbook/evals/performance/comparison/crewai_instantiation.py
# Pydantic AI
python cookbook/evals/performance/comparison/pydantic_ai_instantiation.py
```

LangGraph is on the right, **let's start it first and give it a head start**. Then CrewAI and Pydantic AI follow, and finally BharatMatrix. BharatMatrix obviously finishes first, but let's see by how much.


### Memory Usage

To measure memory usage, we use the `tracemalloc` library. We first calculate a baseline memory usage by running an empty function, then run the Agent 1000x times and calculate the difference. This gives a (reasonably) isolated measurement of the memory usage of the Agent.

We recommend running the evaluation yourself on your own machine, and digging into the code to see how it works. If we've made a mistake, please let us know.

### Results

Taking BharatMatrix as the baseline, we can see that:

| Metric             | BharatMatrix | Langgraph   | PydanticAI | CrewAI     |
| ------------------ | ------------ | ----------- | ---------- | ---------- |
| **Time (seconds)** | 1×           | 529× slower | 57× slower | 70× slower |
| **Memory (MiB)**   | 1×           | 24× higher  | 4× higher  | 10× higher |

Exact numbers from the benchmark:

| Metric             | BharatMatrix | Langgraph | PydanticAI | CrewAI   |
| ------------------ | ------------ | --------- | ---------- | -------- |
| **Time (seconds)** | 0.000003     | 0.001587  | 0.000170   | 0.000210 |
| **Memory (MiB)**   | 0.006642     | 0.161435  | 0.028712   | 0.065652 |

> [!NOTE]
> BharatMatrix agents are designed for performance and while we share benchmarks against other frameworks, we should be mindful that accuracy and reliability are more important than speed.

## Contributions

We welcome contributions, read our [contributing guide](https://github.com/bharatmatrix/bharatmatrix/blob/v2.0/CONTRIBUTING.md) to get started.

## Telemetry

BharatMatrix logs which model an agent used so we can prioritize updates to the most popular providers. You can disable this by setting `BHARATMATRIX_TELEMETRY=false` in your environment.

<p align="left">
  <a href="#top">⬆️ Back to Top</a>
</p>
