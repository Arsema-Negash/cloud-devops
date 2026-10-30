## Task 1: Network Information

- **Operating system:** Windows 10
- **IPv4 address:** Private IPv4 address identified locally; exact address withheld for privacy.
- **Default gateway:** Identified locally; exact address withheld for privacy.
- **Address classification:** Private IPv4 address (if confirmed from the ranges above).
- **Command used:** `ipconfig`

## Task 2: Practice Subnetting

### Starting Network
`10.0.0.0/24`

The starting network was provided in the lab instructions.

### Subnetting Calculations

1. An IPv4 address contains 32 bits.
2. The original prefix is `/24` that means 24 bits are used for the network and 8 bits remain for hosts.
3. We need 4 equal-sized subnets.
4. To calculate the required borrowed bits:

   `2^2 = 4 subnets`

5. Borrowing 2 bits from the host portion gives us a new prefix:

   `24 + 2 = /26`

### Why the Subnet Mask Is 255.255.255.192

The original `/24` subnet mask is:

`255.255.255.0`

In binary:

`11111111.11111111.11111111.00000000`

After borrowing 2 bits, the new `/26` subnet mask becomes:

`11111111.11111111.11111111.11000000`

Converting the last octet to decimal:

`128 + 64 = 192`

Therefore, the new subnet mask is:

`255.255.255.192`

### Addresses Per Subnet

Each IPv4 address contains 32 bits. With a `/26` prefix, 6 bits remain for host addresses.

Total addresses per subnet:

`2^(32-26) = 2^6 = 64`

The conventional usable host addresses are:

`64 - 2 = 62`

Under standard AWS IPv4 subnet rules, AWS reserves 5 addresses per subnet:

`64 - 5 = 59 usable addresses`

### Four Equal-Sized Subnets

| Subnet | CIDR | Network Address | Full Address Range | Conventional Usable Host Range | Broadcast Address | AWS Usable Addresses |
|---|---|---|---|---|---|---|
| 1 | `10.0.0.0/26` | `10.0.0.0` | `10.0.0.0 - 10.0.0.63` | `10.0.0.1 - 10.0.0.62` | `10.0.0.63` | 59 |
| 2 | `10.0.0.64/26` | `10.0.0.64` | `10.0.0.64 - 10.0.0.127` | `10.0.0.65 - 10.0.0.126` | `10.0.0.127` | 59 |
| 3 | `10.0.0.128/26` | `10.0.0.128` | `10.0.0.128 - 10.0.0.191` | `10.0.0.129 - 10.0.0.190` | `10.0.0.191` | 59 |
| 4 | `10.0.0.192/26` | `10.0.0.192` | `10.0.0.192 - 10.0.0.255` | `10.0.0.193 - 10.0.0.254` | `10.0.0.255` | 59 |

### Conclusion

The original `10.0.0.0/24` network was divided into four equal-sized `/26` subnets by borrowing 2 host bits.

Each subnet contains 64 total IPv4 addresses, 62 conventionally usable host addresses, and 59 usable addresses under standard AWS subnet rules.


## Task 3: Test DNS Resolution

### Domain Tested
`example.com`

### Command Used
```bash
getent hosts example.com
```

### Results
- **DNS resolution:** Successful


## Task 4: Inspect an HTTPS Website

### Website Tested
`https://example.com`

### Command Used
```bash
curl -I https://example.com
```

### Results
- **Website loaded successfully:** Yes
- **HTTP status code:** [HTTP/1.1]
- **Protocol version:** [200]

### What HTTPS Adds to HTTP
HTTPS uses TLS encryption to protect communication between a browser and a web server. It also provides server authentication and helps protect data from interception or modification.

### Why DNS Resolution Alone Is Not Enough
DNS only translates a domain name into an IP address. A successful website connection also requires network connectivity, a successful TLS handshake for HTTPS, and a working web server that can return an HTTP response.
- **IP address returned:** [140.32.182.253]

### What DNS Does
DNS (Domain Name System) translates human-readable domain names into IP addresses so computers can locate and communicate with websites and other network services.

