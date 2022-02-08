# Google-Translation-API-Test

## 驗證
1. Creating service accounts and keys<br />
https://cloud.google.com/translate/docs/setup?utm_source=youtube&utm_medium=unpaidsocial&utm_campaign=ram-20190917-Translation-API-Quickstart#creating_service_accounts_and_keys

2. Using the service account key file in your environment
> $export GOOGLE_APPLICATION_CREDENTIALS="KEY_PATH"

## Test 1

測試語言轉換是否成功。<br />

1. Upload "test1.json"<br />
>{<br />
>  "q": "I live in Taiwan.",<br />
>  "source": "en",<br />
>  "target": "zh-tw",<br />
>  "format": "text"<br />
>}<br />

