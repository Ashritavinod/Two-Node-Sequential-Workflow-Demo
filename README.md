# LangGraph: Two-Node Sequential Workflow Demo 📝

This project demonstrates how to create a simple sequential workflow using **LangGraph**. It builds upon the single-node example by showing how to chain two nodes together, where each node modifies the shared state in a specific order.

## 📜 Overview

The goal of this project is to illustrate a basic sequential graph. The workflow processes personal information (`name` and `age`) in two distinct steps to construct a final greeting message.

This example is ideal for understanding how to control the flow of execution in LangGraph:
* **Shared State**: How different nodes can access and modify the same state object.
* **Sequential Processing**: How to define a fixed path from one node to the next.
* **Graph Edges**: The concept of connecting nodes to define the workflow's structure.

## ⚙️ How It Works

The workflow is a two-step process:

### 1. Defining the State (`AgentState`)

First, we define a state object using Python's `TypedDict`. This `AgentState` will be passed through our graph. It contains:
* `name`: The input name (string).
* `age`: The input age (integer).
* `final`: The final message, which is built up by the nodes (string, optional).

### 2. Creating the Processing Nodes

We define two separate Python functions, each acting as a node in our graph.

**Node 1: `process_name`**
This node takes the name from the state and creates the first part of the greeting. It sets the `final` attribute to `"Hi [name]."`.

**Node 2: `process_age`**
This node takes the age and the current `final` message from the state. It then appends the second part of the greeting, `" You are [age] years old!"`, to the existing message.

### 3. Building the Graph

We use LangGraph's `StateGraph` to build the sequential workflow. The flow is a simple chain: `(start) -> node_1 -> node_2 -> (finish)`.

