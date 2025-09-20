# Week 0 — Environment Setup and Tool Installation

This folder presents a clean setup of the open‑source RTL→GDSII toolchain on Ubuntu, including VM guidance, installation steps, and verification snippets.

---

## ✅ Week 0 Tasks

- [x] Create GitHub repo and Week‑wise structure  
- [x] Install and verify tools (Yosys, Icarus Verilog, GTKWave, Magic, NGSpice, Docker, OpenLane; OpenSTA optional)  
- [x] Capture version screenshots and store under Week0/screenshots

---

## 🖥️ Recommended Setup Path

1) Install VirtualBox (if using a VM)  
2) Create Ubuntu 20.04+ VM with required resources  
3) Update OS and base packages  
4) Install simulation tools (Icarus Verilog, GTKWave)  
5) Build synthesis tools (Yosys)  
6) Install layout/verification tools (Magic; OpenSTA optional)  
7) Install Docker and configure user group  
8) Install OpenLane (fetch PDKs; run make test)  
9) Verify each tool and capture screenshots

---

## 💽 Virtual Machine: Step‑by‑Step

- Download and install VirtualBox (Windows/macOS/Linux):
  - https://www.virtualbox.org/wiki/Downloads

- Create a new VM:
  - Name: Ubuntu‑EDA  
  - Type: Linux; Version: Ubuntu 64‑bit  
  - Memory: 6 GB (minimum), prefer 8 GB if available  
  - CPUs: 4 vCPU  
  - Disk: 50 GB VDI, dynamically allocated

- Install Ubuntu 20.04+ ISO:
  - Attach ISO in VM “Storage” → IDE Controller → choose disk → start VM  
  - Follow Ubuntu installer steps; enable third‑party drivers if offered

- Post‑install in the VM:
  - Update packages:
    ```
    sudo apt-get update && sudo apt-get upgrade -y
    ```
  - Install essentials:
    ```
    sudo apt-get install -y build-essential git curl make python3 python3-venv python3-pip
    ```

Tip: If not using a VM, apply all steps directly on a native Ubuntu machine.

---

## 🧰 Tools: What Each One Does (Brief)

- **Yosys** → Open-source logic synthesis  
  Converts Verilog RTL to gate-level netlists, maps to standard-cell libraries via Liberty (.lib), and integrates ABC for technology mapping. 

- **Icarus Verilog (iverilog + vvp)** → Verilog compiler & simulation runtime  
  Used for pre-synthesis functional verification; often paired with **GTKWave** for waveform inspection. 

- **GTKWave** → Waveform viewer  
  Displays `.vcd` or `.fst` simulation outputs to inspect signal activity.

- **Magic** → Layout editor & DRC engine  
  Used for physical verification, interactive layout editing, and basic design rule checks. 

- **OpenSTA (optional)** → Static Timing Analysis  
  Performs setup/hold checks using Liberty models; part of open-source digital flows. 

- **NGSpice** → SPICE simulator  
  For analog/mixed-signal experiments and device-level circuit analysis. 

- **Docker** → Container runtime  
  Orchestrates OpenLane flow and provides reproducible PDK/tool environments. 

- **OpenLane** → Automated RTL → GDSII flow  
  Integrates multiple tools: **Yosys** (synthesis), **OpenROAD** (floorplan/CTS/PnR), **Magic/Netgen** (DRC/LVS), **KLayout** (view), and more.


---

## 📦 Installation — Step‑by‑Step

Run these inside Ubuntu (VM or native). Use sudo privileges.

### 1) Simulation stack (Icarus Verilog + GTKWave)

```
sudo apt-get update
sudo apt-get install -y iverilog gtkwave
```

Quick check:
```
iverilog -V
gtkwave --version
```

### 2) Yosys (build from source)

```
sudo apt install yosys
```

Quick check:
```
yosys -V
```

### 3) NGSpice

```
sudo apt update
sudo apt install -y ngspice
```

Quick check:
```
ngspice -v
```

### 4) Magic VLSI

Prerequisites:
```
sudo apt-get install -y m4 tcsh csh libx11-dev tcl-dev tk-dev \
  libcairo2-dev mesa-common-dev libglu1-mesa-dev libncurses-dev
```

Build and install:
```
git clone https://github.com/RTimothyEdwards/magic
cd magic
./configure
make
sudo make install
magic -version
```

### 5) OpenSTA (optional for SFAL)

Reference build:
- https://github.com/The-OpenROAD-Project/OpenSTA

If installed:
```
sta -version
```

### 6) Docker (required for OpenLane)

```
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
  sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io

sudo docker run hello-world

sudo groupadd docker || true
sudo usermod -aG docker $USER
# Reboot or log out/in for group changes to take effect
```

After reboot:
```
docker run --rm hello-world
docker --version
```

### 7) OpenLane (flow + PDKs)

```
cd $HOME
git clone https://github.com/The-OpenROAD-Project/OpenLane
cd OpenLane
make
make test
```

Checks:
```
git --version
docker --version
python3 --version
python3 -m pip --version
make --version
python3 -m venv -h
```

## 🔍 Quick Verification Samples

- Icarus Verilog minimal run:
  ```
  echo 'module m; initial $display("iverilog_ok"); endmodule' > t.v
  iverilog t.v && ./a.out
  ```
- Yosys help:
  ```
  yosys -Q -p "help"
  ```
- Magic headless ping:
  ```
  magic -dnull -noconsole << EOF
  quit
  EOF
  ```
- Docker hello world:
  ```
  docker run --rm hello-world
  ```
- OpenLane self‑test:
  ```
  cd ~/OpenLane && make test
  ```

---

## 🗂️ Week 0 Folder Structure

```
Week0/
├── README.md
├── screenshots/
│   ├── yosys_version.png
│   ├── iverilog_ok.png
│   ├── gtkwave_version.png
│   ├── magic_version.png
│   ├── docker_hello_world.png
│   └── openlane_make_test.png
└── logs/
    ├── yosys_install.log
    ├── openlane_make.log
    └── openlane_make_test.log
```

- Save terminal outputs under logs/ for traceability.  
- Paste version screenshots under screenshots/.

---

## ⚠️ Troubleshooting Notes

- Docker permission denied: ensure group membership took effect (reboot). [web:47]  
- OpenLane “make test” network failures: retry on stable network; ensure >30 GB free space. [web:157]  
- Magic configure errors: verify all X11/Tcl/Tk/graphics dependencies are installed. [web:157]

---
```
