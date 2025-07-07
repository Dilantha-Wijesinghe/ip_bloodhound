# IP Port Scanner

A fast, async TCP port scanner written in Rust for network reconnaissance and security testing.

## Features

- **Async concurrent scanning**: Uses Tokio for high-performance async operations
- **Customizable port range**: Scan specific port ranges or full range (1-65535)
- **Flexible addressing**: Support for IPv4 and IPv6 addresses with fallback to localhost
- **Real-time feedback**: Visual progress indicators during scanning
- **Clean output**: Sorted list of open ports after completion

## Installation

### Prerequisites
- Rust and Cargo installed ([Install Rust](https://rustup.rs/))

### Build from source
```bash
git clone https://github.com/Dilantha-Wijesinghe/ip_bloodhound.git
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

# Run with default settings (full port range on localhost)
cargo run

# Scan specific IP address
cargo run -- -a <ip_address>

# Scan with custom port range
cargo run -- -s <start_port> -e <end_port> <ip_address>

# Show help
cargo run -- -h
```

### Examples

```bash
# Scan localhost (default behavior)
cargo run

# Scan specific IP address
cargo run -- -a 192.168.1.1

# Scan specific port range on localhost
cargo run -- -s 80 -e 443

# Scan custom range on remote IP
cargo run -- -a 192.168.1.1 -s 20 -e 25

# Show help message
cargo run -- -h
```

## How It Works

The scanner uses an async concurrent approach built on Tokio:

1. **Task Spawning**: Each port gets its own async task using `tokio::task::spawn`
2. **Connection Testing**: Attempts TCP connections to each port concurrently
3. **Result Collection**: Uses mpsc channels to safely collect results from all tasks
4. **Output**: Displays open ports in sorted order

## Command Line Options

- `-a, --address <ADDRESS>`: IP address to scan (defaults to 127.0.0.1)
- `-s, --start <PORT>`: Starting port number (defaults to 1, must be > 0)
- `-e, --end <PORT>`: Ending port number (defaults to 65535, must be ≤ 65535)
- `-h, --help`: Show help information

## Performance

- **Concurrency**: Each port scanned in its own async task
- **Scan time**: Varies by target and port range (localhost: seconds, remote: minutes)
- **Progress indicator**: Dots printed for each open port found
- **Memory efficient**: Uses async tasks instead of OS threads

## Security Considerations

⚠️ **Important**: This tool is intended for authorized network security testing only.

- Only scan networks and systems you own or have explicit permission to test
- Unauthorized port scanning may violate laws and policies
- Some networks may detect and log scanning activity
- Use responsibly and ethically

## Development

### Code Structure

- `src/main.rs`: Main application logic
- `Arguments` struct: Command-line argument parsing using `bpaf`
- `scan()` function: Core async port scanning logic
- Async architecture with Tokio runtime and mpsc channels

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
