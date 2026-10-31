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



## Task 5: HTTP Status Codes and Troubleshooting

### HTTP Status Codes

| Status Code | Meaning |
|---|---|
| 200 | OK — Request succeeded. |
| 301 | Moved Permanently — Resource has moved to another URL. |
| 403 | Forbidden — Access is denied. |
| 404 | Not Found — Requested resource does not exist. |
| 500 | Internal Server Error — Something went wrong on the server. |

### Types of Network and HTTP Problems

- **DNS failure:** The domain name cannot be resolved into an IP address.
- **Connection timeout:** The computer cannot connect to the server within the expected time.
- **TLS certificate error:** The browser cannot verify the server's security certificate.
- **HTTP error response:** The server receives the request but responds with an HTTP error status.

### Key Difference

DNS failures happen before the computer can locate the server using its domain name. Connection and TLS errors happen during the connection process. HTTP errors happen after the server has received and processed the request.


## Task 6: AWS IAM Policy

Created `s3-read-policy.json` to allow reading objects from a specific S3 bucket.

### Policy Questions

1. **Which field defines the allowed action?**  
   The `Action` field defines the permission which is `s3:GetObject`.

2. **Which field defines the resource?**  
   The `Resource` field specifies the S3 objects inside `example-bucket`.

3. **Does this policy allow listing bucket contents?**  
   No. It does not include `s3:ListBucket`.

4. **Why is a narrow permission safer than `s3:*`?**  
   It follows the principle of least privilege by granting only the permissions required.

5. **Why should AWS access keys never be committed to GitHub?**  
   Access keys are sensitive credentials. Exposing them could allow unauthorized access to AWS resources.
