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

Build and install:
```
sudo apt-get install -y m4 tcsh csh libx11-dev tcl-dev tk-dev \
  libcairo2-dev mesa-common-dev libglu1-mesa-dev libncurses-dev

git clone https://github.com/RTimothyEdwards/magic
cd magic
./configure
make
sudo make install
magic -version
cd ..
```

Quick check:
```
magic -dnull -noconsole
version
quit
EOF
```

### 5) OpenSTA 

```
sudo apt-get install -y build-essential libreadline-dev cmake

git clone https://github.com/The-OpenROAD-Project/OpenSTA.git
cd OpenSTA
mkdir build && cd build
cmake ..
make
sudo make install
```

Quick check:
```
sta -version || echo "OpenSTA installed"
cd ../..
```

### 6) Docker (required for OpenLane)

```
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
  sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io

```

Add user to Docker group:
```
sudo groupadd docker || true
sudo usermod -aG docker $USER
# Reboot or log out/in for group changes to take effect
```

After reboot, verify Docker:
```
docker run --rm hello-world
docker --version
```

### 7) OpenLane (RTL → GDSII flow)

```
cd $HOME
git clone https://github.com/The-OpenROAD-Project/OpenLane.git
cd OpenLane
```

Set up Python environment
```
python3 -m venv ./venv
source ./venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

Install PDKs and run basic tests
```
make pdk
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

- Icarus Verilog run
  ```
  echo 'module m; initial $display("iverilog_ok"); endmodule' > t.v
  iverilog t.v -o t.out && ./t.out
  ```
- GTKWave simple waveform
  ```
  # Create a small test VCD for GTKWave
  echo 'module test; reg clk; initial clk = 0; always #5 clk = ~clk; initial #20 $finish; endmodule' > test.v
  iverilog -o test.vvp test.v
  vvp test.vvp
  # Run GTKWave (GUI will open)
  gtkwave test.vcd &
  ```
- Yosys basic synthesis
  ```
  echo 'module top(input a, b, output y); assign y = a & b; endmodule' > top.v
  yosys -p "read_verilog top.v; synth; stat; show" 
  ```
- NGSpice simple circuit
  ```
  # Create a basic RC circuit netlist
  echo '* RC circuit exampleV1 in 0 DC 5
  R1 in out 1k
  C1 out 0 1u
  .tran 1m 10m
  .control
  run
  plot v(out)
  .quit
  .endc
  .end' > rc_circuit.sp
  ngspice rc_circuit.sp
  ```
- Magic VLSI minimal run
  ```
  # Create a minimal layout file
  echo "box 0 0 10 10" > demo.mag

  # Launch Magic GUI and load the minimal design
  magic demo.mag &
  ```
- Magic VLSI minimal run
  ```
  # Create a simple Liberty file for a single inverter
  echo 'library (simple_lib) {
  cell (inv) {
    pin (A) { direction : input; }
    pin (Y) { direction : output; function : "(!A)"; }
  }
  }' > simple.lib

  # Create a simple Verilog netlist for OpenSTA
  echo 'module top(input A, output Y); inv u1(.A(A), .Y(Y)); endmodule' > top.v

  # Run OpenSTA timing analysis
  sta -lib simple.lib -tcl "read_verilog top.v; link_design top; report_timing; exit"
  ```
- Docker hello world:
  ```
  docker run --rm hello-world
  ```
- OpenLane self‑test:
  ```
  cd ~/OpenLane
  make test
  ```

---

## 🗂️ Week 0 Folder Structure

```
Week0/
├── README.md
├── logs
    ├── yosys_run.log             
    ├── iverilog_run.log         
    ├── opensta_run.log           
    ├── docker_hello_world.log    
    ├── openlane_make.log        
    ├── openlane_make_test.log    
├── screenshots/
    │ ├── gtkwave_waveform.png      
    │ └── magic_demo.png            
└── version_check/
    │ ├── gtkwave_version.md
    │ ├── iverilog_version.md
    │ ├── magic_version.md
    │ ├── ngspice.md
    │ ├── ngspice.md
    │ └── yosys opensta docker_verison.md
```

- Save terminal outputs under `logs/` for traceability.  
- Paste screenshots of actual runs under `screenshots/`.  
---

## ⚠️ Troubleshooting Notes

- **Docker permission denied**: ensure group membership took effect (reboot or log out/in).  
- **OpenLane “make test” failures**: retry on stable network; ensure >30 GB free space.  
- **Magic GUI errors**: verify all X11/Tcl/Tk/graphics dependencies are installed.  
- **OpenSTA errors**: ensure `cmake` and `libreadline-dev` are installed; minimal Liberty/netlist test should pass.  
- **GTKWave issues**: make sure the `.vcd` file is generated and GUI can open it.

---
```
