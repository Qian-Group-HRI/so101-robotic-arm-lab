<p align="center">
  <img src="assets/images/X.png" width="900" alt="SO101 Robotic Arm Lab – Full Pipeline">
</p>

<h1 align="center">SO-101 Robotic Arm Lab</h1>

<p align="center">
  <strong>Qian Group · Human–Robot Interaction Lab · University of Houston</strong>
</p>

<p align="center">
  <em>From unboxing to autonomous manipulation — a complete, reproducible pipeline for building, calibrating, and deploying imitation-learning policies on the SO-101 robotic arm platform.</em>
</p>

<p align="center">
  <a href="https://github.com/Qian-Group-HRI/so101-robotic-arm-lab/stargazers">
    <img src="https://img.shields.io/github/stars/Qian-Group-HRI/so101-robotic-arm-lab?style=for-the-badge&color=3D348B&labelColor=2B2640" alt="Stars">
  </a>&nbsp;
  <a href="https://github.com/Qian-Group-HRI/so101-robotic-arm-lab/network/members">
    <img src="https://img.shields.io/github/forks/Qian-Group-HRI/so101-robotic-arm-lab?style=for-the-badge&color=6A8E4E&labelColor=2B2640" alt="Forks">
  </a>&nbsp;
  <a href="https://github.com/Qian-Group-HRI/so101-robotic-arm-lab/issues">
    <img src="https://img.shields.io/github/issues/Qian-Group-HRI/so101-robotic-arm-lab?style=for-the-badge&color=C4723A&labelColor=2B2640" alt="Issues">
  </a>&nbsp;
  <a href="#">
    <img src="https://img.shields.io/badge/platform-Jetson_Orin-76B900?style=for-the-badge&labelColor=2B2640" alt="Jetson Orin">
  </a>&nbsp;
  <a href="https://github.com/huggingface/lerobot">
    <img src="https://img.shields.io/badge/framework-LeRobot-FFD21E?style=for-the-badge&labelColor=2B2640" alt="LeRobot">
  </a>
</p>

<br>

---

<br>

## Table of Contents

