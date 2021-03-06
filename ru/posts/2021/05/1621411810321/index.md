---
title: 'Генератор иконок для сайта'
description: ''
images:
  - 'https://images.unsplash.com/photo-1554061523-c90d630a7ac9'
categories:
  - 'Dev'
tags:
  - 'imagemagick'
  - 'inkscape'
  - 'convert'
authors:
  - 'KitsuneSolar'
licenses:
  - 'cc-by-sa-4.0'

date: '2021-05-18T10:41:46+03:00'
hash: '841ba281a22b95ee797d251a5dc111d8c73f09b8'
uuid: '841ba281-a22b-55ee-b97d-251a5dc111d8'
slug: '841ba281-a22b-55ee-b97d-251a5dc111d8'

comments: 1
feedback: 1
draft: 0
---

Сделал для сайта автоматизированное создание иконок типа `favicon`, которыми пользуются браузеры и устройства для своих нужд.

<!--more-->

Я накидал небольшой скрипт, состоящий из двух функций `png()` и `ico()`. Функция `png()` берёт файл `icon.svg` и преобразует его в PNG, указанных в массиве `size`, размеров. Функция `ico()` также берёт файл `icon.svg` и преобразует его в формат ICO, который содержит в себе несколько размеров изображения.

## Использование

Для работы скрипта необходимо, чтобы в системе были установлены **Inkscape** и **ImageMagick**. Скрипт можно сохранить с произвольным именем, например, `icon.sh` в директорию, где находится изображение `icon.svg`. Далее, вызывать функции следующим образом:

```text
user@localhost ~ % bash icon.sh png
```

```text
user@localhost ~ % bash icon.sh ico
```

Скрипт ищет файл `icon.svg` и преобразует его в необходимые изображения.

## Скрипт

{{< github-repo "pkgstore/linux-bash-favicon" >}}
