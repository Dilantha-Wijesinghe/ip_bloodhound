# IP Port Scanner

A fast, multi-threaded TCP port scanner written in Rust for network reconnaissance and security testing.

## Features

- **Multi-threaded scanning**: Configurable thread count for optimal performance
- **Full port range**: Scans all TCP ports (1-65535)
- **IPv4 and IPv6 support**: Compatible with both IP address formats
- **Real-time feedback**: Visual progress indicators during scanning
- **Clean output**: Sorted list of open ports after completion

## Installation

### Prerequisites
- Rust and Cargo installed ([Install Rust](https://rustup.rs/))

### Build from source
```bash
git clone https://github.com/Dilantha-Wijesinghe/ip_sniffer.git
cd ip_sniffer
cargo build --release
```

## Usage

### Basic Commands

```bash
# Build the project
cargo build

# Quick syntax check
cargo check

# Run with default settings (4 threads)
cargo run -- <ip_address>

# Run with custom thread count
cargo run -- -j <thread_count> <ip_address>

# Show help
cargo run -- -h
```

### Examples

```bash
# Scan localhost with default 4 threads
cargo run -- 127.0.0.1

# Scan remote IP with 8 threads
cargo run -- -j 8 192.168.1.1

# Show help message
cargo run -- -h
```

## How It Works

The scanner uses a multi-threaded approach to efficiently scan all 65,535 TCP ports:

1. **Thread Distribution**: Each thread scans every nth port (where n = thread count)
   - Thread 1: ports 1, 5, 9, 13...
   - Thread 2: ports 2, 6, 10, 14...
   - Thread 3: ports 3, 7, 11, 15...
   - And so on...

2. **Connection Testing**: Attempts TCP connections to each port
3. **Result Collection**: Uses channels to safely collect results from all threads
4. **Output**: Displays open ports in sorted order

## Performance

- **Default threads**: 4 (balanced performance)
- **Scan time**: Varies by target (localhost: seconds, remote: minutes)
- **Progress indicator**: Dots printed for each open port found

## Security Considerations

⚠️ **Important**: This tool is intended for authorized network security testing only.

- Only scan networks and systems you own or have explicit permission to test
- Unauthorized port scanning may violate laws and policies
- Some networks may detect and log scanning activity
- Use responsibly and ethically

## Development

### Code Structure

- `src/main.rs`: Main application logic
- `Arguments` struct: Command-line argument parsing
- `scan()` function: Core port scanning logic
- Multi-threaded architecture with mpsc channels

### Development Commands

```bash
# Format code
cargo fmt

# Run linter
cargo clippy

# Run tests (when available)
cargo test
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Run `cargo fmt` and `cargo clippy`
5. Submit a pull request

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Disclaimer

This software is provided for educational and authorized testing purposes only. Users are responsible for ensuring compliance with applicable laws and regulations.
