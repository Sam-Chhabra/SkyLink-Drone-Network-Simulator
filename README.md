# 🚁 SkyLink – Distributed Drone Network Simulator

SkyLink is a distributed drone network simulation written in Rust.  
It models a network of drones, clients, and servers communicating through unreliable links using custom protocols, source routing, and concurrent message passing.

Developed as part of the **Advanced Programming 2024/2025 course project**.

---

## 📌 Overview

SkyLink simulates a real-world drone communication infrastructure where:

- Drones act as routing nodes
- Clients and servers operate at the network edges
- Communication is unreliable (packet drops & crashes)
- Nodes use source routing instead of routing tables
- Packets may be fragmented and reassembled
- The network topology can change at runtime

The system guarantees eventual packet delivery despite unreliable links.

---

## 🧠 System Architecture

The network consists of:

### 🚁 Drones (Routing Nodes)
- Forward packets between clients and servers
- May drop packets (Packet Drop Probability)
- May crash during simulation
- Do NOT maintain routing tables
- Run on independent Rust threads

### 🖥 Servers
Two types:
- **Content Servers**
  - Text Server
  - Media Server
- **Communication Servers**
  - Client registration
  - Message forwarding
  - Client list retrieval

Each server connects to at least two drones for redundancy.

### 💬 Clients
Two types:
- **Web Browser**
  - Retrieves text files and related media
- **Chat Client**
  - Registers to communication server
  - Sends messages to other clients

Each client connects to at most two drones.

### 🎛 Simulation Controller
- Dynamically modifies network topology
- Can:
  - Crash drones
  - Add/remove neighbors
  - Change packet drop probability
- Visualizes:
  - Nodes and connections
  - Packet transmissions
  - Dropped packets
  - Crash events

---

## 🔄 Communication Model

- Bidirectional communication
- Implemented using `crossbeam` channels
- Each node runs in its own Rust thread
- Nodes listen to:
  - Packet channel
  - Simulation command channel
- Uses `select!` macro for multi-channel handling

---

## 🌐 Source Routing

SkyLink implements **source routing**:

- Clients and servers determine packet paths
- Drones do not store routing tables
- Network Discovery Protocol is used to:
  - Discover topology
  - Adapt to crashes
  - Update routing paths

---

## 📦 Packet Handling

Two levels of packets:

### High-Level Packets
- Client-server messages
- File requests
- Chat messages

### Low-Level Packets (Fragments)
- Serialized messages
- Fragmented if exceeding max size
- Sequenced and reassembled at destination

The system handles:
- Lost packets
- Lost acknowledgements
- Drone crashes
- Eventual delivery guarantees

---

## ⚙ Technical Features

- Multi-threaded distributed architecture
- Crossbeam channels
- Custom protocol implementation
- Packet serialization
- Fragmentation & reassembly
- Crash simulation
- Dynamic topology updates
- Event monitoring system
- No unsafe Rust
- Clippy-clean and idiomatic code

---

## 🛠 Technologies

- Rust
- Crossbeam channels
- Multi-threading
- Custom networking protocols
- Cargo build system

---

## 🚀 Running the Project

Clone the repository:

# 🚁 SkyLink – Distributed Drone Network Simulator

SkyLink is a distributed drone network simulation written in Rust.  
It models a network of drones, clients, and servers communicating through unreliable links using custom protocols, source routing, and concurrent message passing.

Developed as part of the **Advanced Programming 2024/2025 course project**.

---

## 📌 Overview

SkyLink simulates a real-world drone communication infrastructure where:

- Drones act as routing nodes
- Clients and servers operate at the network edges
- Communication is unreliable (packet drops & crashes)
- Nodes use source routing instead of routing tables
- Packets may be fragmented and reassembled
- The network topology can change at runtime

The system guarantees eventual packet delivery despite unreliable links.

---

## 🧠 System Architecture

The network consists of:

### 🚁 Drones (Routing Nodes)
- Forward packets between clients and servers
- May drop packets (Packet Drop Probability)
- May crash during simulation
- Do NOT maintain routing tables
- Run on independent Rust threads

### 🖥 Servers
Two types:
- **Content Servers**
  - Text Server
  - Media Server
