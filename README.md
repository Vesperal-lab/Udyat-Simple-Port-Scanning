## Changelog

### v1.2
- Added START/END port validation
- Added /16 network warning
- Added confirmation before scanning /16
- Improved cancellation handling
- Improved invalid option handling
- Logo updated
- CIDR suport

Udyat Simple Port Scanning

A simple TCP port scanner written in pure Bash, using the shell's built-in /dev/tcp pseudo-device to test connections without relying on external tools like nmap or nc.

This project was built as a learning exercise in networking fundamentals and beginner-level penetration testing.

Features
Pure Bash implementation, no external dependencies required
Scans a range of TCP ports on a given host
Uses connection timeouts to avoid hanging on filtered ports
Simple, readable output showing which ports are open
Requirements
Bash (this script relies on the /dev/tcp feature, which is not available in sh/dash or other POSIX-only shells)
A Unix-like environment (Linux, macOS, WSL)
Usage:

chmod +x Udyat
./Udyat <target_host> <start_port> <end_port>

Example:

./Udyat 127.0.0.1 1 1000

Output:

SCANNING 127.0.0.1 FROM 1 UNTIL 1000
PORT 22: OPEN
PORT 80: OPEN
__________________SCAN FINISHED____________________
How it works

Bash provides a special pseudo-device path, /dev/tcp/HOST/PORT, which internally opens a TCP connection when read from or written to. This script loops through a range of ports and attempts to open a connection to each one:

If the connection succeeds, the port is reported as open.
If the connection fails or times out, nothing is reported.

A timeout wrapper is used around each connection attempt to prevent the script from hanging on ports that are filtered by a firewall (which neither accept nor actively refuse the connection).

Disclaimer

This tool is intended for educational purposes and authorized security testing only. Only scan hosts and networks you own or have explicit permission to test. Unauthorized port scanning of systems you do not own may be illegal depending on your jurisdiction.
