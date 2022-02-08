# Google-Translation-API-Test

## 驗證
1. Creating service accounts and keys<br />
https://cloud.google.com/translate/docs/setup?utm_source=youtube&utm_medium=unpaidsocial&utm_campaign=ram-20190917-Translation-API-Quickstart#creating_service_accounts_and_keys

2. Using the service account key file in your environment
> $export GOOGLE_APPLICATION_CREDENTIALS="KEY_PATH"

## Test 1

測試語言轉換是否成功。<br />

1. Upload "test1.json"<br />
```
{
  "q": "I live in Taiwan.",
  "source": "en",
  "target": "zh-tw",
  "format": "text"
}
```

2. POST<br />
```
curl -X POST \
-H "Authorization: Bearer "$(gcloud auth application-default print-access-token) \
-H "Content-Type: application/json" \
--data @test1.json \
-i \
"https://translation.googleapis.com/language/translate/v2"
```

Result:<br />
```
HTTP/2 200 
content-type: application/json; charset=UTF-8
vary: X-Origin
vary: Referer
vary: Origin,Accept-Encoding
date: Tue, 08 Feb 2022 07:32:55 GMT
server: ESF
cache-control: private
x-xss-protection: 0
x-frame-options: SAMEORIGIN
x-content-type-options: nosniff
alt-svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000,h3-Q050=":443"; ma=2592000,h3-Q046=":443"; ma=2592000,h3-Q043=":443"; ma=2592000,quic=":443"; ma=2592000; v="46,43"
accept-ranges: none

{
  "data": {
    "translations": [
      {
        "translatedText": "我住在台灣。"
      }
    ]
  }
}
```


