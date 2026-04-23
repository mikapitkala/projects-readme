# 🚆 Stations Pathfinder

**Stations Pathfinder** is a terminal-based Go application that simulates trains moving through a network of stations. It supports intelligent path planning, conflict-free concurrent train movement, and test-driven simulation validation. Designed for correctness, scale, and clarity — even with up to 10,000 stations and trains.

---

## 📦 Features

- 🗺️ Load custom station networks from structured `.txt` files
- 🚄 Compute multiple disjoint paths between start and end stations
- 🔁 Simulate train movements turn-by-turn with conflict rules:
  - One train per station per turn (except start/end)
  - No repeated track usage in a turn
  - Each train moves once per turn
- 🧪 Extensive test suite with manual and Go test modes
- ⚡ Efficient simulation engine — handles up to **10,000 stations and 10,000 trains**
- 🎥 **Visual simulation** in the terminal: see how trains move turn by turn with colored output
- 📦 Automatically saves oversized results in compressed format (gzip)

---

## 📁 Folder Structure

```
stations-pathfinder/
├── cmd/
│   └── stations/        # Main entrypoint
├── internal/
│   ├── algorithms/      # Pathfinding & deduplication
│   ├── color/           # All the pretty colors
│   ├── fileio/          # File parsing and io
│   ├── graph/           # Network loading & structure
│   ├── grid/            # Visualizer
│   ├── planner/         # Train simulation engine
│   └── helpers/         # utils
├── network_maps/        # Input map files
├── scripts/             # Helper scripts (see below)
├── test/                # Go tests & descriptions
├── go.mod
└── README.md
```

---

## 🚀 Usage

### Run a simulation manually

```bash
go run cmd/stations/main.go <map> <start> <end> <num_trains>
```

Example:

```bash
go run cmd/stations/main.go network_maps/01_london.txt waterloo st_pancras 3
```

---

## 🛠️ Development & Testing Tools

Inside the `scripts/` folder:

### ✅ `gorun`

> Quickly run a predefined simulation without retyping arguments.

```bash
./scripts/gorun
```

Edit variables in the script to change the map, stations, or number of trains. Useful for debugging or testing specific networks.

---

### ✅ `goTests`

> Wrapper around `go test` to run all or individual tests.

```bash
./scripts/goTests         # Run all Go test functions
./scripts/goTests 3       # Run only test index 3
```

This uses Go’s testing framework and allows precise test selection based on index.

---

### ✅ `testScript.sh`

> Simulates how a user might interact with the program.  
> Each test has a description, input scenario, and expected behavior.

```bash
./scripts/testScript.sh        # Run all tests interactively
./scripts/testScript.sh 9      # Run only Question 9
```

Includes:
- Skip logic for specific questions
- Descriptive prompts and test guidance
- ✅/❌ results based on expected exit codes
- Safe detection and normalization of working directory

> You may need to add execute permission to run the script on your machine.
```bash
chmod +x testScript.sh
```

---

## 💡 Advanced Capabilities

- ⚙️ **Simulation scalability** — fully optimized for large maps up to **10,000 stations**
- 🎬 **Train movement visualizer** — styled terminal output shows train positions and transitions per turn
- 🧠 **Selective test execution** — run only the test you're interested in
- 📁 **Compressed output support** — large results saved efficiently using gzip (if threshold exceeded)

---

## 👨‍💻 Developed By

- **Pavel Aleksandrov**  
- **Mika Pitkälä**
