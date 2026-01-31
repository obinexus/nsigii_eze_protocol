# Evolution

### Activation‑state model (formal, minimal)
**States:** \(S=\{\textbf{NoSignal},\ \textbf{SignalStart},\ \textbf{NoiseStart},\ \textbf{NoiseStop},\ \textbf{PowerStart},\ \textbf{PowerStop}\}\).  
**Parameters (per agent/neuron/module):** **power** \(p\in[0,1]\), **signal** \(s\in\mathbb{R}_{\ge0}\), **noise** \(n\in\mathbb{R}_{\ge0}\), **threshold** \(\theta\).  
**Firing rule (single step):**
\[
\text{activate iff } s + \alpha p - \beta n > \theta
\]
where \(\alpha,\beta>0\) are gain factors (tunable). **If** activation occurs from a clear \(s\) → **SignalStart**; **if** activation driven by \(n\) (i.e., \(s\) small, \(n\) large) → **NoiseStart**. **PowerStart/Stop** are entered when \(p\) crosses a boot threshold \(p_{boot}\).  

**Transition semantics (discrete time):** evaluate the inequality each tick; update \(p,s,n\) by sensors/inputs; apply hysteresis to avoid chattering (use two thresholds \(\theta_{on}>\theta_{off}\)). **This is a small finite state machine you can simulate.**

---

### Lambda coherence rule (formal)
**Notation:** treat internal micro‑computations as **left lambdas** \(\lambda_L\) and external, observable actions as **right lambdas** \(\lambda_R\). Use standard lambda calculus notation for reduction and composition.  

**Rule (informal → formal):** *two internal coherent reductions produce one stable external action.*  
Formally:
\[
\lambda_R \;\equiv\; \mathcal{F}(\lambda_L,\lambda_L)
\]
where \(\mathcal{F}\) is a composition operator (e.g., sequential reduction then normalization). In reduction notation:
\[
\lambda_L \xrightarrow{\beta^*} v,\quad \lambda_L' \xrightarrow{\beta^*} v' \quad\Rightarrow\quad \lambda_R \xrightarrow{\beta^*} \text{normalize}(v\circ v')
\]
You can encode the “two‑left → one‑right” constraint as a **resource invariant**: require at least two internal reductions with coherence score \(C\) above a threshold before emitting \(\lambda_R\).

---

### Coherence operator \(C\) (scoring)
Define \(C\) as a function mapping a set of processes \(P=\{p_i\}\) to a scalar in \([0,1]\) that measures mutual support (inspired by computational coherence models) — e.g., weighted sum of pairwise support divided by max possible support:
\[
C(P)=\frac{\sum_{i<j} w_{ij}\, \text{support}(p_i,p_j)}{\sum_{i<j} w_{ij}}
\]
**Use \(C\) to gate emission:** only allow \(\lambda_R\) when \(C(P)\ge\tau\). This ties your QA/gating idea to a formal coherence test.

