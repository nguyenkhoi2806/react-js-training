# Review last lesson

## Week 7 Exercise

Set up a project using React version 18 or later

**Requirements:**

- ESLint + Prettier + a UI component library (optional)
- Project structure should support reusable basic or feature-based modules
- Layout should follow the design of [this site](https://foreverbuy.in/)
- Assets can be found in the folder: forever-assets.zip
- Logic functions should follow the behavior of [this site](https://foreverbuy.in/)
- APIs can be reused from [this site](https://foreverbuy.in/) or replaced with JSON using localStorage

## Api list

### List product

<https://api.foreverbuy.in/api/product/list>>

### User login

curl '<https://api.foreverbuy.in/api/user/login>' \
 -H 'Accept: application/json, text/plain, _/_' \
 -H 'Accept-Language: en-US,en;q=0.9' \
 -H 'Cache-Control: no-cache' \
 -H 'Connection: keep-alive' \
 -H 'Content-Type: application/json' \
 -H 'Origin: <https://foreverbuy.in>' \
 -H 'Pragma: no-cache' \
 -H 'Referer: <https://foreverbuy.in/>' \
 -H 'Sec-Fetch-Dest: empty' \
 -H 'Sec-Fetch-Mode: cors' \
 -H 'Sec-Fetch-Site: same-site' \
 -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36 Edg/137.0.0.0' \
 -H 'sec-ch-ua: "Microsoft Edge";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
 -H 'sec-ch-ua-mobile: ?0' \
 -H 'sec-ch-ua-platform: "macOS"' \
 --data-raw '{"email":"<abc@gmail.com>","password":"123456"}'

### User register

curl '<https://api.foreverbuy.in/api/user/register>' \
 -H 'Accept: application/json, text/plain, _/_' \
 -H 'Accept-Language: en-US,en;q=0.9' \
 -H 'Cache-Control: no-cache' \
 -H 'Connection: keep-alive' \
 -H 'Content-Type: application/json' \
 -H 'Origin: <https://foreverbuy.in>' \
 -H 'Pragma: no-cache' \
 -H 'Referer: <https://foreverbuy.in/>' \
 -H 'Sec-Fetch-Dest: empty' \
 -H 'Sec-Fetch-Mode: cors' \
 -H 'Sec-Fetch-Site: same-site' \
 -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36 Edg/137.0.0.0' \
 -H 'sec-ch-ua: "Microsoft Edge";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
 -H 'sec-ch-ua-mobile: ?0' \
 -H 'sec-ch-ua-platform: "macOS"' \
 --data-raw '{"name":"khoile","email":"<abc@gmail.com>","password":"123456"}'

### Submit cart

curl '<https://api.foreverbuy.in/api/order/place>' \
 -H 'Accept: application/json, text/plain, _/_' \
 -H 'Accept-Language: en-US,en;q=0.9' \
 -H 'Cache-Control: no-cache' \
 -H 'Connection: keep-alive' \
 -H 'Content-Type: application/json' \
 -H 'Origin: <https://foreverbuy.in>' \
 -H 'Pragma: no-cache' \
 -H 'Referer: <https://foreverbuy.in/>' \
 -H 'Sec-Fetch-Dest: empty' \
 -H 'Sec-Fetch-Mode: cors' \
 -H 'Sec-Fetch-Site: same-site' \
 -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36 Edg/137.0.0.0' \
 -H 'sec-ch-ua: "Microsoft Edge";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
 -H 'sec-ch-ua-mobile: ?0' \
 -H 'sec-ch-ua-platform: "macOS"' \
 -H 'token;' \
 --data-raw '{"address":{"firstName":"Khoi KOREAN","lastName":"Le","email":"<abc@gmail.com>","street":"65 Đường số 30, Linh Đông, trực thuộc, thành phố Thủ Đức, Thành phố Hồ Chí Minh","city":"Ho Chi Minh","state":"21321","zipcode":"700000","country":"Vietnam","phone":"0396159997"},"items":[{"\_id":"6683d5e07f779795ecfa98bd","name":"Men Tapered Fit Flat-Front Trousers","description":"A lightweight, usually knitted, pullover shirt, close-fitting and with a round neckline and short sleeves, worn as an undershirt or outer garment.","price":58,"image":["https://raw.githubusercontent.com/avinashdm/gs-images/main/forever/p_img15.png"],"category":"Men","subCategory":"Bottomwear","sizes":["S","M","L","XL","XXL"],"bestseller":false,"date":1719915311964,"\_\_v":0,"size":"XL","quantity":1}],"amount":68}'

### Login admin

curl '<https://api.foreverbuy.in/api/user/admin>' \
 -H 'Accept: application/json, text/plain, _/_' \
 -H 'Accept-Language: en-US,en;q=0.9' \
 -H 'Cache-Control: no-cache' \
 -H 'Connection: keep-alive' \
 -H 'Content-Type: application/json' \
 -H 'Origin: <https://admin.foreverbuy.in>' \
 -H 'Pragma: no-cache' \
 -H 'Referer: <https://admin.foreverbuy.in/>' \
 -H 'Sec-Fetch-Dest: empty' \
 -H 'Sec-Fetch-Mode: cors' \
 -H 'Sec-Fetch-Site: same-site' \
 -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36 Edg/137.0.0.0' \
 -H 'sec-ch-ua: "Microsoft Edge";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
 -H 'sec-ch-ua-mobile: ?0' \
 -H 'sec-ch-ua-platform: "macOS"' \
 --data-raw '{"email":"<admin@example.com>","password":"greatstack123"}'

### List order

curl '<https://api.foreverbuy.in/api/order/list>' \
 -H 'Accept: application/json, text/plain, _/_' \
 -H 'Accept-Language: en-US,en;q=0.9' \
 -H 'Cache-Control: no-cache' \
 -H 'Connection: keep-alive' \
 -H 'Content-Type: application/json' \
 -H 'Origin: <https://admin.foreverbuy.in>' \
 -H 'Pragma: no-cache' \
 -H 'Referer: <https://admin.foreverbuy.in/>' \
 -H 'Sec-Fetch-Dest: empty' \
 -H 'Sec-Fetch-Mode: cors' \
 -H 'Sec-Fetch-Site: same-site' \
 -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36 Edg/137.0.0.0' \
 -H 'sec-ch-ua: "Microsoft Edge";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
 -H 'sec-ch-ua-mobile: ?0' \
 -H 'sec-ch-ua-platform: "macOS"' \
 -H 'token: eyJhbGciOiJIUzI1NiJ9.YWRtaW5AZXhhbXBsZS5jb21ncmVhdHN0YWNrMTIz.4OrQphsHNe6B8_uPr78EUPXtWPxJ9jQoP8nsPD9TgNA' \
 --data-raw '{}'

### Update order status

curl '<https://api.foreverbuy.in/api/order/status>' \
 -H 'Accept: application/json, text/plain, _/_' \
 -H 'Accept-Language: en-US,en;q=0.9' \
 -H 'Cache-Control: no-cache' \
 -H 'Connection: keep-alive' \
 -H 'Content-Type: application/json' \
 -H 'Origin: <https://admin.foreverbuy.in>' \
 -H 'Pragma: no-cache' \
 -H 'Referer: <https://admin.foreverbuy.in/>' \
 -H 'Sec-Fetch-Dest: empty' \
 -H 'Sec-Fetch-Mode: cors' \
 -H 'Sec-Fetch-Site: same-site' \
 -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36 Edg/137.0.0.0' \
 -H 'sec-ch-ua: "Microsoft Edge";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
 -H 'sec-ch-ua-mobile: ?0' \
 -H 'sec-ch-ua-platform: "macOS"' \
 -H 'token: eyJhbGciOiJIUzI1NiJ9.YWRtaW5AZXhhbXBsZS5jb21ncmVhdHN0YWNrMTIz.4OrQphsHNe6B8_uPr78EUPXtWPxJ9jQoP8nsPD9TgNA' \
 --data-raw '{"orderId":"684677c517795830be9c52da","status":"Shipped"}'
