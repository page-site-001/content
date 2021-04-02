---
title: 'Monero Unit'
description: ''
images:
  - 'https://images.unsplash.com/photo-1552057426-9f23e61fa7b1'
categories:
  - 'Crypto'
  - 'Linux'
tags:
  - 'monero'
  - 'systemd'
authors:
  - 'KitsuneSolar'
date: '2021-03-05T14:03:20+03:00'
hash: '0a8155474f1812a0aa99c463421872cae7feee23'
uuid: '0a815547-4f18-52a0-9a99-c463421872ca'
slug: '0a815547-4f18-52a0-9a99-c463421872ca'
draft: 0
---

Бум майнинга. Скупают видеокарты, ноутбуки. Будут майнить на тостерах и стиральных машинах. Решил попробовать **Monero**. Задача была запустить майнер в фоне, желательно в отдельной сессии. И чтобы запускался он каждый раз при старте машины.

<!--more-->

Написал небольшой **systemd unit** для майнера [xmrig](https://github.com/search?q=xmrig).

{{< github-repos "KitsuneSolar/xmrig-systemd" >}}

Запускается от имени `root` в отдельной сессии **screen**, но можно запускать от любого пользователя: в командах запуска и остановки необходимо вместо `root` прописывать имя другого пользователя.

## Установка

1. Установить `screen`.
2. Поместить в директорию `/etc/systemd/system` файл `xmrig@.service`.
3. В файле `xmrig@.service` задать в параметре `ExecStart` путь до `xmrig.run.sh`.

## Использование

```bash
# Запуск
systemctl enable --now xmrig@root

# Остановка
systemctl disable --now xmrig@root
```
