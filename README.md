# Google-Translation-API-Test

## Description
測試 google translation API

## Test Case
| ID  | 題目 | 預期結果  | 實際結果 | 
| --- | --- | --- | --- |
| 1-1  | 輸入指示英文轉換繁體中文，語言轉換是否成功 | 成功，回傳200 | Pass | 
| 1-2  | 輸入的其中一欄沒有填寫，語言轉換是否成功  | 不成功，回傳400 | Pass | 
| 2  | 同時輸入多種語言，是否成功偵測語言 | 成功，回傳200 | Pass | 
| 3  | 是否成功取得所有語言編號 | 成功，回傳200 | Pass | 

## Verification
1. Creating service accounts and keys<br />
https://cloud.google.com/translate/docs/setup?utm_source=youtube&utm_medium=unpaidsocial&utm_campaign=ram-20190917-Translation-API-Quickstart#creating_service_accounts_and_keys

2. Using the service account key file in your environment
> $export GOOGLE_APPLICATION_CREDENTIALS="KEY_PATH"

## Test 1-1
1. Upload "test1-1.json"<br />
```
{
  "q": "I live in Taiwan.",
  "source": "en",
  "target": "zh-tw",
  "format": "text"
}
```

2. POST API<br />
```
curl -X POST \
-H "Authorization: Bearer "$(gcloud auth application-default print-access-token) \
-H "Content-Type: application/json" \
--data @test1-1.json \
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

## Test 1-2

1. Upload "test1-2.json"
```
{
  "q": "I live in Taiwan.",
  "source": "en",
  "target": "",
  "format": "text"
}
```

2. POST API<br />
```
curl -X POST \
-H "Authorization: Bearer "$(gcloud auth application-default print-access-token) \
-H "Content-Type: application/json" \
--data @test1-2.json \
-i \
"https://translation.googleapis.com/language/translate/v2"
```

Result:<br />
```
HTTP/2 400 
vary: X-Origin
vary: Referer
vary: Origin,Accept-Encoding
content-type: application/json; charset=UTF-8
date: Tue, 08 Feb 2022 08:23:10 GMT
server: ESF
cache-control: private
x-xss-protection: 0
x-frame-options: SAMEORIGIN
x-content-type-options: nosniff
alt-svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000,h3-Q050=":443"; ma=2592000,h3-Q046=":443"; ma=2592000,h3-Q043=":443"; ma=2592000,quic=":443"; ma=2592000; v="46,43"
accept-ranges: none

{
  "error": {
    "code": 400,
    "message": "Invalid Value",
    "errors": [
      {
        "message": "Invalid Value",
        "domain": "global",
        "reason": "invalid"
      }
    ]
  }
}
```
## Test 2
1. Upload "test2.json"<br />
```
{
  "q": [
    "I live in Taiwan.",
    "我住在台灣。",
    "私は台湾に住んでいます。"
  ]
}
```

2. POST API<br />
```
curl -X POST \
-H "Authorization: Bearer "$(gcloud auth application-default print-access-token) \
-H "Content-Type: application/json" \
--data @test2.json \
-i \
"https://translation.googleapis.com/language/translate/v2/detect"
```

Result:<br />
```
HTTP/2 200 
content-type: application/json; charset=UTF-8
vary: X-Origin
vary: Referer
vary: Origin,Accept-Encoding
date: Tue, 08 Feb 2022 08:29:41 GMT
server: ESF
cache-control: private
x-xss-protection: 0
x-frame-options: SAMEORIGIN
x-content-type-options: nosniff
alt-svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000,h3-Q050=":443"; ma=2592000,h3-Q046=":443"; ma=2592000,h3-Q043=":443"; ma=2592000,quic=":443"; ma=2592000; v="46,43"
accept-ranges: none

{
  "data": {
    "detections": [
      [
        {
          "isReliable": false,
          "language": "en",
          "confidence": 1
        }
      ],
      [
        {
          "isReliable": false,
          "language": "zh-TW",
          "confidence": 1
        }
      ],
      [
        {
          "isReliable": false,
          "confidence": 1,
          "language": "ja"
        }
      ]
    ]
  }
}
```
## Test 3
1. GET API<br />
```
curl -X GET \
-H "Authorization: Bearer "$(gcloud auth application-default print-access-token) \
-i \
https://translation.googleapis.com/language/translate/v2/languages
```

Result:<br />
```
HTTP/2 200 
content-type: application/json; charset=UTF-8
vary: X-Origin
vary: Referer
vary: Origin,Accept-Encoding
date: Tue, 08 Feb 2022 08:37:12 GMT
server: ESF
cache-control: private
x-xss-protection: 0
x-frame-options: SAMEORIGIN
x-content-type-options: nosniff
alt-svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000,h3-Q050=":443"; ma=2592000,h3-Q046=":443"; ma=2592000,h3-Q043=":443"; ma=2592000,quic=":443"; ma=2592000; v="46,43"
accept-ranges: none

{
  "data": {
    "languages": [
      {
        "language": "af"
      },
      {
        "language": "am"
      },
      {
        "language": "ar"
      },
      {
        "language": "az"
      },
      {
        "language": "be"
      },
...}
```
