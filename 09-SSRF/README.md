# Server Side Request Forgery

- Listed under OWASP's A01:2025 - Broken Access Control.
- It's a webapp Vulnerability that allows an attacker cause the Server Side application to make a request to an unintend location.
- In other Cases they may be able to force the server to connect to arbitary External system

## Impact 

- A Success full attack can lead to unauthorized action.
- Some time the attacker might try arbitary command execution

## Common SSRF attack 

-  Against the server itself :  In an ssrf attack against the server,the attacker causes the application to make an http request back to the server that is hosting the application Via its loopback network interface
ex :
`Api=http://stock.weliketoshop.net:8080/product/stock/check%3FproductId%3D6%26storeId%3D1`

in this situation the attacker modifies 
`stockApi=http://localhost/admin`
	
- Against other back -end system : In some cases, the application server is able to interact with back-end systems that are not directly reachable by users. These systems often have non-routable private IP addresses. The back-end systems are normally protected by the network topology, so they often have a weaker security posture.
`ex: stockApi=http://192.168.0.68/admin`

## SSRF – Hidden Attack Surface

1. Partial URLs: User input is used to construct a complete URL.
2. XML Data: XXE in XML can trigger server-side requests.
3. Referer Header: Analytics software may visit URLs from the Referer header.
4. Blind SSRF: The server makes a request, but the response isn't visible.

## How to Prevent SSRF

1. Allowlist trusted URLs and domains.
2. Block localhost, private IPs, and cloud metadata endpoints.
3. Disable external entities in XML parsers.
4. Restrict redirects and outbound network traffic.

# Server Side Request Forgery(SSRF) Labs

## Lab Write-ups

| Lab | Description |
|---|---|
| [Lab 01](./Lab_01.md) | SSRF Lab 01 |
| [Lab 02](./Lab_02.md) | SSRF Lab 02 |
| [Lab 03](./Lab_03.md) | SSRF Lab 03 |
| [Lab 04](./Lab_04.md) | SSRF Lab 04 |
| [Lab 05](./Lab_05.md) | Ssrf Lab 05 |
| [Lab 06](./Lab_06.md) | SSRF Lab 06 |
| [Lab 07](./Lab_07.md) | SSRF Lab 07 |
