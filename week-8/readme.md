# Review last lesson

## Week 7 Exercise

Set up a project using React version 18 or later

**Requirements:**

- ESLint + Prettier + a UI component library (optional)
- Project structure should support reusable basic or feature-based modules
- Layout should follow the design of [this site](https://prescripto.vercel.app/)
- Assets can be found in the folder: forever-assets.zip
- Logic functions should follow the behavior of [this site](https://prescripto.vercel.app/)
- APIs can be reused from [this site](https://prescripto.vercel.app/) or replaced with JSON using localStorage

## Api list

### List doctor

curl '<https://prescripto-backend.vercel.app/api/doctor/list>' \
 -H 'accept: application/json, text/plain, _/_' \
 -H 'accept-language: en-US,en;q=0.9' \
 -H 'cache-control: no-cache' \
 -H 'origin: <https://prescripto.vercel.app>' \
 -H 'pragma: no-cache' \
 -H 'priority: u=1, i' \
 -H 'referer: <https://prescripto.vercel.app/>' \
 -H 'sec-ch-ua: "Google Chrome";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
 -H 'sec-ch-ua-mobile: ?0' \
 -H 'sec-ch-ua-platform: "macOS"' \
 -H 'sec-fetch-dest: empty' \
 -H 'sec-fetch-mode: cors' \
 -H 'sec-fetch-site: cross-site' \
 -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36'

### Get Profile

curl '<https://prescripto-backend.vercel.app/api/user/get-profile>' \
 -H 'accept: application/json, text/plain, _/_' \
 -H 'accept-language: en-US,en;q=0.9' \
 -H 'cache-control: no-cache' \
 -H 'origin: <https://prescripto.vercel.app>' \
 -H 'pragma: no-cache' \
 -H 'priority: u=1, i' \
 -H 'referer: <https://prescripto.vercel.app/>' \
 -H 'sec-ch-ua: "Google Chrome";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
 -H 'sec-ch-ua-mobile: ?0' \
 -H 'sec-ch-ua-platform: "macOS"' \
 -H 'sec-fetch-dest: empty' \
 -H 'sec-fetch-mode: cors' \
 -H 'sec-fetch-site: cross-site' \
 -H 'token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjY4NDhhN2U4OTY0MGIwODI4NGQxZjM0ZSIsImlhdCI6MTc0OTU5MjA0Mn0.B9UfU79I9bWscATnLdupg6zWqPCPl67V7-HbeaOCr1g' \
 -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36'

### Update profile

curl '<https://prescripto-backend.vercel.app/api/user/update-profile>' \
 -H 'accept: application/json, text/plain, _/_' \
 -H 'accept-language: en-US,en;q=0.9' \
 -H 'cache-control: no-cache' \
 -H 'content-type: multipart/form-data; boundary=----WebKitFormBoundaryALbDwttBBiQ1WDTb' \
 -H 'origin: <https://prescripto.vercel.app>' \
 -H 'pragma: no-cache' \
 -H 'priority: u=1, i' \
 -H 'referer: <https://prescripto.vercel.app/>' \
 -H 'sec-ch-ua: "Google Chrome";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
 -H 'sec-ch-ua-mobile: ?0' \
 -H 'sec-ch-ua-platform: "macOS"' \
 -H 'sec-fetch-dest: empty' \
 -H 'sec-fetch-mode: cors' \
 -H 'sec-fetch-site: cross-site' \
 -H 'token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjY4NDhhN2U4OTY0MGIwODI4NGQxZjM0ZSIsImlhdCI6MTc0OTU5MjA0Mn0.B9UfU79I9bWscATnLdupg6zWqPCPl67V7-HbeaOCr1g' \
 -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36' \
 --data-raw $'------WebKitFormBoundaryALbDwttBBiQ1WDTb\r\nContent-Disposition: form-data; name="name"\r\n\r\nkhoi\r\n------WebKitFormBoundaryALbDwttBBiQ1WDTb\r\nContent-Disposition: form-data; name="phone"\r\n\r\n000000000\r\n------WebKitFormBoundaryALbDwttBBiQ1WDTb\r\nContent-Disposition: form-data; name="address"\r\n\r\n{"line1":"","line2":""}\r\n------WebKitFormBoundaryALbDwttBBiQ1WDTb\r\nContent-Disposition: form-data; name="gender"\r\n\r\nMale\r\n------WebKitFormBoundaryALbDwttBBiQ1WDTb\r\nContent-Disposition: form-data; name="dob"\r\n\r\n1993-07-28\r\n------WebKitFormBoundaryALbDwttBBiQ1WDTb--\r\n'

### Create account

curl '<https://prescripto-backend.vercel.app/api/user/register>' \
 -H 'accept: application/json, text/plain, _/_' \
 -H 'accept-language: en-US,en;q=0.9' \
 -H 'cache-control: no-cache' \
 -H 'content-type: application/json' \
 -H 'origin: <https://prescripto.vercel.app>' \
 -H 'pragma: no-cache' \
 -H 'priority: u=1, i' \
 -H 'referer: <https://prescripto.vercel.app/>' \
 -H 'sec-ch-ua: "Google Chrome";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
 -H 'sec-ch-ua-mobile: ?0' \
 -H 'sec-ch-ua-platform: "macOS"' \
 -H 'sec-fetch-dest: empty' \
 -H 'sec-fetch-mode: cors' \
 -H 'sec-fetch-site: cross-site' \
 -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36' \
 --data-raw '{"name":"sads","email":"<khoi@gmail.com>","password":"1234"}'

### Login account

curl '<https://prescripto-backend.vercel.app/api/user/login>' \
 -H 'accept: application/json, text/plain, _/_' \
 -H 'accept-language: en-US,en;q=0.9' \
 -H 'cache-control: no-cache' \
 -H 'content-type: application/json' \
 -H 'origin: <https://prescripto.vercel.app>' \
 -H 'pragma: no-cache' \
 -H 'priority: u=1, i' \
 -H 'referer: <https://prescripto.vercel.app/>' \
 -H 'sec-ch-ua: "Google Chrome";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
 -H 'sec-ch-ua-mobile: ?0' \
 -H 'sec-ch-ua-platform: "macOS"' \
 -H 'sec-fetch-dest: empty' \
 -H 'sec-fetch-mode: cors' \
 -H 'sec-fetch-site: cross-site' \
 -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36' \
 --data-raw '{"email":"<abc@gmail.com>","password":"123456"}'

## Admin Panel login

curl '<https://prescripto-backend.vercel.app/api/admin/login>' \
 -H 'accept: application/json, text/plain, _/_' \
 -H 'accept-language: en-US,en;q=0.9' \
 -H 'cache-control: no-cache' \
 -H 'content-type: application/json' \
 -H 'origin: <https://prescripto-admin.vercel.app>' \
 -H 'pragma: no-cache' \
 -H 'priority: u=1, i' \
 -H 'referer: <https://prescripto-admin.vercel.app/>' \
 -H 'sec-ch-ua: "Google Chrome";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
 -H 'sec-ch-ua-mobile: ?0' \
 -H 'sec-ch-ua-platform: "macOS"' \
 -H 'sec-fetch-dest: empty' \
 -H 'sec-fetch-mode: cors' \
 -H 'sec-fetch-site: cross-site' \
 -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36' \
 --data-raw '{"email":"<admin@example.com>","password":"greatstack123"}'

## Admin Panel all doctors

curl '<https://prescripto-backend.vercel.app/api/admin/all-doctors>' \
 -H 'accept: application/json, text/plain, _/_' \
 -H 'accept-language: en-US,en;q=0.9' \
 -H 'atoken: eyJhbGciOiJIUzI1NiJ9.YWRtaW5AZXhhbXBsZS5jb21ncmVhdHN0YWNrMTIz.4OrQphsHNe6B8_uPr78EUPXtWPxJ9jQoP8nsPD9TgNA' \
 -H 'cache-control: no-cache' \
 -H 'origin: <https://prescripto-admin.vercel.app>' \
 -H 'pragma: no-cache' \
 -H 'priority: u=1, i' \
 -H 'referer: <https://prescripto-admin.vercel.app/>' \
 -H 'sec-ch-ua: "Google Chrome";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
 -H 'sec-ch-ua-mobile: ?0' \
 -H 'sec-ch-ua-platform: "macOS"' \
 -H 'sec-fetch-dest: empty' \
 -H 'sec-fetch-mode: cors' \
 -H 'sec-fetch-site: cross-site' \
 -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36'

## Admin Panel appointment list

curl 'https://prescripto-backend.vercel.app/api/admin/appointments' \
 -H 'accept: application/json, text/plain, _/_' \
 -H 'accept-language: en-US,en;q=0.9' \
 -H 'atoken: eyJhbGciOiJIUzI1NiJ9.YWRtaW5AZXhhbXBsZS5jb21ncmVhdHN0YWNrMTIz.4OrQphsHNe6B8_uPr78EUPXtWPxJ9jQoP8nsPD9TgNA' \
 -H 'cache-control: no-cache' \
 -H 'origin: https://prescripto-admin.vercel.app' \
 -H 'pragma: no-cache' \
 -H 'priority: u=1, i' \
 -H 'referer: https://prescripto-admin.vercel.app/' \
 -H 'sec-ch-ua: "Google Chrome";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
 -H 'sec-ch-ua-mobile: ?0' \
 -H 'sec-ch-ua-platform: "macOS"' \
 -H 'sec-fetch-dest: empty' \
 -H 'sec-fetch-mode: cors' \
 -H 'sec-fetch-site: cross-site' \
 -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36'
