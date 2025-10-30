# IP Sniffer

A fast, multi-threaded port scanner written in Rust for discovering open TCP ports on target IP addresses.

## Features

- **Multi-threaded scanning**: Configurable number of threads for faster scanning
- **IPv4 and IPv6 support**: Works with both IP address formats
- **TCP port scanning**: Scans all TCP ports (1-65535)
- **Real-time feedback**: Shows scanning progress with dots
- **Sorted results**: Displays open ports in ascending order

## Installation

### Prerequisites

- Rust (1.70 or later)
- Cargo package manager

### Build from source

```bash
git clone <repository-url>
cd ip_sniffer
cargo build --release
```

The compiled binary will be available at `target/release/ip_sniffer`.

## Usage

### Basic Usage

```bash
# Scan an IP address with default settings (4 threads)
ip_sniffer 192.168.1.1

# Scan IPv6 address
ip_sniffer 2001:db8::1
```

### Advanced Usage

```bash
# Specify number of threads for faster scanning
ip_sniffer -j 8 192.168.1.1

# Get help information
ip_sniffer --help
ip_sniffer -h
```

### Command Line Arguments

- `<IP_ADDRESS>`: Target IP address (IPv4 or IPv6) - **Required**
- `-j, --threads <THREADS>`: Number of threads to use (default: 4)
- `-h, --help`: Show help message and usage information
- `-v, --version`: Show version information

### Examples

```bash
# Scan localhost with 4 threads (default)
ip_sniffer 127.0.0.1

# Fast scan with 16 threads
ip_sniffer -j 16 192.168.1.100

# Scan a remote server
ip_sniffer -j 8 example.com
```

## How It Works

The IP sniffer uses a multi-threaded approach to efficiently scan TCP ports:

1. **Thread Distribution**: Divides the port range (1-65535) among the specified number of threads
2. **TCP Connection Attempts**: Each thread attempts to establish TCP connections to assigned ports
3. **Result Collection**: Successfully connected ports are collected and sorted
4. **Output**: Displays all open ports in ascending order

## Performance Considerations

- **Thread Count**: More threads generally mean faster scanning, but too many threads may overwhelm the target or your network
- **Network Limitations**: Scanning speed is limited by network latency and target response time
- **Resource Usage**: Higher thread counts consume more system resources

### Recommended Thread Counts

- **Local Network**: 8-16 threads
- **Remote Hosts**: 4-8 threads
- **Slow Networks**: 2-4 threads

## Output Format

During scanning:
```
......................
```
Each dot represents a successful connection attempt.

Results:
```
[*] 22 is open
[*] 80 is open
[*] 443 is open
```

## License

This project is available under the MIT License. See the LICENSE file for more details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Disclaimer

This tool is intended for educational purposes and legitimate network administration tasks. Always ensure you have proper authorization before scanning networks or systems you do not own.

## Version

Current version: 0.1.0