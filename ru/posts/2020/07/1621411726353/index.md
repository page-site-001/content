---
title: 'GnuPG: Создание и работа с ключами шифрования'
description: ''
images:
  - 'https://images.unsplash.com/photo-1572435555646-7ad9a149ad91'
categories:
  - 'Crypto'
tags:
  - 'gpg'
  - 'gnupg'
authors:
  - 'KitsuneSolar'

date: '2020-07-16T09:55:17+03:00'
hash: '7a204545daa838ce6a3575e732e1bcc08558b2e1'
uuid: '7a204545-daa8-58ce-ba35-75e732e1bcc0'
slug: '7a204545-daa8-58ce-ba35-75e732e1bcc0'

comments: 1
draft: 0
---

**GnuPG (GPG)** это программа для шифрования информации и создания электронных цифровых подписей. Она создавалась в качестве свободной альтернативе несвободному **PGP**.

<!--more-->

## Создание ключа

GPG предоставляет различные алгоритмы шифрования. Я предпочитаю алгоритм **ECC**, основанный на эллиптических кривых (Elliptic Curve Cryptography).

Для создания ключей шифрования, нужно чтобы в системе была установлена утилита GPG. Для систем **Debian** и **CentOS / Fedora** этим занимается пакет `gnupg`, устанавливается командами:

```bash
# CentOS 8 / Fedora
dnf install gnupg

# Debian
apt install gnupg
```

После того, как пакет установлен, можно начать создание ключа командой:

```bash
gpg --expert --full-gen-key
```

Команда вернёт следующий результат:

```
gpg (GnuPG) 2.2.20; Copyright (C) 2020 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
   (7) DSA (set your own capabilities)
   (8) RSA (set your own capabilities)
   (9) ECC and ECC
  (10) ECC (sign only)
  (11) ECC (set your own capabilities)
  (13) Existing key
  (14) Existing key from card
Your selection?
```

Здесь спрашивается, какой конкретно ключ мы хотим получить. Вводим `9`. Получаем:

```
Please select which elliptic curve you want:
   (1) Curve 25519
   (3) NIST P-256
   (4) NIST P-384
   (5) NIST P-521
   (9) secp256k1
Your selection?
```

А здесь уже предстоит выбрать алгоритм шифрования. Вводим `1`. Получаем:

```
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0)
```

На последнем шаге настройки ключа спрашивается время действия ключа. Обычно, личные ключи генерируются с безлимитным временем действия. Вводим `0` (этот пункт идёт по умолчанию).

Дальше будет пара-тройка вопросов по поводу имени владельца ключа, его адреса e-mail и с просьбой указать комментарий. Таким образом, создаётся пара ключей: закрытый и открытый. Открытый ключ можно публиковать на различных ресурсах с целью идентификации владельца и подтверждения его личности. Например, так работает верификация коммитов на GitLab’е и GitHub’е. Закрытый ключ должен всегда оставаться внутри системы.

## Список ключей в системе

Посмотреть установленные в системе ключи можно командой:

```bash
gpg --list-keys --keyid-format LONG --with-fingerprint
```

Здесь:
- `--list-keys` - показать список ключей.
- `--keyid-format LONG` - формат отображения каждого ключа в расширенном (`LONG`) формате.
- `--with-fingerprint` - вывести отпечаток. Для себя всегда добавляю эту опцию на всякий случай.

Команда вернёт следующий результат:

```bash
pub   ed25519/JTM4BAVLPI8F0XHR 2020-02-17 [SC]                                # Key: ID.
      Key fingerprint = XXXX XXXX XXXX XXXX XXXX  XXXX XXXX XXXX XXXX XXXX    # Key: Fingerprint.
uid                 [ultimate] John Doe <john.doe@example.com>                # Key: INFO.
sub   cv25519/AI9NEDUOWRF016Y2 2020-02-17 [E]
```

Здесь:
- `JTM4BAVLPI8F0XHR` - идентификатор ключа. Он потребуется для каких-либо действий с ключом (редактирование / удаление / и т.п.).
- `[ultimate]` - уровень доверия к ключу.
- `John Doe` - имя хозяина ключа.
- `<john.doe@example.com>` - почта хозяина ключа.
- `ed25519` & `cv25519` - алгоритмы шифрования.

## Экспорт и импорт ключа

При создании открытого и закрытого ключей, необходимо экспортировать их для того, чтобы они хранились где-то независимо от системы, например, на какой-нибудь карте памяти или USB-флешке. Следующие две команды выполняют необходимые действия:

```bash
# Export: PUBLIC.
gpg --armor --output JohnDoe.public.asc --export JTM4BAVLPI8F0XHR

# Export: PRIVATE.
gpg --armor --output JohnDoe.private.asc --export-secret-keys JTM4BAVLPI8F0XHR
```

Здесь:
- `--armor` - экспорт ключа в формате **ASCII** (текстовый формат).
- `--output` - имя файлы, в который будет экспортирован ключ.
- `--export JTM4BAVLPI8F0XHR` - экспорт открытого ключа с идентификатором `JTM4BAVLPI8F0XHR`.
- `--export-secret-keys JTM4BAVLPI8F0XHR` - экспорт закрытого ключа с идентификатором `JTM4BAVLPI8F0XHR`.

С экспортом разобрались. Теперь по поводу импорта... Импортировать также необходимо открытый и закрытый ключи. Следующие две команды выполняют необходимые действия:

```bash
# Import: PUBLIC.
gpg --import JohnDoe.public.asc

# Import: PRIVATE.
gpg --import JohnDoe.private.asc
```

После импорта ключ приобретает **стандартный уровень доверия**. Для повышения или понижения уровня доверия, ключ необходимо отредактировать.

## Редактирование ключа

Следующая команда позволяет отредактировать ключ:

```
gpg --edit-key JTM4BAVLPI8F0XHR
```

Здесь:
- `--edit-key JTM4BAVLPI8F0XHR` - редактирование ключа с идентификатором `JTM4BAVLPI8F0XHR`.

Режим редактирования ключа представляет собой текстовый интерфейс, в который вручную вбиваются команды. Например, повысим уровень доверия к ключу до максимального (ultimate).

1. Вводим `trust`.
2. Выбираем `5 (I trust ultimately)`.
3. Вводим `quit` (выход).