---
title: 'Первичная настройка UAIK'
description: ''
images:
  - 'https://images.unsplash.com/photo-1518432031352-d6fc5c10da5a'
categories:
  - 'OS'
  - 'Linux'
tags:
  - 'linux'
  - 'fedora'
authors:
  - 'KitsuneSolar'
date: '2020-06-02T09:20:27+03:00'
hash: '59781965afe7cdd5d798d1c5ba6cdafd6a250c4a'
uuid: '59781965-afe7-5dd5-9798-d1c5ba6cdafd'
slug: '59781965-afe7-5dd5-9798-d1c5ba6cdafd'
draft: 0
---

После автоматической установки (Kickstart) при помощи [UAIK](https://uaik.github.io/) , Fedora запустится в текстовом режиме. На этом этапе необходимо произвести первичную настройку операционной системы.

<!--more-->

#### Включение графического режима

```bash
systemctl set-default graphical.target
```

#### Создание пользователя

```bash
# Добавить пользователя.
useradd -mc "User 0001" user-0001

# Установить пароль для пользователя.
passwd user-0001
```

#### Отключение пользователя

```bash
# Отключить пользователя.
usermod -L user-0000
```

#### Перемещение пользователя

```bash
usermod -md /new_home/user-0001 user-0001
```

#### Работа с диском

Чтобы создать на новом диске раздел, необходимо войти в программу `parted`:

```bash
parted -a optimal /dev/sdb
```

Выполнить следующие команды:

```bash
(parted) mklabel gpt
(parted) mkpart primary 0% 100%
(parted) quit
```

Создать файловую систему:

```bash
mkfs.xfs /dev/sdb1
```

Настроить автоматическое монтирование раздела в `/etc/fstab`:

```bash
/dev/sdb1 /home/storage xfs defaults 0 0
```
