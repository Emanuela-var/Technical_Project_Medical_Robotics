# 🏥 Concentric Tube Robot Simulation

<div align="center">

![SOFA](https://img.shields.io/badge/SOFA-v24.12.00-orange?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.12-blue?style=for-the-badge&logo=python&logoColor=white)
![MATLAB](https://img.shields.io/badge/MATLAB-Analysis-red?style=for-the-badge&logo=mathworks)
![License](https://img.shields.io/badge/License-Academic-green?style=for-the-badge)

**A SOFA-based simulation of a Concentric Tube Robot (CTR) for minimally invasive surgery**

*Technical Project - Medical Robotics*

*Università degli Studi di Napoli Federico II - PRISMA Lab*

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [CTR Design Parameters](#-ctr-design-parameters)
- [Development Environment](#-development-environment)
- [Project Structure](#-project-structure)
- [Installation](#-installation)
- [Usage](#-usage)
- [Keyboard Controls](#-keyboard-controls)
- [Workspace Analysis](#-workspace-analysis)
- [Tissue Interaction](#-tissue-interaction)
- [Results](#-results)
- [Authors](#-authors)

---

## 🎯 Overview

This project implements a simulation scene in **SOFA (Simulation Open Framework Architecture)** of a **Concentric Tube Robot (CTR)** interacting with elastic objects through keyboard commands.

**Concentric Tube Robots** are well suited for **minimally invasive surgery** inside body cavities. The particular composition of concentrically arranged tubes allows for simple, yet dextrous, robotic manipulators. Actuation is achieved mechanically by relative rotation and axial translation of all the tubes, producing tentacle-like motion.

### Project Goals

1. Model a CTR with three tubes using the Beam Adapter plugin
2. Implement keyboard controller for tube translation and rotation
3. Extract and plot the 3D workspace of the CTR tip
4. Generate volumetric mesh and elastic objects for tissue simulation
5. Simulate CTR interaction with soft and stiff tissues
6. Achieve target contact force of 0.3 N through parameter tuning

---

## ✨ Features

- **Three-tube CTR Model** using SOFA's Beam Adapter plugin
- **Real-time Keyboard Control** for individual tube manipulation
- **Tip Position Tracking** with CSV export functionality
- **3D Workspace Visualization** in MATLAB
- **Volumetric Mesh Generation** from surface meshes (liver)
- **Elastic Object Simulation** with configurable stiffness
- **Contact Force Registration** and analysis
- **Parameter Tuning** for achieving target force values

---

## 🔧 CTR Design Parameters

### Tube Specifications

| Parameter | Tube 1 (Outer) | Tube 2 (Medium) | Tube 3 (Inner) |
|-----------|----------------|-----------------|----------------|
| **Straight Length** | 110 mm | 135 mm | 170 mm |
| **Curved Length** | 30 mm | 40 mm | 55 mm |
| **Tube Radius** | 0.95 mm | 0.85 mm | 0.75 mm |
| **Radius of Curvature** | 100 mm | 115 mm | 140 mm |

### Material Properties

| Property | Inner Tube | Medium Tube | Outer Tube |
|----------|------------|-------------|------------|
| **Radius** [mm] | 0.75 | 0.80* | 0.95 |
| **Mass Density** [kg/m³] | 6450 | 8000* | 6450 |
| **Young's Modulus** [GPa] | 77 | 77 | 77 |

*\*Modified from nominal values to achieve 0.3 N contact force*

---

## 💻 Development Environment

<table>
<tr>
<td align="center" width="33%">
<img src="https://www.sofa-framework.org/wp-content/uploads/2021/05/SOFA_logo.png" width="100" alt="SOFA"/><br/>
<b>SOFA Framework</b><br/>
<sub>Physics simulation for deformable objects and robotics</sub>
</td>
<td align="center" width="33%">
<img src="https://upload.wikimedia.org/wikipedia/commons/2/21/Matlab_Logo.png" width="80" alt="MATLAB"/><br/>
<b>MATLAB</b><br/>
<sub>Data analysis and 3D visualization</sub>
</td>
<td align="center" width="33%">
<img src="https://www.python.org/static/community_logos/python-logo-generic.svg" width="120" alt="Python"/><br/>
<b>Python 3.12</b><br/>
<sub>Scripting and SOFA controllers</sub>
</td>
</tr>
</table>

### Required SOFA Plugins

- **BeamAdapter** - For modeling flexible beam structures
- **SoftRobots** - Soft robotics components
- **CGAL** - Mesh generation from polyhedron

---

## 📁 Project Structure

```
CTR_Medical_Robotics/
│
├── sofa_scenes/
│   ├── CTR_Group3_Simulation.py      # Main simulation scene
│   ├── CTR_Group3_pt4.py             # Interaction simulation
│   └── keyboard_controller.py         # Keyboard input handler
│
├── meshes/
│   ├── liver.obj                      # Surface mesh
│   └── liver_volumetric.vtk           # Generated volumetric mesh
│
├── data/
│   ├── tip_positions.csv              # Recorded tip positions
│   ├── tip_positions_plus10.csv       # +10% tube length case
│   ├── tip_positions_minus10.csv      # -10% tube length case
│   └── contact_forces.csv             # Force measurements
│
├── matlab_analysis/
│   ├── RM.m                           # 3D trajectory plotting
│   └── force_analysis.m               # Contact force analysis
│
├── docs/
│   ├── Technical_Project_Medical_Robotics.pdf
│   └── Presentation.pdf
│
└── README.md
```

---

## 🚀 Installation

### Prerequisites

1. **SOFA Framework v24.12.00** with Python 3.12 support
   ```bash
   # Follow installation guide at:
   # https://www.sofa-framework.org/download/
   ```

2. **BeamAdapter Plugin**
   ```bash
   # Install following:
   # https://sofa-framework.github.io/doc/
   ```

3. **Python Dependencies**
   ```bash
   pip install numpy scipy
   ```

4. **MATLAB** (for visualization and analysis)

### Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/CTR-Medical-Robotics.git
   cd CTR-Medical-Robotics
   ```

2. Copy scene files to SOFA share directory:
   ```bash
   cp sofa_scenes/*.py $SOFA_ROOT/share/sofa/
   ```

3. Launch SOFA and load the simulation:
   ```bash
   runSofa CTR_Group3_Simulation.py
   ```

---

## 🎮 Usage

### Running the Simulation

1. **Launch SOFA GUI**:
   ```bash
   runSofa sofa_scenes/CTR_Group3_Simulation.py
   ```

2. **Start Animation**: Click "Animate" button or press `Space`

3. **Control the CTR**: Use keyboard commands (see below)

4. **Record Data**: Press `t` for tip position, `f` for forces

---

## ⌨️ Keyboard Controls

| Key | Action |
|-----|--------|
| `1` | Select Tube 1 (Outer) |
| `2` | Select Tube 2 (Medium) |
| `3` | Select Tube 3 (Inner) |
| `u` | Insert selected tube (translate forward) |
| `j` | Retract selected tube (translate backward) |
| `h` | Rotate selected tube (clockwise) |
| `k` | Rotate selected tube (counter-clockwise) |
| `t` | Log current tip position to CSV |
| `f` | Record contact forces to CSV |

### Controller Implementation

The keyboard controller inherits from SOFA's `Sofa.Core.Controller` class and overrides `onKeypressedEvent()`:

```python
class KeyboardController(Sofa.Core.Controller):
    def onKeypressedEvent(self, event):
        key = event['key']
        if key == 'u':
            self.irController.deployControlledInstrument(self.selected_tube)
        elif key == 'h':
            self.irController.rotateControlledInstrument(self.selected_tube)
        # ... additional controls
```

---

## 📊 Workspace Analysis

The 3D workspace is generated by varying insertion length and rotation of each tube, then plotting the tip positions.

### Comparison Cases

| Case | Inner Tube Length | Medium Tube Length |
|------|-------------------|-------------------|
| **Nominal** | 170 mm | 135 mm |
| **+10%** | 187 mm | 148.5 mm |
| **-10%** | 153 mm | 121.5 mm |

### MATLAB Visualization

```matlab
% Import the data
data = readtable('tip_positions.csv');

% Extract coordinates
x = data.X;
y = data.Y;
z = data.Z;

% Plot the 3D trajectory
figure;
plot3(x, y, z, 'b-', 'LineWidth', 2);
grid on;
xlabel('X (mm)');
ylabel('Y (mm)');
zlabel('Z (mm)');
title('CTR Tip Trajectory');
```

---

## 🫀 Tissue Interaction

### Elastic Object Configuration

The liver mesh is converted to a volumetric mesh using CGAL's `MeshGenerationFromPolyhedron`:

```python
liver.addObject('MeshGenerationFromPolyhedron', 
    name="tetraGenerator",
    inputPoints="@liverLoader.position",
    inputTriangles="@liverLoader.triangles",
    drawTetras="1",
    facetSize="10",
    cellSize="10")
```

### Stiffness Cases

| Case | Young's Modulus | Description |
|------|-----------------|-------------|
| **Stiff Object** | 50e6 Pa | Rigid tissue simulation |
| **Soft Object** | 2e3 Pa | Soft tissue (e.g., liver) |

### Target Force Achievement

To achieve the target contact force of **0.3 N**, the following parameters were tuned:

- **Medium tube radius**: 0.80 mm (-0.05 mm from nominal)
- **Medium tube mass density**: 8000 kg/m³ (+1550 from nominal)

**Result**: Contact force magnitude of **0.3071 N** ✓

---

## 📈 Results

### Force Registration Output

```
Contact force at point 0: [-0.2798, 0.1254, -0.0158], Magnitude: 0.3071 N
```

### Key Findings

1. **Workspace Analysis**: Tube length variations of ±10% significantly affect reachable workspace
2. **Tissue Interaction**: CTR successfully navigates and contacts elastic liver model
3. **Force Control**: Target force of 0.3 N achieved through medium tube parameter modification
4. **Real-time Control**: Keyboard controller enables intuitive manipulation of all three tubes

### Performance Metrics

| Metric | Value |
|--------|-------|
| Simulation FPS | ~60 FPS |
| Force Registration Accuracy | ±0.001 N |
| Position Tracking Resolution | 0.001 mm |

---

## 👥 Authors

| Name | Role |
|------|------|
| **Serena Catapano** | Team Member |
| **Emanuele Gaudino** | Team Member |
| **Paola Percuoco** | Team Member |
| **Emanuela Varone** | Team Member |

**Professor**: Fanny Ficuciello

**Course**: Medical Robotics - Technical Project  
**Institution**: Università degli Studi di Napoli Federico II  
**Laboratory**: PRISMA Lab  
**Group**: 3

---

## 📚 References

1. SOFA Framework Documentation - [sofa-framework.org](https://www.sofa-framework.org/)
2. BeamAdapter Plugin - [GitHub](https://github.com/sofa-framework/BeamAdapter)
3. Webster, R.J., & Jones, B.A. (2010). *Design and Kinematic Modeling of Constant Curvature Continuum Robots: A Review*. International Journal of Robotics Research.
4. Dupont, P.E., et al. (2010). *Design and Control of Concentric-Tube Robots*. IEEE Transactions on Robotics.

---

## 📄 License

This project is developed for academic purposes as part of the Medical Robotics course at Università degli Studi di Napoli Federico II.

---

<div align="center">

**⭐ If you find this project useful, please consider giving it a star! ⭐**

*For questions or collaborations, feel free to open an issue.*

</div>
