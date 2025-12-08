<h1 align="center">SO101 Robotic Arm Lab</h1>

This repository is the central lab hub for the SO101 robotic arm under the Qian group. It documents everything from hardware assembly and calibration to control scripts, training pipelines, and imitation learning procedures, so new students and collaborators can go from unboxing to deployment without guesswork.

<h2>Introduction</h2>

The SO-10xARM is a fully open-source robotic arm platform from TheRobotStudio that pairs a **leader** arm (for teleoperation) with a **follower** arm (the robot executing the motion) 🤖. The project provides detailed 3D-printable parts, assembly instructions, and operation guides, making it possible to build a real robot from scratch rather than just simulating one. On the software side, **LeRobot** is a PyTorch-based robotics framework focused on real-world control via **imitation learning**: it bundles models, curated datasets of human demonstrations, and simulation environments so users can start training and deploying policies without reinventing the full stack. The goal is simple but ambitious: drastically lower the barrier to real-world robotics by sharing reusable datasets and pretrained models, and progressively adding support for affordable, capable robot platforms like the SO-10xARM 🧠🛠️.

<p align="center">
  <img src="assets/images/X.png" width="900" alt="SO101 pipeline">
</p>

In our setup, the **SO-ARM10x** is integrated with a **reComputer Jetson AI kit** (Jetson Orin / AGX Orin), giving us a compact system that combines precise robotic arm control with serious on-board AI compute power. Together with the **LeRobot** framework, this forms a complete development pipeline suitable for education, research, and light industrial automation: from building the arm and wiring the hardware, to configuring the environment, collecting demonstrations with the leader–follower setup, and training imitation learning policies that run directly on the Jetson platform 🎓🧪. This documentation (wiki/README) walks through that entire process—assembly, calibration, debugging, data collection, and model training—so that others in the lab (and beyond) can reproduce and extend our real-world LeRobot experiments on the SO-ARM10x.

<h2>Main Features</h2>

- **Open-source & affordable** 🧩 – Fully open-source, low-cost robotic arm solution from TheRobotStudio, suitable for students, labs, and hobbyists.
- **Deep LeRobot integration** 🤖 – Designed to plug directly into the LeRobot framework for data collection, imitation learning, and deployment.
- **Rich learning resources** 📚 – Comes with detailed assembly and calibration guides, plus tutorials for testing, data collection, training, and deployment so new users can get productive quickly.
- **NVIDIA Jetson compatible** 🧠 – Supports deployment with the reComputer Jetson platforms (e.g., Mini J4012 with Orin NX 16 GB), enabling on-board inference and real-time control.
- **Multi-scene applications** 🏭 – Applicable to education, research, and light industrial / automation tasks, enabling efficient and precise robot operation across diverse scenarios.



<h2>What's new?</h2>



| Feature                          | SO-ARM100                                                | SO-ARM101                                                                 | Why it matters                                                                 |
|----------------------------------|----------------------------------------------------------|---------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| Wiring at joint 3                | Wiring prone to disconnection; could restrict motion     | Optimized wiring that avoids disconnections and no longer limits movement | More reliable experiments and a larger, safer workspace for the arm            |
| Leader arm gear ratios          | Motors required external gearboxes for proper behavior   | Motors use optimized internal gear ratios, no external gearbox needed     | Simpler, cleaner hardware with smoother, more accurate leader control          |
| Leader–follower functionality    | One-way: human drives leader → follower copies           | Two-way: leader can follow follower motion in real time                    | Enables human intervention / correction during learned policy execution        |

<br><br>

<h3 align="center">Sample Training Demo</h3>

<p align="center">
  <a href="https://youtu.be/JrF_ymUvrqc">
    <img src="assets/images/hero_thumb.png" width="600" alt="SO-ARM101 leader–follower demo">
  </a>
</p>

<p align="center">
  <em>Click the thumbnail to watch the SO-ARM101 demo on YouTube.</em>
</p>


<h2>Specifications (key differences)</h2><br>

