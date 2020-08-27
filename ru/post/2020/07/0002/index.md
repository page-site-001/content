---
title: 'MikroTik и Cloudflare: Динамический IP для домена'
description: ''
images:
  - 'https://images.unsplash.com/photo-1521542464131-cb30f7398bc6'
categories:
  - 'Cloudflare'
  - 'MikroTik'
tags:
  - 'router'
  - 'mikrotik'
  - 'cloudflare'
authors:
  - 'dun43v'
date: '2020-07-12T18:09:48+03:00'
hash: 'ff2ae66e8e14dc4a5aa60cd2e59f6517c64426b0'
uuid: 'ff2ae66e-8e14-5c4a-baa6-0cd2e59f6517'
slug: 'ff2ae66e-8e14-5c4a-baa6-0cd2e59f6517'
draft: 0
---

Когда то на просторах интернета нашёл скрипт реализации динамической смены IP из MikroTik напрямую в панели управления Cloudflare при помощи API. Сам скрипт я немного подкорректировал и опубликовал в [MikroTik Marketplace](https://github.com/marketplace-mikrotik/mikrotik-ext-cloudflare). Где нашёл скрипт уже не помню, вроде бы на страницах официального форума MikroTik. Привожу описание скрипта и переменных.

<!--more-->

Сам скрипт нужно настроить под себя, прописав в нём значения переменных. Значения переменных я указал в [README](https://github.com/marketplace-mikrotik/mikrotik-ext-cloudflare/blob/main/README.md) на GitHub’е. Большинство значений можно узнать из панели управления доменом в Cloudflare, но для получения значения переменной `cfDNSID` необходимо выполнит немного телодвижений.

Для начала в терминале Linux выполнить следующую команду:

```bash
curl -X GET "https://api.cloudflare.com/client/v4/zones/API_ZONE_ID/dns_records"  \
-H "X-Auth-Email: USER_EMAIL"                                                     \
-H "X-Auth-Key: USER_TOKEN"                                                       \
-H "Content-Type: application/json" | python -mjson.tool
```

...соответственно, подставив собственные значения, например (значения фальшивые):

```bash
curl -X GET "https://api.cloudflare.com/client/v4/zones/Q7dslfag51U2B3jRpmbxMInDTCoSFYyH/dns_records"   \
-H "X-Auth-Email: user@cloudflare.com"                                                                  \
-H "X-Auth-Key: CcDXmj5lzd9Na3Wi2fQLPvAJIuwUrxF1VnMyS"                                                  \
-H "Content-Type: application/json" | python -mjson.tool
```

Команды вернёт результат в формате JSON, к примеру (результаты фальшивые):

```json
{
    "result": [
        {
            "id": "gJDSG5la4IWNOEVn6K2PHyope8Q9YhzC",
            "zone_id": "Q7dslfag51U2B3jRpmbxMInDTCoSFYyH",
            "zone_name": "example.com",
            "name": "example.com",
            "type": "A",
            "content": "192.168.10.232",
            "proxiable": true,
            "proxied": true,
            "ttl": 1,
            "locked": false,
            "meta": {
                "auto_added": false,
                "managed_by_apps": false,
                "managed_by_argo_tunnel": false,
                "source": "primary"
            },
            "created_on": "2020-02-23T21:26:27.56227Z",
            "modified_on": "2020-02-23T21:26:27.56227Z"
        }
    ],
    "success": true,
    "errors": [],
    "messages": [],
    "result_info": {
        "page": 1,
        "per_page": 20,
        "count": 7,
        "total_count": 7,
        "total_pages": 1
    }
}
```

Смотрим поле `id` и значение этого поля вставляем в переменную `cfDNSID`.

На этом всё. Не забываем выдать скрипту необходимые права в панели MikroTik, а также прописать автоматический запуск скрипта через **Scheduler**.