# Torus-10: Infinite Video Generation via Relational Message Passing

> **"The Intelligence is in the Record. The Weights are just the Physics."**

## 📌 TL;DR

**Torus-10** is a Proof-of-Concept implementation of the [Commitment Semantics with Latent Message Passing](https://github.com/AISemanticsStudy/commitment-semantics-with-latent-message-passing) theory applied to Video Generation.

Instead of using massive VRAM-heavy Diffusion models or standard Transformers with quadratic attention, this model uses a **Relational Database (PostgreSQL)** as an "Infinite KVCache" and a small **Pixel LLM** as a "Physics Engine."

By enforcing a **3-Torus Topology** (Space-Time wrapping) and a fixed **Moore Neighborhood** (Radius-1), this architecture achieves ** inference complexity**, allowing for infinite-resolution and infinite-duration video generation on consumer hardware.

---

## 🏗️ The Architecture

The system is a "Bi-Cameral" Generative State Machine composed of three parts:

### 1. The World Log (PostgreSQL)

* **Role:** The "Memory" and "Canvas".
* **Function:** Stores the **Idempotent Discrete Records (IDRs)**. Every pixel generated is an ACID transaction.
* **Innovation:** Replaces the ephemeral GPU KVCache with durable, queryable disk storage.

### 2. The Director (Frozen LLM)

* **Role:** High-Level Semantic Control.
* **Function:** Broadcasts a global "Concept Token" (e.g., "Explosion", "Calm Water") for each frame.
* **Topology:** 1D Causal Timeline.

### 3. The Physics Engine (Pixel LLM)

* **Role:** Local Transition Kernel.
* **Function:** Predicts the next state of a single patch based strictly on its immediate physical neighbors.
* **Topology:** 3-Torus (Space wraps to start; Time flows forward).
* **Context:** Fixed length of **10 Tokens** (Moore Neighborhood).

---

## 🧠 Why This Works (The Theory)

### The "Commitment" Definition

In this model, **Intelligence** is not the probability cloud in the GPU; it is the committed record in the Database.

* **Inference:** The collapse of probability into a specific Token ID.
* **Commitment:** The `INSERT` statement into the Log. Once inserted, the pixel becomes an immutable fact that future pixels must respect.

### The  Scalability

Because the Pixel LLM uses a fixed neighborhood (10 tokens), the computational cost to generate a pixel at `x=10,000` is identical to `x=0`.

* **Standard ViT:**  (Chokes on 4K video).
* **Torus-10:**  (Can generate Gigapixel textures).

---

## ⚙️ Technical Specifications

### Data Model

Instead of raw pixels, we use **Discrete Patches** (Vector Quantized tokens).

* **Unit:** 16x16 Pixel Patch.
* **Vocab:** 4096 Visual Tokens.
* **Neighborhood:** 1 Global + 1 Self (Past) + 8 Spatial Neighbors = **10 Tokens**.

### Database Schema (The "VRAM")

```sql
CREATE TABLE world_log (
    frame_id INT NOT NULL,
    x INT NOT NULL,
    y INT NOT NULL,
    token_id INT NOT NULL, -- The "Commitment"
    PRIMARY KEY (frame_id, x, y)
);
-- The DB grows linearly. It acts as a Write-Ahead Log (WAL) of the reality.

```

### Performance Constraints

| Metric | 256p Video | 4K Video |
| --- | --- | --- |
| **Grid Size** | 16x16 Patches | 240x135 Patches |
| **Tokens/Frame** | 256 | 32,400 |
| **Commitment Rate** | 7.6K / sec | 972K / sec |
| **Storage Growth** | ~2 MB / min | ~233 MB / min |
| **Rec. Hardware** | Raspberry Pi | NVIDIA RTX 3070 + SSD |

---

## 🚀 Usage

### 1. Training (Learning the Physics)

We train the Pixel LLM to learn the "Transition Rules" of the visual world (e.g., "Smoke rises", "Water flows").

```bash
# Data is loaded from DB, formatted into "Neighborhood Packets", and fed to the LLM.
python train_physics.py --dataset ./fluids_dataset --epochs 100

```

### 2. Inference (Creating Reality)

The inference loop is a "Read-Compute-Write" cycle against the Database.

```python
# Pseudocode of the Commitment Loop
db = PostgresConnection()
model = PixelLLM.load("physics_v1.pt")

for t in range(START_FRAME, END_FRAME):
    # 1. GATHER: Fetch the state of the universe at t-1
    #    Uses Torus logic (wrapping edges) to find neighbors.
    past_state = db.query_torus_state(frame=t-1)

    # 2. COMPUTE: Run the Physics Engine
    #    Inputs: [Global_Token, Top, Left, Right, Bottom...]
    logits = model(past_state)

    # 3. COLLAPSE: Sample from the probability distribution
    next_tokens = sample(logits)

    # 4. COMMIT: Materialize the new reality into the Log
    db.insert_batch(frame=t, tokens=next_tokens)
    print(f"Frame {t} Committed to History.")

```

---

## ❓ FAQ

### Why use a Relational DB? Isn't it slow?

For **Video**, no.

1. **Latency vs. Bandwidth:** We batch-commit whole frames. Postgres can handle millions of insertions per second in batches.
2. **Infinite Context:** The DB allows us to store Terabytes of history (long video) while the GPU only loads the "Active Surface" (the current frame). It breaks the VRAM bottleneck.

### Can this generate text?

**No.**
This architecture relies on **Local Locality** (a pixel depends on its physical neighbors). Text relies on **Semantic Non-Locality** (a word depends on a context from 1000 words ago). The "Torus" topology breaks for text.

### Is this a Cellular Automata?

Yes. It is effectively a **Neural Cellular Automata** where the "Update Rule" is a learned Transformer rather than a hard-coded script.
