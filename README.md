# GNN-Based Intrusion Detection in IoT Communication Graphs
### A Survey of Architectures, Datasets, and Open Challenges


> **Preprint:** *(link pending submission)*  


---

## Abstract

This survey examines whether reported progress in GNN-based IoT intrusion detection reflects genuine advances toward securing real-world deployments, or whether it is an artefact of a narrow, self-reinforcing experimental paradigm. The central thesis is that the primary constraints on progress are **not architectural** — they are foundational: how graphs are constructed from raw traffic, how datasets are collected and labelled, and how models are evaluated against deployment realities.

We present a **three-dimensional taxonomy** spanning graph structure, model architecture, and learning paradigm; a **quantitative landscape analysis** of 34 primary GNN-based studies; a **rigorous dataset audit**; and a **structured research agenda** of eight falsifiable challenges. Approximately 55% of the core corpus clusters in a single region of the design space — flow-based graphs × GCN/GAT × supervised learning — dominant not because it is optimal, but because it is convenient. The models are not the bottleneck. The foundations are.


---

## Corpus

50 papers assembled via systematic search across IEEE Xplore, ACM Digital Library, SpringerLink, and arXiv (January 2018 – March 2026). Taxonomy statistics (Sections 4–6) are computed over **Tiers 1–3 only (34 GNN-based papers)**. Tier 4 and 5 papers inform the dataset critique (Section 8) and survey positioning (Section 2).

| Tier | Scope | Count |
|------|-------|-------|
| **1** | Core GNN-based IoT IDS — GNN as primary model, explicit IoT focus | 14 |
| **2** | GNN-based IDS — broader scope or alternative graph formulations | 16 |
| **3** | Graph construction and topology studies | 4 |
| **4** | IoT IDS datasets and benchmarking papers | 5 |
| **5** | Related surveys (GNN security, IoT security, anomaly detection) | 11 |
| | **Total** | **50** |

### Year Distribution (Tiers 1–3, N=34)

| Year | Papers | Notes |
|------|--------|-------|
| 2020 | 1 | Field emergence |
| 2021 | 3 | Early edge-centric work |
| 2022 | 2 | E-GraphSAGE, Anomal-E |
| 2023 | 9 | Rapid growth phase |
| 2024 | 8 | Maturation, hybrid models |
| 2025 | 7 | Federated, LLM-hybrid |
| 2026 | 3 | Preprints / early access |

70.6% of GNN papers published 2023–2025.

---

## Taxonomy

Every GNN paper is classified across three axes. The dominant cluster — **flow-based × GCN/GAT × supervised** — accounts for ≈55% of Tier 1 papers.

### Axis I — Graph Structure

| Type | N | % | Key Limitation |
|------|---|---|----------------|
| Flow-based | 12 | 35.3% | No temporal continuity; breaks at window boundaries |
| Spatio-temporal (snapshot) | 8 | 23.5% | Discrete windows; no continuous-time modeling |
| Heterogeneous | 6 | 17.6% | Complex schema; limited generalisability |
| Similarity-based | 4 | 11.8% | Artificial structure; O(N²) cost; semantically uninterpretable |
| Learned graph | 4 | 11.8% | Training instability; O(N²) edge inference; no semantic interpretation |

### Axis II — Model Architecture

| Architecture | N | % |
|---|--:|--:|
| GraphSAGE-based | 9 | 26.5% |
| Hybrid / Spatio-temporal | 8 | 23.5% |
| GCN-based | 8 | 23.5% |
| GAT-based | 7 | 20.6% |
| Graph learning models | 4 | 11.8% |

### Axis III — Learning Paradigm

| Paradigm | N | % |
|---|--:|--:|
| Supervised | 25 | 73.5% |
| Semi-supervised | 4 | 11.8% |
| Federated | 2 | 5.9% |
| Self-supervised | 2 | 5.9% |
| Hybrid | 1 | 2.9% |

73.5% supervised despite known label scarcity in operational IoT environments. 

---

## Key Findings

