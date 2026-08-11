## Changelog

### v1.3

* Added Banner grabbing
* Added HTTP/HTTPS Status detection
* Added HTTP/HTTPS Server banner detection
* Added `get_status()` function
* Improved output with banner and status information

### v1.2

* Added START/END port validation
* Added /16 network warning
* Added confirmation before scanning /16
* Improved cancellation handling
* Improved invalid option handling
* Logo updated
* CIDR support
* Added IPv4 validation

#### Improved

* Better handling of invalid options during the `/16` confirmation prompt.
* Proper scan cancellation when `N` or an empty input is provided.
* Clearer error messages for invalid input.
* Improved execution flow and input handling.

#### Current Features

* TCP connect scanning using `/dev/tcp`.
* `/24` and `/16` network support.
* Custom starting and ending ports.
* 3-second connection timeout.
* Basic service identification based on port numbers.
* Input validation and error handling.
* Warning before potentially large scans.
* TCP banner grabbing.
* HTTP/HTTPS banner grabbing using `curl`.
* HTTP/HTTPS status detection.

Udyat Simple Port Scanning

A simple TCP port scanner written in pure Bash, using the shell's built-in /dev/tcp pseudo-device to test connections without relying on external tools like nmap or nc.

This project was built as a learning exercise in networking fundamentals and beginner-level penetration testing.


## Limitations

This scanner is not intended to replace Nmap.

It currently performs TCP connect scanning and
does not implement SYN scanning, UDP scanning,
service fingerprinting, or concurrent scanning.

Features
Pure Bash implementation, no external dependencies required
Scans a range of TCP ports on a given host
Uses connection timeouts to avoid hanging on filtered ports
Simple, readable output showing which ports are open
Basic service identification based on port numbers
TCP banner grabbing
HTTP/HTTPS banner and status detection

Requirements
Bash (this script relies on the /dev/tcp feature, which is not available in sh/dash or other POSIX-only shells)
A Unix-like environment (Linux, macOS, WSL)
curl (required for HTTP/HTTPS banner and status grabbing)

Usage:

chmod +x Udyat
./Udyat <target_host> <start_port> <end_port>

Example:

./Udyat 192.xxx.x.x/24 1 100

### Example Output

```text
𓂀 SCANNING 192.xxx.x.x/24 FROM 1 UNTIL 255 𓂀

IP: 192.xxx.x.x PORT 22: OPEN
EXPECTED: SSH
BANNER: SSH-2.0-OpenSSH

IP: 192.xxx.x.x PORT 80: OPEN
EXPECTED: HTTP
BANNER: Server: nginx
STATUS: HTTP/1.1 200 OK

******************SCAN FINISHED******************
```

How it works

Bash provides a special pseudo-device path, /dev/tcp/HOST/PORT, which internally opens a TCP connection when read from or written to. This script loops through a range of ports and attempts to open a connection to each one:

If the connection succeeds, the port is reported as open.
If the connection fails or times out, nothing is reported.

For HTTP and HTTPS ports, Udyat uses curl to retrieve the server banner and HTTP status from the response headers.

For other TCP services, Udyat attempts to read a banner after establishing a connection.

A timeout wrapper is used around each connection attempt to prevent the script from hanging on ports that are filtered by a firewall (which neither accept nor actively refuse the connection).

Disclaimer

This tool is intended for educational purposes and authorized security testing only. Only scan hosts and networks you own or have explicit permission to test. Unauthorized port scanning of systems you do not own may be illegal depending on your jurisdiction.

## What I learned

This project helped me understand:

- TCP connection establishment
- Port states
- Network CIDR notation
- Bash /dev/tcp
- Connection timeouts
- Input validation
- Network scanning limitations

### Roadmap

* [x] Banner grabbing
* [x] HTTP/HTTPS Status detection
* [x] Advanced IPv4 validation
* [ ] Concurrent scanning
* [ ] Improved service detection
* [ ] Result export
