# Ultimate System Stress Testing Tools 🚀

A comprehensive collection of the most effective stress testing tools for Linux systems, organized by hardware component. Each tool has been carefully selected for maximum effectiveness, ease of use, and reliability.


## 📋 Table of Contents

- [Overview](#overview)
- [Tools by Component](#tools-by-component)
  - [GPU Testing](#-gpu-testing)
  - [CPU Testing](#-cpu-testing)
  - [Memory Testing](#-memory-testing)
  - [Storage Testing](#-storage-testing)
  - [System Monitoring](#-system-monitoring)
- [All-in-One Solutions](#-all-in-one-solutions)
- [Scripts](#scripts)
- [Installation](#installation)
- [Usage Examples](#usage-examples)
- [Contributing](#contributing)
- [License](#license)

## Overview

This repository contains the ultimate collection of single-tool solutions for stress testing different hardware components. Instead of using multiple tools with varying quality, we've identified the **one best tool** for each category.

## Tools by Component

### 🎮 GPU Testing

**Tool: [gpu-burn](https://github.com/wilicc/gpu-burn)**
- Maximum GPU utilization (99-100%)
- Tests both compute and memory
- Detects unstable overclocks quickly
- Real-time error reporting

```bash
# NVIDIA GPUs
./gpu_burn 600

# AMD GPUs
glmark2 --run-forever
```

### 🧠 CPU Testing

**Tool: [stress-ng](https://github.com/ColinIanKing/stress-ng)**
- 260+ stress testing methods
- Tests all CPU instruction sets
- Comprehensive cache and pipeline stress
- Detailed performance metrics

```bash
# Comprehensive CPU stress
stress-ng --cpu $(nproc) --cpu-method all --metrics --timeout 600s

# Maximum heat generation
stress-ng --matrix $(nproc) --timeout 600s

# Watch on separate terminal
watch -n 1 'sensors | grep -E "Tctl|Tccd1|Tccd2"'
```

### 💾 Memory Testing

**Tool: [memtester](https://pyropus.ca./software/memtester/)**
- Most thorough pattern testing
- Catches subtle memory errors
- Battle-tested reliability
- Clear pass/fail results

```bash
# Test maximum available memory
sudo memtester $(free -m | awk 'NR==2{printf "%dM", $7*0.9}') 5

# Alternative with stress-ng
stress-ng --vm 2 --vm-bytes 90% --vm-method all --verify --timeout 600s
```

### 💿 Storage Testing

**Tool: [fio](https://github.com/axboe/fio)**
- Industry standard benchmarking
- Extremely configurable
- Tests all I/O patterns
- Detailed performance metrics

```bash
# Quick random I/O test
fio --name=test --ioengine=libaio --direct=1 --bs=4k --rw=randrw --size=1G --runtime=600

# Use predefined job file
fio configs/storage-stress.fio
```

### 📊 System Monitoring

**Tool: [glances](https://github.com/nicolargo/glances)**
- All-in-one system monitoring
- GPU monitoring built-in
- Real-time alerts
- Web interface available

```bash
# Terminal interface
glances

# Web interface
glances -w
# Browse to http://localhost:61208
```

## 🔥 All-in-One Solutions

### s-tui - Interactive Stress Testing
Beautiful terminal UI combining stress testing with real-time monitoring.

```bash
# Install and run
sudo apt install -y s-tui stress
s-tui
# Press 's' to start stress test
```

## Scripts

### Additional Scripts

- [`install-dependencies.sh`](scripts/install-dependencies.sh) - Automated tool installation
- [`gpu-test.sh`](scripts/gpu-test.sh) - GPU-specific stress testing
- [`cpu-test.sh`](scripts/cpu-test.sh) - CPU-specific stress testing
- [`memory-test.sh`](scripts/memory-test.sh) - Memory-specific stress testing
- [`storage-test.sh`](scripts/storage-test.sh) - Storage-specific stress testing

## Installation

### Automated Installation

```bash
# Install all dependencies
./install-dependencies.sh

# Install specific components
./install-dependencies.sh --gpu-only
./install-dependencies.sh --cpu-only
```

### Manual Installation

#### Ubuntu/Debian
```bash
sudo apt update
sudo apt install -y stress-ng memtester glances fio s-tui

# For GPU testing
git clone https://github.com/wilicc/gpu-burn
cd gpu-burn && make
```

#### CentOS/RHEL/Fedora
```bash
sudo dnf install -y stress-ng glances fio
# memtester may need to be compiled from source
```

#### Arch Linux
```bash
sudo pacman -S stress-ng glances fio
yay -S memtester s-tui
```

## Usage Examples

### Quick Component Tests

```bash
# Test GPU for 5 minutes
./scripts/gpu-test.sh 300

# Test CPU with all methods
./scripts/cpu-test.sh --method all --duration 600

# Test memory with specific pattern
./scripts/memory-test.sh --size 8G --iterations 3

# Test storage with custom config
./scripts/storage-test.sh --config configs/nvme-test.fio
```

### Advanced Usage

```bash
# Stress test with temperature limits
./scripts/ultimate-stress.sh 3600 --temp-limit 80 --auto-stop

# Export monitoring data
./scripts/ultimate-stress.sh 600 --export-csv results.csv

# Run specific stress patterns
./scripts/ultimate-stress.sh 600 --cpu-method matrix --mem-method all
```

## Configuration Files

Pre-configured test profiles are available in the [`configs/`](configs/) directory:

- `storage-stress.fio` - Comprehensive storage testing
- `memory-patterns.conf` - Memory test configurations
- `gpu-profiles.conf` - GPU stress test profiles
- `monitoring.conf` - System monitoring settings

## Power User Tips

### Maximum Heat Generation
```bash
# CPU: Matrix operations generate most heat
stress-ng --matrix $(nproc) --timeout 600s

# GPU: Maximum power draw
./gpu_burn 600
```

### Stability Testing for Overclocking
```bash
# Long-duration stability test
stress-ng --cpu $(nproc) --cpu-method all --verify --timeout 3600s
```

### Automated Temperature Protection
```bash
# Auto-stop if temperatures exceed limits
./scripts/ultimate-stress.sh 3600 --temp-limit 90 --auto-stop
```

## Quick Reference

| Component | Tool | Quick Command |
|-----------|------|---------------|
| **GPU** | gpu-burn | `./gpu_burn 600` |
| **CPU** | stress-ng | `stress-ng --cpu $(nproc) --cpu-method all --timeout 600s` |
| **Memory** | memtester | `sudo memtester 8G 5` |
| **Storage** | fio | `fio --name=test --ioengine=libaio --direct=1 --bs=4k --rw=randrw --size=1G --runtime=600` |
| **Monitor** | glances | `glances` |
| **All-in-one** | s-tui | `s-tui` |

## Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

### Areas for Contribution
- Additional platform support (macOS, Windows)
- New stress testing tools
- Performance optimizations
- Documentation improvements
- Bug fixes and testing

## Troubleshooting

Common issues and solutions can be found in our [Troubleshooting Guide](TROUBLESHOOTING.md).

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [stress-ng](https://github.com/ColinIanKing/stress-ng) by Colin Ian King
- [gpu-burn](https://github.com/wilicc/gpu-burn) by Ville Timonen
- [glances](https://github.com/nicolargo/glances) by Nicolas Hennion
- [fio](https://github.com/axboe/fio) by Jens Axboe
- [memtester](https://pyropus.ca./software/memtester/) by Charles Cazabon

## Support

If you find this repository helpful, please consider:
- ⭐ Starring the repository
- 🐛 Reporting bugs
- 💡 Suggesting new features
- 📖 Improving documentation

---

**Note**: Always ensure adequate cooling and monitor temperatures when stress testing. The tools in this repository can generate significant heat and power consumption.