| Finding | Detail |
|---------|--------|
| **Dominant cluster** | ≈55% of Tier-1 papers: flow-based × GCN/GAT × supervised — convenient, not optimal |
| **No native graph datasets** | All 34 GNN papers construct graphs post-hoc from tabular data |
| **Zero continuous-time models** | 0/8 spatio-temporal papers use TGN, JODIE, or any event-driven architecture |
| **Supervised dominance** | 73.5% supervised despite operational label scarcity |
| **No controlled ablations** | Only ≈18% of papers compare GNN vs. non-GNN baselines under identical conditions |
| **Reproducibility gap** | Minority release code; graph construction parameters routinely underreported |
| **Deployment chasm** | Near-zero papers evaluate under real-time, streaming, or resource-constrained conditions |

---

## Surveyed Papers

**Legend:** ✅ Explicit IoT focus · ⚠️ Borderline/IoT-adjacent · ❌ Out of scope

---

### Tier 1 — Core GNN-Based IoT IDS (14 papers)

| Paper | Year | Venue | GNN Model | Graph Type | Learning | Dataset(s) | IoT |
|-------|------|-------|-----------|------------|----------|------------|-----|
| [E-GraphSAGE: A Graph Neural Network based Intrusion Detection System for IoT](https://dl.acm.org/doi/10.1109/NOMS54207.2022.9789878) | 2022 | IEEE/IFIP NOMS | E-GraphSAGE | Flow-based | Supervised | BoT-IoT, ToN-IoT, NF-BoT-IoT, NF-ToN-IoT | ✅ |
| [Anomal-E: A Self-Supervised Network Intrusion Detection System based on Graph Neural Networks](https://dl.acm.org/doi/10.1016/j.knosys.2022.110030) | 2023 | Knowledge-Based Systems | E-GraphSAGE + DGI | Flow-based | Self-supervised | NF-UNSW-NB15-v2, NF-CSE-CIC-IDS2018-v2 | ✅ |
| [E-GRACL: an IoT intrusion detection system based on graph neural networks](https://link.springer.com/article/10.1007/s11227-024-06471-5) | 2025 | Journal of Supercomputing | Enhanced E-GraphSAGE + Contrastive Learning | Flow-based | Hybrid (Supervised + Self-supervised) | NF-BoT-IoT-v2, NF-ToN-IoT-v2, NF-CSE-CIC-IDS2018-v2 | ✅ |
| [Graph-based Solutions with Residuals for Intrusion Detection (E-ResGAT)](https://arxiv.org/abs/2111.13597) | 2021 | arXiv | E-ResGAT (GraphSAGE + GAT + residuals) | Flow-based (bipartite/line graph) | Supervised | UNSW-NB15, CIC-DarkNet, CSE-CIC-IDS, ToN-IoT | ⚠️ |
| [Applying self-supervised learning to network intrusion detection for network flows with GNN (NEGAT/NEGSC)](https://doi.org/10.1016/j.comnet.2024.110495) | 2024 | Computer Networks (Elsevier) | NEGAT + NEGSC | Flow-based | Self-supervised | NF-BoT-IoT, NF-BoT-IoT-v2, NF-CSE-CIC-IDS2018, NF-CSE-CIC-IDS2018-v2 | ⚠️ |
| [Graph-based federated learning approach for intrusion detection in IoT networks (FedGATSage)](https://www.nature.com/articles/s41598-025-25175-1) | 2025 | Scientific Reports | Hybrid GAT + GraphSAGE (federated) | Multi-level / hierarchical | Federated (Supervised) | NF-ToN-IoT, CIC-ToN-IoT | ✅ |
| [A new concatenated Multigraph Neural Network for IoT intrusion detection](https://doi.org/10.1016/j.iot.2023.100818) | 2023 | Elsevier Internet of Things | Hybrid GNN (GCN + GAT + GCN) | Multigraph | Supervised | ToN-IoT, BoT-IoT, NF-ToN-IoT, NF-BoT-IoT | ✅ |
| [Industrial IoT Intrusion Detection System Based on Graph Neural Network](https://www.mdpi.com/2073-8994/17/7/997) | 2025 | Symmetry (MDPI) | GraphSAGE + LSTM Aggregator | Spatio-temporal | Supervised | BoT-IoT, ACI-IoT-2023, OPCUA | ✅ |
| [BS-GAT: a network IDS based on GNN for edge computing](https://link.springer.com/article/10.1186/s42400-024-00296-8) | 2025 | Cybersecurity (SpringerOpen) | BS-GAT (Graph Attention Network) | Similarity-based | Supervised | NF-BoT-IoT-v2, NF-ToN-IoT-v2 | ⚠️ |
| [Unveiling the potential of Graph Neural Networks for robust Intrusion Detection](https://arxiv.org/pdf/2107.14756) | 2021 | arXiv | Custom Message Passing GNN (GRU-based) | Heterogeneous (host-flow) | Supervised | CIC-IDS2017 | ⚠️ |
| [Spatial–Temporal GNN with Autoencoder Pretraining for IoT Intrusion Detection](https://www.nature.com/articles/s41598-025-25175-1) | 2026 | Scientific Reports | ST-GNN + Graph Autoencoder | Spatio-temporal | Hybrid (Self-supervised + Supervised) | BoT-IoT, ToN-IoT | ✅ |
| [N-STGAT: Network Spatio-Temporal Graph Attention Network for IoT Intrusion Detection](https://ieeexplore.ieee.org/document/10285068) | 2023 | MDPI Sensors | Spatio-Temporal GAT | Spatio-temporal | Supervised | CIC-IDS2017, BoT-IoT | ✅ |
| [PPT-GNN: Pretrained Spatio-Temporal GNNs for Network Intrusion Detection](https://arxiv.org/abs/2403.11830) | 2024 | IEEE/Elsevier | Pretrained ST-GNN (contrastive + temporal) | Spatio-temporal | Self-supervised + Transfer | NF-BoT-IoT, NF-ToN-IoT | ✅ |
| [MST-GAT: Multimodal Spatio-Temporal Graph Attention Network for IoT Intrusion Detection](https://doi.org/10.1016/j.iot.2023.100818) | 2023 | IEEE/Elsevier | Multimodal ST-GAT | Multimodal | Supervised | BoT-IoT, IoT-23 | ✅ |

---

### Tier 2 — GNN-Based IDS: Broader Scope (16 papers)

| Paper | Year | Venue | GNN Model | Graph Type | Learning | Dataset(s) | IoT |
|-------|------|-------|-----------|------------|----------|------------|-----|
| [Advanced intrusion detection in IoT using Graph Attention Networks](https://www.nature.com/articles/s41598-025-94624-8) | 2025 | Scientific Reports | GAT | Similarity-based | Supervised | NSL-KDD | ✅ |
| [IIoT IDS based on Reconstructed Graph Neural Networks](https://ieeexplore.ieee.org/document/9802721) | 2023 | IEEE Trans. Network Science & Engineering | GCN with joint graph learning | Learned graph | Supervised | Mississippi ICS (gas pipeline, water tank) | ✅ |
| [Flow Topology-Based GCN for IDS in Label-Limited IoT Networks (TAGCN)](http://staff.ustc.edu.cn/~kpxue/paper/TNSM-xiaohengdeng-2023.01.pdf) | 2023 | IEEE Trans. Network and Service Management | TAGCN + Attention | Flow-based (time-constrained) | Semi-supervised | UNSW-NB15, CIC-Darknet2020, ISCXTor2016 | ✅ |
| [Automating Botnet Detection with Graph Neural Networks](https://arxiv.org/abs/2003.06344) | 2020 | MLSys Workshop | Custom GCN (random-walk normalization) | Flow-based | Supervised | Synthetic + CAIDA botnet traffic | ⚠️ |
| [NF-GNN: Network Flow Graph Neural Networks for Malware Detection and Classification](https://arxiv.org/abs/2103.03939) | 2021 | SSDBM | NF-GNN (custom edge-feature GNN) | Flow-based | Hybrid (Supervised + Unsupervised) | CICAndMal2017 | ⚠️ |
| [StrucTemp-GNN: Structural-Temporal GNN for IoT Intrusion Detection](https://link.springer.com/chapter/10.1007/978-3-031-52426-4_2) | 2023 | Springer | Hybrid GNN (GCN + temporal/GRU) | Spatio-temporal heterogeneous | Supervised | 4 IoT datasets | ✅ |
| [GNN-IDS: Graph Neural Network based Intrusion Detection System](https://dl.acm.org/doi/10.1145/3664476.3664515) | 2024 | ARES Conference (ACM) | GCN, GCN-EW, GAT | Hybrid attack + communication graph | Supervised | Synthetic + CIC-IDS2017 | ⚠️ |
| [Leveraging Graph Neural Networks for Botnet Detection](https://link.springer.com/chapter/10.1007/978-3-031-50920-9_11) | 2024 | Springer CCIS | Multiple (GCN, GraphSAGE, SGConv, TAGConv) | Flow-based | Supervised | ISCX-Bot-2014 | ⚠️ |
| [Top-K Similarity Graph Framework for IoT Intrusion Detection](https://www.mdpi.com/2078-2489/16/6/499) | — | MDPI | GraphSAGE | Similarity-based | Supervised | NF-ToN-IoT, NF-BoT-IoT | ✅ |
| [Dynamic Spatial–Temporal GNN for IDS in Internet of Vehicles](https://arxiv.org/abs/2507.10836) | 2025 | Scientific Reports | ST-GNN (GCN + temporal attention/GRU) | Spatio-temporal | Supervised | Vehicular IoT (VANET/IoV) | ✅ |
| [XG-NID: Explainable GNN for Network IDS with LLM Integration](https://arxiv.org/abs/2401.05680) | 2024 | IEEE/arXiv | Heterogeneous GNN + LLM explanation module | Heterogeneous | Hybrid (Supervised + LLM) | CIC-IDS2017, NF-ToN-IoT | ⚠️ |
| [K-GetNID: Knowledge-guided GNN for Intrusion Detection](https://ieeexplore.ieee.org/document/9686606) | 2024 | IEEE Trans. Information Forensics and Security | Knowledge-guided GNN (GraphSAGE/GAT hybrid) | Knowledge-enhanced | Supervised | CIC-IDS2017, NF-BoT-IoT | ⚠️ |
| [LGAT: Learning Graph Attention Networks for Intrusion Detection](https://arxiv.org/abs/2506.20806) | 2024 | Neurocomputing (Elsevier) | Graph Learning GAT (structure learning + attention) | Learned graph | Supervised | CIC-IDS2017, UNSW-NB15 | ⚠️ |
| [Graph Neural Networks for Network Anomaly Detection: A Unified Framework](https://dl.acm.org/doi/10.1145/3565571) | 2022 | IEEE Trans./Elsevier | GCN, GAT, GraphSAGE | Communication/feature graph | Hybrid (Supervised + Unsupervised) | Multiple network security datasets | ⚠️ |
| [Heterogeneous Graph Neural Networks for Cybersecurity Event Detection](https://dl.acm.org/doi/10.1145/3669906) | 2023 | ACM/IEEE | Heterogeneous GNN (R-GCN/HAN) | Heterogeneous security graph | Supervised | Enterprise cybersecurity datasets | ⚠️ |
| [Large Language Model-Augmented GNNs for Cyber Threat Detection](https://arxiv.org/abs/2502.10556) | 2025 | arXiv/IEEE | GNN + LLM hybrid | Heterogeneous + semantic | Hybrid (Supervised + LLM) | CIC-IDS2017, IoT-23 | ⚠️ |

---

### Tier 3 — Graph Construction and Topology Studies (4 papers)

Papers that directly examine how graph construction choices shape GNN performance — the empirical backbone of Section 7.

| Paper | Year | Venue | GNN Model | Graph Type | Learning | Dataset(s) | IoT |
|-------|------|-------|-----------|------------|----------|------------|-----|
| [How the Graph Construction Technique Shapes Performance in IoT Botnet Detection](https://arxiv.org/abs/2603.06654) | 2026 | arXiv | GAT | Similarity (kNN/Gabriel/ε-radius variants) | Supervised | N-BaIoT | ✅ |
| [Spatio-Temporal GNNs for Anomaly Detection in Complex Industrial Processes (ST-VGSAE)](https://ieeexplore.ieee.org/document/10285068) | 2026 | Sensors (MDPI) | ST-VGSAE (VGAE + GCN + Statistical Attention) | Spatio-temporal industrial | Unsupervised | Tennessee Eastman (TE) | ✅ |
| [Attention-based Graph Structure Learning for Network Intrusion Detection](https://doi.org/10.1016/j.comnet.2024.110495) | 2023 | IEEE/Elsevier | Attention-based Graph Learning GNN | Learned (attention-based) | Supervised | CIC-IDS2017, BoT-IoT | ⚠️ |
| [Adaptive Graph Learning for Intrusion Detection in Network Traffic](https://doi.org/10.1007/s11036-021-01843-0) | 2024 | Elsevier | Adaptive GNN (GCN + graph learning module) | Adaptive/dynamic learned | Supervised | NF-ToN-IoT, CIC-IDS2017 | ⚠️ |

---

### Tier 4 — Dataset and Benchmarking Papers (5 papers)

None are natively graph-structured — itself a central finding of Section 8.

| Paper | Year | Venue | Dataset Introduced | IoT-Specific | Native Graph |
|-------|------|-------|--------------------|---|---|
| [TON_IoT Telemetry Dataset: A New Generation Dataset of IoT and IIoT for Data-Driven IDS](https://doi.org/10.1109/ACCESS.2020.3022862) | 2020 | IEEE Access | TON_IoT | ✅ Yes | ❌ No |
| [Toward Generating a New Intrusion Detection Dataset and Intrusion Traffic Characterization (CIC-IDS2017)](https://www.researchgate.net/publication/322870767) | 2018 | ICISSP | CIC-IDS2017 | ⚠️ Partial | ❌ No |
| [NetFlow Datasets for ML-based Network Intrusion Detection Systems](https://arxiv.org/abs/2011.09144) | 2020 | arXiv | NF-UNSW-NB15, NF-BoT-IoT, NF-ToN-IoT, NF-CSE-CIC-IDS2018, NF-UQ-NIDS | ⚠️ Partial | ❌ No |
| [IoT-23: A labeled dataset with malicious and benign IoT network traffic](https://doi.org/10.5281/zenodo.4743745) | 2020 | Zenodo | IoT-23 | ✅ Yes | ❌ No |
| [Towards a Standard Feature Set for Network Intrusion Detection System Datasets](https://doi.org/10.1007/s11036-021-01843-0) | 2022 | Mobile Networks & Applications | Standardised NetFlow feature set (43 features) | ⚠️ Partial | ❌ No |

---

### Tier 5 — Related Surveys (11 papers)

Used to position this survey in Section 2. This is the only survey that is simultaneously GNN-specific, IoT-specific, and construction-critical — with a quantitative corpus analysis, a dataset audit against IoT realism criteria, and an explicit normative argument that construction methodology is the primary bottleneck.

#### Group A — IoT Security Surveys (Broad)

| Paper | Year | Venue | GNN-Specific | IoT-Specific | Construction Critique |
|-------|------|-------|---|---|---|
| [A Survey of Machine and Deep Learning Methods for Internet of Things (IoT) Security](https://ieeexplore.ieee.org/document/9072101/) | 2020 | IEEE COMST | No | ✅ Yes | No |
| [Machine Learning in IoT Security: Current Solutions and Future Challenges](https://www.researchgate.net/publication/340453998) | 2020 | IEEE COMST | No | ✅ Yes | No |
| [Deep Learning-Based Intrusion Detection Systems: A Systematic Review](https://doi.org/10.1109/ACCESS.2021.3097247) | 2021 | IEEE Access | No | ⚠️ Partial | No |
| [Deep learning for intrusion detection in emerging technologies: a comprehensive survey and new perspectives](https://link.springer.com/article/10.1007/s10462-025-11346-z) | 2025 | Artificial Intelligence Review | No | ✅ Yes | No |
| [A survey on intrusion detection system in IoT networks](https://www.sciencedirect.com/science/article/pii/S2772918424000481) | 2025 | Cyber Security and Applications | No | ✅ Yes | No |
| [A Survey of Deep Learning Technologies for Intrusion Detection in Internet of Things](https://ieeexplore.ieee.org/document/10379640/) | 2024 | IEEE Access | No | ✅ Yes | No |
| [A Review of Intrusion Detection Systems Using Machine and Deep Learning in IoT](https://doi.org/10.3390/electronics9071177) | 2020 | Electronics (MDPI) | No | ✅ Yes | No |

#### Group B — GNN Security and Malware Detection Surveys

| Paper | Year | Venue | GNN-Specific | IoT-Specific | Construction Critique |
|-------|------|-------|---|---|---|
| [A Survey on Malware Detection with Graph Representation Learning](https://dl.acm.org/doi/10.1145/3664649) | 2024 | ACM Computing Surveys | ✅ Yes | No | No |
| [Use of Graph Neural Networks in Aiding Defensive Cyber Operations](https://arxiv.org/abs/2401.05680) | 2024 | ACM Trans. Privacy & Security | ✅ Yes | No | No |

#### Group C — GNN IDS and Dynamic Graph Surveys (Closest Adjacent Work)

| Paper | Year | Venue | GNN-Specific | IoT-Specific | Construction Critique |
|-------|------|-------|---|---|---|
| [Graph Neural Networks for Intrusion Detection: A Survey on Graph Construction, Learning, and Deployment](https://www.sciencedirect.com/science/article/abs/pii/S0167404824001226) | 2024 | Computers & Security | ✅ Yes | ⚠️ Partial | ⚠️ Limited |
| [Dynamic Graph Neural Networks for Anomaly Detection: A Comprehensive Survey](https://arxiv.org/abs/2409.09957) | 2026 | Artificial Intelligence Review | ✅ Yes | No | No |

---

## Dataset Quick Reference

| Dataset | Type / Tier | IoT-Specific | Temporal | Native Graph | Key Limitation |
|---------|-------------|---|---|---|---|
| **NSL-KDD** | Synthetic / T1 | ❌ | ❌ | ❌ | Outdated; no IoT protocols |
| **UNSW-NB15 / NF-UNSW-NB15** | Semi-simulated / T1 | ⚠️ | ❌ | ❌ | Partially simulated; limited IoT realism |
| **BoT-IoT / NF-BoT-IoT** | Synthetic / T1 | ✅ | ❌ | ❌ | Scripted attacks; unrealistic traffic patterns |
| **CIC-IDS2017 / CSE-CIC-IDS2018** | Semi-realistic / T2 | ⚠️ | ⚠️ | ❌ | NetFlow abstraction; static evaluation |
| **TON_IoT / NF-ToN-IoT** | Semi-realistic / T2 | ✅ | ⚠️ | ❌ | Not graph-native; lacks streaming evaluation |
| **N-BaIoT** | Semi-realistic / T2 | ✅ | ❌ | ❌ | Statistical features only; device-specific scope |
| **IoT-23** | Real-world / T3 | ✅ | ⚠️ | ❌ | Limited annotation; no temporal graph structure |
| **Mississippi ICS** | Realistic industrial / T3 | ✅ | ⚠️ | ❌ | Small-scale; domain-specific |
| **Tennessee Eastman (TE)** | Simulated industrial / T2 | ✅ | ✅ | ❌ | Simulated; limited real-world validity |
| **ISCX-Bot-2014** | Semi-realistic / T2 | ⚠️ | ❌ | ❌ | Outdated; limited attack diversity |
| **CICAndMal2017** | Semi-realistic / T2 | ⚠️ | ❌ | ❌ | Android malware focus; limited IoT traffic |

No dataset in the corpus is simultaneously natively graph-structured, temporally continuous, and IoT-representative. See Section 8.

---

## Citation

*(To be added upon publication.)*

```bibtex
@article{gnn_iot_ids_survey_2026,
  title   = {Graph Neural Network Based Intrusion Detection in IoT Communication Graphs: 
             A Survey of Architectures, Datasets, and Open Challenges},
  author  = {Mubaraq Onipede},
  journal = {[Target Venue]},
  year    = {2026},
  note    = {Under review}
}
```

---

## License

Survey paper © the author(s). Corpus data files and README released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

---

*Last updated: June 2026 · Corpus covers January 2018 – May 2026*
