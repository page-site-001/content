---
title: 'Запись ISO на USB Flash Drive'
description: ''
images:
  - 'https://images.unsplash.com/photo-1587145820098-23e484e69816'
categories:
  - 'OS'
  - 'Linux'
tags:
  - 'linux'
  - 'usb'
authors:
  - 'Tails_IM'
date: '2020-06-02T09:20:24+03:00'
hash: '5d90ef6ff05f046288a228dac0bb2f48577eadd6'
uuid: '5d90ef6f-f05f-5462-b8a2-28dac0bb2f48'
slug: '5d90ef6f-f05f-5462-b8a2-28dac0bb2f48'
draft: 0
---

Команды для "правильной" записи ISO на USB Flash Drive.

<!--more-->

1. Определить USB-накопитель при помощи команды `fdisk -l`.
2. Отмонтировать ВСЕ разделы с USB-накопителя командой `umount /dev/sdX*`, где `X` - буква накопителя (например, `umount /dev/sdc*`).
3. Загрузить ISO на USB-накопитель:

```bash
# Отмонтировать и очистить USB-накопитель.
umount /dev/sdX* && sgdisk -Z /dev/sdX

# Записать образ на USB-накопитель.
dd if=image.iso of=/dev/sdX bs=4M oflag=direct status=progress; sync

# Извлечь USB-накопитель.
eject /dev/sdX
```