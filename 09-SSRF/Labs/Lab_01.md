
# Lab-01 SSRF

## Basic SSRF against the local server

### Problem

- This lab has a stock check feature which fetches data from an internal system.
- To solve the lab, change the stock check URL to access the `admin` interface at `http://localhost/admin` and delete the user `carlos`.


### Solution

- Connect To burp suite. After that you can go to any images and Click the View details and check the stock.

- After connect with burp, send the stockcheck Request to repeter.

- In Repeter Change the request `stockApi=http%3A%2F%2Fstock.weliketoshop.net%3A8080%2Fproduct%2Fstock%2Fcheck%3FproductId%3D1%26storeId%3D1` To this `stockApi=http%3A%2F%2Flocalhost/admin` The server send 200 response and you can search 
for Carlos 

- After Find the path you can delete the Carlos user `stockApi=http://localhost/admin/delete?username=carlos`

- Lab solved !!!