- **Communication Servers**
  - Client registration
  - Message forwarding
  - Client list retrieval

Each server connects to at least two drones for redundancy.

### 💬 Clients
Two types:
- **Web Browser**
  - Retrieves text files and related media
- **Chat Client**
  - Registers to communication server
  - Sends messages to other clients

Each client connects to at most two drones.

### 🎛 Simulation Controller
- Dynamically modifies network topology
- Can:
  - Crash drones
  - Add/remove neighbors
  - Change packet drop probability
- Visualizes:
  - Nodes and connections
  - Packet transmissions
  - Dropped packets
  - Crash events

---

## 🔄 Communication Model

- Bidirectional communication
- Implemented using `crossbeam` channels
- Each node runs in its own Rust thread
- Nodes listen to:
  - Packet channel
  - Simulation command channel
- Uses `select!` macro for multi-channel handling

---

## 🌐 Source Routing

SkyLink implements **source routing**:

- Clients and servers determine packet paths
- Drones do not store routing tables
- Network Discovery Protocol is used to:
  - Discover topology
  - Adapt to crashes
  - Update routing paths

---

## 📦 Packet Handling

Two levels of packets:

### High-Level Packets
- Client-server messages
- File requests
- Chat messages

### Low-Level Packets (Fragments)
- Serialized messages
- Fragmented if exceeding max size
- Sequenced and reassembled at destination

The system handles:
- Lost packets
- Lost acknowledgements
- Drone crashes
- Eventual delivery guarantees

---

## ⚙ Technical Features

- Multi-threaded distributed architecture
- Crossbeam channels
- Custom protocol implementation
- Packet serialization
- Fragmentation & reassembly
- Crash simulation
- Dynamic topology updates
- Event monitoring system
- No unsafe Rust
- Clippy-clean and idiomatic code

---

## 🛠 Technologies

- Rust
- Crossbeam channels
- Multi-threading
- Custom networking protocols
- Cargo build system

---

## 🚀 Running the Project

Clone the repository:

```bash
git clone https://github.com/Sam-Chhabra/SkyLink-Drone-Network-Simulator.git
cd SkyLink-Drone-Network-Simulator
```

Build the project:

```bash
cargo build
```

Run the simulation:

```bash
cargo run
```

Run tests:

```bash
cargo test
```

Format the code:

```bash
cargo fmt
```

---

## 📂 Project Structure

```
.
├── src/
│   ├── clients_gio/         # Client implementation (variant 1)
│   ├── clients_sam/         # Client implementation (variant 2)
│   ├── server/              # Communication & content server logic
│   ├── simulation_control/  # Runtime topology controller
│   ├── test/                # Testing modules
│   ├── initializer.rs       # Network initialization logic
│   ├── main.rs              # Entry point
│   ├── message.rs           # Packet/message definitions
│   ├── network_edge.rs      # Network edge abstraction
│   └── routing.rs           # Source routing logic
│
├── inputs/                  # Simulation configuration files
├── getdroned_logs/          # Runtime logs
├── image.html               # Visualization / UI component
├── Cargo.toml               # Project configuration
├── Cargo.lock               # Dependency lock file
└── README.md
```

---

## 🧪 Reliability Model

The simulation models unreliable networking conditions:

- Per-drone Packet Drop Probability
- Drone crash simulation
- Failure notification messages
- Dynamic network rediscovery
- Runtime topology updates

Despite unreliable links, the system guarantees eventual packet delivery using protocol-level handling of:

- Lost packets
- Lost acknowledgements
- Drone failures
- Network changes

---

## 👥 Contributions

Originally developed as part of a university group project.

This repository contains my maintained and structured version of the system, including:

- Distributed architecture design  
- Protocol implementation  
- Concurrency model using crossbeam channels  
- Packet fragmentation & reassembly logic  
- Simulation controller implementation  

---

## 🏁 Conclusion

SkyLink demonstrates:

- Distributed systems architecture  
- Multi-threaded Rust programming  
- Crossbeam channel-based communication  
- Source routing  
- Packet serialization and fragmentation  
- Fault-tolerant communication handling  
- Dynamic network simulation  

The project models a realistic drone-based communication infrastructure with strong emphasis on correctness, reliability, and concurrency.