| | Section | Description |
|---|---------|-------------|
| 🧭 | [Introduction](#introduction) | Project overview and motivation |
| ✨ | [Main Features](#main-features) | Key capabilities at a glance |
| 🆕 | [What's New in SO-101](#whats-new) | SO-100 → SO-101 upgrades |
| 📐 | [Specifications](#specifications-key-differences) | Motor, power, and sensor specs |
| 🔧 | [Complete Setup](#complete-setup) | Hardware assembly & software install |
| 🥝 | [KIWI Control Center](#kiwi-control-center) | Web dashboard for real-time arm control |
| 🧠 | [Imitation Learning](#imitation-learning) | Data collection → Training → Deployment |
| 🗺️ | [Roadmap](#roadmap) | What's coming next |
| 🤝 | [Contributing](#contributing) | How to get involved |
| 📜 | [Acknowledgments](#acknowledgments) | Credits and references |

<br>

---

<br>

## Introduction

The **SO-10xARM** is a fully open-source robotic arm platform from [TheRobotStudio](https://www.therobotstudio.com/) that pairs a **leader** arm (for teleoperation) with a **follower** arm (the robot executing the motion) 🤖. The project provides detailed 3D-printable parts, assembly instructions, and operation guides, making it possible to build a real robot from scratch rather than just simulating one.

On the software side, **[LeRobot](https://github.com/huggingface/lerobot)** is a PyTorch-based robotics framework focused on real-world control via **imitation learning**: it bundles models, curated datasets of human demonstrations, and simulation environments so users can start training and deploying policies without reinventing the full stack. The goal is simple but ambitious — drastically lower the barrier to real-world robotics by sharing reusable datasets and pretrained models, and progressively adding support for affordable, capable robot platforms like the SO-10xARM 🧠🛠️.

In our setup, the **SO-ARM10x** is integrated with a **reComputer Jetson AI kit** (Jetson Orin / AGX Orin), giving us a compact system that combines precise robotic arm control with serious on-board AI compute power. Together with LeRobot, this forms a complete development pipeline suitable for education, research, and light industrial automation: from building the arm and wiring the hardware, to configuring the environment, collecting demonstrations with the leader–follower setup, and training imitation learning policies that run directly on the Jetson platform 🎓🧪.

This documentation walks through that entire process — assembly, calibration, debugging, data collection, and model training — so that others in the lab (and beyond) can reproduce and extend our real-world LeRobot experiments on the SO-ARM10x.

<br>

---

<br>

## Main Features

| | Feature | Details |
|---|---------|---------|
| 🧩 | **Open-source & affordable** | Fully open-source, low-cost robotic arm solution from TheRobotStudio, suitable for students, labs, and hobbyists. |
| 🤖 | **Deep LeRobot integration** | Designed to plug directly into the LeRobot framework for data collection, imitation learning, and deployment. |
| 📚 | **Rich learning resources** | Comes with detailed assembly and calibration guides, plus tutorials for testing, data collection, training, and deployment. |
| 🧠 | **NVIDIA Jetson compatible** | Supports deployment with reComputer Jetson platforms (e.g., Orin NX 16 GB), enabling on-board inference and real-time control. |
| 🥝 | **KIWI Control Center** | Web-based dashboard (Flask + SocketIO) for real-time arm control, gesture execution, and system monitoring. |
| 🏭 | **Multi-scene applications** | Applicable to education, research, and light industrial / automation tasks across diverse scenarios. |

<br>

---

<br>

<h2 id="whats-new">What's New in SO-101</h2>

The SO-ARM101 is a meaningful step up from the SO-ARM100 across reliability, control quality, and real-time human–robot interaction.

| Feature | SO-ARM100 | SO-ARM101 | Why It Matters |
|---------|-----------|-----------|----------------|
| **Wiring at joint 3** | Prone to disconnection; could restrict motion | Optimized wiring — no disconnections, full range of motion | More reliable experiments and a larger, safer workspace |
| **Leader arm gear ratios** | Motors required external gearboxes | Optimized internal gear ratios, no external gearbox needed | Simpler, cleaner hardware with smoother leader control |
| **Leader–follower mode** | One-way: human drives leader → follower copies | Two-way: leader can follow follower in real time | Enables human correction during learned policy execution |

<br>

<h3 align="center">🎬 Sample Training Demo</h3>

<p align="center">
  <a href="https://youtu.be/JrF_ymUvrqc">
    <img src="assets/images/hero_thumb.png" width="640" alt="SO-ARM101 leader–follower demo">
  </a>
</p>
<p align="center">
  <em>▶ Click to watch the SO-ARM101 leader–follower demo on YouTube</em>
</p>

<br>

---

<br>

## Specifications (key differences)

| Item | SO-ARM100 Kit | SO-ARM100 Kit Pro | SO-ARM101 Kit | SO-ARM101 Kit Pro |
|------|---------------|-------------------|---------------|-------------------|
| **Leader arm motors** | 12× ST-3215-C001 (7.4 V), ~1:345 all joints | 12× ST-3215-C018 / C047 (12 V), ~1:345 all joints | 1× C001 (7.4 V, ~1:345) J2 · 2× C044 (7.4 V, ~1:191) J1 & J3 · 3× C046 (7.4 V, ~1:147) J4–J6 | Same leader layout (12 V rails) * |
| **Follower arm** | Same as leader | Same as leader | Same as SO-ARM100 follower | Same as SO-ARM101 follower |
| **Power supply** | 5.5 × 2.1 mm barrel, 5 V 4 A | 5.5 × 2.1 mm barrel, 12 V 2 A | 5.5 × 2.1 mm barrel, 5 V 4 A | 12 V 2 A (follower) + 5 V 4 A (leader) |
| **Angle sensor** | 12-bit magnetic encoder | Same | Same | Same |
| **Operating range** | 0 °C – 40 °C | Same | Same | Same |
| **Communication** | UART | Same | Same | Same |

> \* *Exact motor list for SO-ARM101 Kit Pro to be confirmed.*

<br>

---

<br>

<h1 align="center">Complete Setup</h1>

<p align="center"><em>Each card below links to a dedicated guide. Follow them in order for a smooth build experience.</em></p>

<br>

<h3 align="center">Phase 1 — Planning & Fabrication</h3>

<p align="center">
  <a href="docs/bom.md">
    <img src="assets/images/bom.png" alt="Bill of Materials" width="30%" style="border-radius:12px; margin:0 8px;">
  </a>
  <a href="docs/ise.md">
    <img src="assets/images/ISE.png" alt="Initial Setup & Environment" width="30%" style="border-radius:12px; margin:0 8px;">
  </a>
  <a href="docs/3d.md">
    <img src="assets/images/3d.png" alt="3D Printing Guide" width="30%" style="border-radius:12px; margin:0 8px;">
  </a>
</p>

<br>

<h3 align="center">Phase 2 — Build & Configure</h3>

<p align="center">
  <a href="docs/install.md">
    <img src="assets/images/install.png" alt="Software Installation" width="30%" style="border-radius:12px; margin:0 8px;">
  </a>
  <a href="docs/configure_motors.md">
    <img src="assets/images/motors.png" alt="Motor Configuration" width="30%" style="border-radius:12px; margin:0 8px;">
  </a>
  <a href="docs/assembly.md">
    <img src="assets/images/Assembly.png" alt="Assembly Guide" width="30%" style="border-radius:12px; margin:0 8px;">
  </a>
</p>

<br>

<h3 align="center">Phase 3 — Calibrate & Operate</h3>

<p align="center">
  <a href="docs/calibrate.md">
    <img src="assets/images/calibration.png" alt="Calibration" width="30%" style="border-radius:12px; margin:0 8px;">
  </a>
  <a href="docs/teleoperate.md">
    <img src="assets/images/teleoperate.png" alt="Teleoperation" width="30%" style="border-radius:12px; margin:0 8px;">
  </a>
  <a href="docs/cameras.md">
    <img src="assets/images/cameras.png" alt="Camera Setup" width="30%" style="border-radius:12px; margin:0 8px;">
  </a>
</p>

<br>

---

<br>

<h1 align="center">🥝 KIWI Control Center</h1>

<p align="center">
  <em>Keep It Witty & Interactive — a web-based dashboard for real-time dual-arm control, gesture execution, and system monitoring.</em>
</p>

<br>

<p align="center">
  <a href="dashboard/">
    <img src="assets/images/kiwi_dashboard.png" alt="KIWI Control Center Dashboard" width="80%" style="border-radius:12px;">
  </a>
</p>

<br>

The **KIWI Control Center** is a Flask + SocketIO web dashboard that provides a browser-based interface for controlling both SO-101 arms in real time. It runs on both Windows and Jetson, and supports dual-arm management from a single screen.

**Key capabilities:**

| | Feature | Description |
|---|---------|-------------|
| 🤖 | **Dual-arm status** | Real-time position, temperature, and load readouts for all 12 servos across both leader and follower arms |
| 👋 | **Gesture library** | One-click execution of pre-built gestures (wave, nod, bow, high-five, thumbs up) with automatic return to resting position |
| 🌡️ | **Temperature monitoring** | Live temperature chart tracking servo heat across both arms over time |
| 🔒 | **Port-safe architecture** | Thread-safe serial communication using `threading.Lock()` — no port conflicts between status polling and gesture commands |
| 🔴 | **Emergency stop** | Instant torque kill across all servos from the browser |
| 🔍 | **Auto port detection** | Automatically finds connected arms on startup — works with COM ports (Windows) and `/dev/ttyACM*` (Jetson/Linux) |

**Quick start:**

```bash
cd dashboard
pip install flask flask-socketio scservo-sdk pyserial
python app.py --leader COM5 --follower COM6   # Windows
python app.py --leader /dev/ttyACM0 --follower /dev/ttyACM1  # Jetson/Linux
python app.py --simulate   # Demo mode without hardware
```

Then open **http://localhost:5000** in your browser.

> 📖 **Dashboard source →** [dashboard/](dashboard/)

<br>

---

<br>

<h1 align="center">Imitation Learning</h1>

<p align="center">
  <em>Teach the robot by showing, not programming — collect human demonstrations, train a visuomotor policy, and deploy it back on the real arm.</em>
</p>

<br>

Imitation learning (IL) is the core approach we use to make the SO-101 perform useful tasks autonomously. Instead of hand-coding every motion, we **record expert demonstrations** using the leader–follower teleoperation setup, then **train a neural policy** that maps camera observations and joint states to motor actions. The trained policy is deployed directly on the arm (or on the Jetson for on-board inference), producing fluid, reactive behavior that generalizes across small variations in object position and orientation.

LeRobot supports several state-of-the-art IL architectures out of the box. The two we focus on in this lab are:

| Architecture | What It Does | Strengths |
|---|---|---|
| **ACT** (Action Chunking with Transformers) | Predicts *chunks* of future actions using a Transformer, reducing compounding error. | Fast inference, smooth trajectories, works well with 50–100 demonstrations. |
| **Diffusion Policy** | Formulates action prediction as a denoising diffusion process over the action space. | Handles multi-modal action distributions; robust to ambiguous demonstrations. |

<br>

The imitation learning workflow has three stages, each covered in detail below.

<br>

<h2 align="center">Stage 1 · Data Collection</h2>

<p align="center">
  <a href="docs/data_collection.md">
    <img src="assets/images/data_collection.png" alt="Data Collection Guide" width="55%" style="border-radius:12px;">
  </a>
</p>

<br>

High-quality demonstrations are the foundation of every successful policy. During data collection, a human operator physically moves the **leader arm** to perform a task while the **follower arm** mirrors the motion in real time. LeRobot simultaneously records:

- **Joint positions** from all 6 servos on both arms (state + action pairs)
- **Camera frames** from one or more USB cameras observing the workspace
- **Timestamps** for precise temporal alignment

**Best practices for collecting demonstrations:**

- **Consistency matters.** Keep object placement, lighting, and camera angles as stable as possible across episodes. Small, deliberate variations help generalization — random chaos does not.
- **Aim for 50–100 episodes** per task as a starting point. Simple pick-and-place tasks can work with fewer; complex multi-step tasks may need more.
- **Slow, deliberate motions** produce cleaner data than fast, jerky ones. The policy learns from what it sees — noisy demonstrations yield noisy behavior.
- **Review your data** after collection. LeRobot's `visualize_dataset` utility lets you scrub through episodes and catch bad recordings before they pollute training.

```bash
# Example: record 50 episodes for a pick-and-place task
python lerobot/scripts/control_robot.py \
  --robot.type=so101 \
  --control.type=record \
  --control.fps=30 \
  --control.single_task="Pick up the block and place it in the bin" \
  --control.repo_id=YOUR_HF_USERNAME/so101_pick_place \
  --control.num_episodes=50 \
  --control.push_to_hub=1
```

Each episode is stored as a self-contained record (joint arrays + image frames + metadata) and can optionally be pushed to the HuggingFace Hub for versioning and sharing.

> 📖 **Full walkthrough →** [docs/data_collection.md](docs/data_collection.md)

<br>

---

<br>

<h2 align="center">Stage 2 · Training</h2>

<p align="center">
  <a href="docs/training.md">
    <img src="assets/images/training.png" alt="Training Guide" width="55%" style="border-radius:12px;">
  </a>
</p>

<br>

Once demonstrations are collected, the next step is to train a policy that can reproduce (and generalize from) the recorded behavior. LeRobot handles the heavy lifting — dataset loading, augmentation, model architecture, and logging — so you can focus on experiment design.

**Training overview:**

1. **Choose an architecture.** ACT is a great default — fast to train, easy to tune. Switch to Diffusion Policy if your task has multiple valid strategies (e.g., the robot could approach an object from either side).
2. **Configure your run.** LeRobot uses Hydra-based YAML configs for full control over hyperparameters, dataset splits, and training schedules.
3. **Launch training.** A single command kicks off the full pipeline — data loading, model initialization, optimization, checkpointing, and WandB / TensorBoard logging.
4. **Monitor convergence.** Watch the training and validation loss curves. For ACT, you should see action-prediction loss drop steadily within the first few thousand steps.

```bash
# Example: train an ACT policy on collected demonstrations
python lerobot/scripts/train.py \
  --policy.type=act \
  --dataset.repo_id=YOUR_HF_USERNAME/so101_pick_place \
  --dataset.episodes=[0:50] \
  --training.num_epochs=2000 \
  --training.batch_size=8 \
  --eval.use_async_eval=true \
  --output_dir=outputs/act_pick_place \
  --wandb.enable=true
```

**Hardware notes:**

| Platform | Training Experience |
|---|---|
| **Cloud / desktop GPU** (RTX 3090, A100, etc.) | Recommended for full training runs. ACT trains in ~2–4 hours on 50 episodes. |
| **Jetson Orin Nano Super** | Viable for small-scale fine-tuning and experimentation. Full training is slower but absolutely doable for sub-200M-param models. |

**Tips for better policies:**

- **Start small.** Train on 20 episodes first. If the policy learns the rough motion, scale up data. If it doesn't, fix your data before collecting more.
- **Use image augmentation.** LeRobot supports random crops, color jitter, and more. This significantly improves generalization to lighting and camera shifts.
- **Save checkpoints frequently.** Sometimes an earlier checkpoint outperforms the final one — especially if you overtrain on a small dataset.

> 📖 **Full walkthrough →** [docs/training.md](docs/training.md)

<br>

---

<br>

<h2 align="center">Stage 3 · Evaluation & Deployment</h2>

<p align="center">
  <a href="docs/deployment.md">
    <img src="assets/images/deployment.png" alt="Deployment Guide" width="55%" style="border-radius:12px;">
  </a>
</p>

<br>

The final stage closes the loop: load the trained policy, run inference in real time, and watch the arm execute the task autonomously. This is where all the work pays off — and where you'll iterate fastest.

**Deployment workflow:**

1. **Load a checkpoint.** Point the deployment script at your best checkpoint (from training or downloaded from the Hub).
2. **Run the policy.** The script reads live camera frames and current joint positions, feeds them through the policy network, and sends predicted actions to the follower arm's servos.
3. **Evaluate and iterate.** Run 10+ evaluation episodes. Track success rate, watch for failure modes, and decide whether you need more data, different augmentation, or longer training.

```bash
# Example: deploy a trained ACT policy on the real arm
python lerobot/scripts/control_robot.py \
  --robot.type=so101 \
  --control.type=record \
  --control.fps=30 \
  --control.single_task="Pick up the block and place it in the bin" \
  --control.policy.path=outputs/act_pick_place/checkpoints/last/pretrained_model \
  --control.num_episodes=10
```

**What to expect on your first deployment:**

The policy will likely be *close but imperfect*. Common issues and fixes:

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| Arm reaches toward the object but misses | Camera angle shifted between data collection and deployment | Re-mount the camera or collect a few more demos with the current setup |
| Gripper closes too early / too late | Inconsistent gripper timing in demonstrations | Re-record episodes with more deliberate gripper actions |
| Jerky, stuttering motion | Low control frequency or policy inference too slow | Increase FPS, reduce image resolution, or use a lighter model |
| Arm freezes or produces random actions | Wrong checkpoint or mismatched configuration | Verify the config YAML matches the training setup exactly |

**Deploying on Jetson Orin Nano Super:**

For fully on-board inference (no laptop required), the Jetson Orin Nano Super is the recommended platform. The 8 GB of shared GPU memory handles ACT and Diffusion Policy models comfortably for real-time control at 30 FPS with a single camera stream.

> 📖 **Full walkthrough →** [docs/deployment.md](docs/deployment.md)

<br>

---

<br>

<h2 align="center">The Full Loop</h2>

<p align="center">
  <em>The imitation learning cycle is inherently iterative — each deployment reveals what the policy still needs to learn, which informs the next round of data collection.</em>
</p>

<br>

```
  ┌──────────────────────────────────────────────────────────────────┐
  │                                                                  │
  │    ┌─────────────┐    ┌─────────────┐    ┌──────────────────┐   │
  │    │    COLLECT   │    │    TRAIN    │    │     DEPLOY       │   │
  │    │  demos with  │───▶│  ACT or     │───▶│  run policy on   │   │
  │    │  leader arm  │    │  Diffusion  │    │  the real arm    │   │
  │    └─────────────┘    └─────────────┘    └────────┬─────────┘   │
  │           ▲                                       │             │
  │           │           Evaluate & iterate          │             │
  │           └───────────────────────────────────────┘             │
  │                                                                  │
  └──────────────────────────────────────────────────────────────────┘
```

<br>

---

<br>

## Roadmap

We are actively extending this platform. Here's what's on the horizon:

- [x] **KIWI Control Center** — Web-based dashboard for real-time arm control, gesture execution, and system monitoring ✅
- [ ] **LeKiWi mobile base integration** — Mount the SO-101 on a mobile base for autonomous navigation + manipulation
- [ ] **Multi-arm coordination** — Synchronized dual-arm tasks (e.g., bi-manual pick-and-place, choreographed demos)
- [ ] **Face & emotion recognition** — Vision pipeline for personalized human–robot interaction
- [ ] **On-board Jetson deployment guide** — End-to-end tutorial for running everything on the Jetson Orin Nano Super without a laptop
- [ ] **Pre-trained policy zoo** — Ready-to-deploy checkpoints for common tasks (pick-place, stacking, sorting)

<br>

---

<br>

## Contributing

We welcome contributions from students, researchers, and hobbyists. Whether it's fixing a typo, adding a new task demo, or improving the training pipeline — every contribution helps.

1. **Fork** the repository
2. **Create a branch** for your feature (`git checkout -b feature/your-feature`)
3. **Commit** your changes with clear messages
4. **Open a Pull Request** describing what you changed and why

For questions, ideas, or bug reports, please [open an issue](https://github.com/Qian-Group-HRI/so101-robotic-arm-lab/issues).

<br>

---

<br>

## Acknowledgments

This project builds on the work of many open-source communities and research groups:

- **[TheRobotStudio](https://www.therobotstudio.com/)** — for the SO-10xARM hardware design and open-source philosophy
- **[HuggingFace LeRobot](https://github.com/huggingface/lerobot)** — for the imitation learning framework that powers our training and deployment pipeline
- **[NVIDIA Jetson](https://developer.nvidia.com/embedded-computing)** — for making powerful edge AI accessible to robotics researchers
- **[Vizuara AI](https://www.vizuara.ai/)** — *Modern Robotics Learning From Scratch* course by Dr. Rajat, which informed much of our learning journey
- **Qian Group, University of Houston** — for lab resources, mentorship, and the space to build

<br>

<p align="center">
  <img src="https://img.shields.io/badge/Built_with-LeRobot-FFD21E?style=flat-square&logo=huggingface&logoColor=black" alt="LeRobot">&nbsp;
  <img src="https://img.shields.io/badge/Powered_by-Jetson_Orin-76B900?style=flat-square&logo=nvidia&logoColor=white" alt="Jetson">&nbsp;
  <img src="https://img.shields.io/badge/Hardware-SO--101_Arm-3D348B?style=flat-square" alt="SO-101">&nbsp;
  <img src="https://img.shields.io/badge/Made_at-University_of_Houston-C8102E?style=flat-square" alt="UH">
</p>

<p align="center">
  <sub>© 2025 Qian Group · Human–Robot Interaction Lab · University of Houston</sub>
</p>