| Item              | SO-ARM100 Arm Kit                                                   | SO-ARM100 Arm Kit Pro                                                | SO-ARM101 Arm Kit                                                                                                                                     | SO-ARM101 Arm Kit Pro                                                |
|-------------------|---------------------------------------------------------------------|-----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| Leader arm motors | 12× ST-3215-C001 (7.4 V) servos, ~1:345 gear ratio on all joints    | 12× ST-3215-C018 / ST-3215-C047 (12 V) with ~1:345 ratio on all joints | 1× ST-3215-C001 (7.4 V, ~1:345) for joint 2; 2× ST-3215-C044 (7.4 V, ~1:191) for joints 1 & 3; 3× ST-3215-C046 (7.4 V, ~1:147) for joints 4–6 (incl. gripper) | Same leader motor layout as SO-ARM101 Arm Kit (12 V power rails) *    |
| Follower arm      | Same as leader arm                                                 | Same as leader arm                                                   | Same as SO-ARM100 follower arm                                                                                                                        | Same as SO-ARM101 follower arm                                        |
| Power supply      | 5.5 mm × 2.1 mm barrel jack, 5 V 4 A                               | 5.5 mm × 2.1 mm barrel jack, 12 V 2 A                                | 5.5 mm × 2.1 mm barrel jack, 5 V 4 A                                                                                                                  | 5.5 mm × 2.1 mm, 12 V 2 A (follower) + 5 V 4 A (leader)               |
| Angle sensor      | 12-bit magnetic encoder                                            | Same                                                                 | Same                                                                                                                                                  | Same                                                                   |
| Operating range   | 0 °C – 40 °C                                                       | Same                                                                 | Same                                                                                                                                                  | Same                                                                   |
| Communication     | UART                                                               | Same                                                                 | Same                                                                                                                                                  | Same                                                                   |
| Control method    | PC                                                                 | Same                                                                 | Same                                                                                                                                                  | Same                                                                   |

> *Tune the text in the last column once you have the exact motor list for SO-ARM101 Arm Kit Pro.

<br>


<h1 align="center"><b>Complete Setup</b></h1>

<p align="center">
  <a href="docs/bom.md">
      <img
        src="assets/images/bom.png"
        alt="BOM"
        width="30%"
        style="border-radius:12px; margin:0 8px;"
      >
  </a>
  <a href="docs/ise.md">
    <img
      src="assets/images/ISE.png"
      alt="3D Printing Guide"
      width="30%"
      style="border-radius:12px; margin:0 8px;"
    >
  </a>
  <a href="docs/3d.md">
    <img
      src="assets/images/3d.png"
      alt="Calibration"
      width="30%"
      style="border-radius:12px; margin:0 8px;"
    >
  </a>
</p>

***
<br>

<p align="center">
  <a href="docs/install.md">
    <img
      src="assets/images/install.png"
      alt="BOM"
      width="30%"
      style="border-radius:12px; margin:0 8px;"
    >
  </a>
  <a href="docs/configure_motors.md">
      <img
      src="assets/images/motors.png"
      alt="3D Printing Guide"
      width="30%"
      style="border-radius:12px; margin:0 8px;"
    >
  </a>
  <a href="docs/assembly.md">
      <img
      src="assets/images/Assembly.png"
      alt="Calibration"
      width="30%"
      style="border-radius:12px; margin:0 8px;"
    >
  </a>
  
</p>

<p align="center">
  <a href="docs/calibrate.md">
      <img
      src="assets/images/calibration.png"
      alt="Calibration"
      width="30%"
      style="border-radius:12px; margin:0 8px;"
    >
  </a>
  <a href="docs/">
      <img
      src="assets/images/teleoperate.png"
      alt="3D Printing Guide"
      width="30%"
      style="border-radius:12px; margin:0 8px;"
    >
  </a>
  <img
    src="assets/images/cameras.png"
    alt="Calibration"
    width="30%"
    style="border-radius:12px; margin:0 8px;"
  >
  
</p>

<br>


<h2 align="center"><b>Imitation Learning</b></h2>
<br><br>

---
