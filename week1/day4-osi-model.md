# Week 1 Day 4 - OSI Model

## The 7 layers (bottom to top)
1. Physical - cables, wireless signals, hardware
2. Data Link - MAC addresses, switches, frames
3. Network - IP addresses, routers, packets
4. Transport - TCP/UDP, ports, reliable delivery
5. Session - establishing and managing connections
6. Presentation - encryption/decryption, data formatting (TLS lives here)
7. Application - HTTP, DNS, FTP, what users interact with

## Mnemonic (bottom to top)
Please Do Not Throw Sausage Pizza Away

## Security attacks by layer
- Layer 1 Physical: cable tapping, signal jamming
- Layer 2 Data Link: ARP spoofing, MAC flooding
- Layer 3 Network: IP spoofing, routing attacks
- Layer 4 Transport: SYN flood, port scanning
- Layer 5 Session: session hijacking, cookie theft
- Layer 6 Presentation: SSL stripping, MitM via missing encryption
- Layer 7 Application: SQL injection, XSS, phishing

## HTTP vs HTTPS
- HTTP = unencrypted, Layer 6 (Presentation) has no protection
- HTTPS = TLS encryption at Layer 6 wraps Layer 7 conversation
- MitM attacker on same network can read all HTTP traffic in plain text
- PCI-DSS requires encryption of cardholder data in transit - HTTP violates this

## curl -v http://example.com output mapped to layers
- IPv4: 104.20.23.154 = Layer 3 (Network) - IP address resolution
- Trying 104.20.23.154:80 = Layer 4 (Transport) - TCP connection on port 80
- GET / HTTP/1.1 = Layer 7 (Application) - HTTP request
- HTTP/1.1 200 OK = Layer 7 (Application) - HTTP response
- Layers 1,2,5,6 operate invisibly underneath

## Finance background link
- HTTP on a payment page = mailing bank details on a postcard
- PCI-DSS requires HTTPS for all cardholder data transmission
- MitM attack = intercepting a financial message in transit
- TLS certificate = digital equivalent of a tamper-evident seal
