---
title: 'XenForo: Первичные настройки движка и параметры системы'
description: ''
images:
  - 'https://images.unsplash.com/photo-1429772011165-0c2e054367b8'
categories:
  - 'CMF'
  - 'XenForo'
  - 'InDev'
tags:
  - 'cms'
  - 'cmf'
  - 'php'
  - 'xenforo'
authors:
  - 'Tails_IM'
date: '2020-08-27T17:03:13+03:00'
hash: '16cabd8ae6243911104d9d9da85e0bce88e64b70'
uuid: '16cabd8a-e624-5911-904d-9d9da85e0bce'
slug: '16cabd8a-e624-5911-904d-9d9da85e0bce'
draft: 0
---

У меня в проекта значится несколько форумов на движке XenForo. Здесь я собрал для себя первичные параметры и настройки движка XenForo.

<!--more-->

## config.php

Примеры параметров в файле config.php для первоначальной установки и запуска системы.

```php
<?php

# Database.
$config['db']['host']                             = '127.0.0.1';
$config['db']['port']                             = 3306;
$config['db']['username']                         = '';
$config['db']['password']                         = '';
$config['db']['dbname']                           = '';
$config['db']['socket']                           = null;

# Unicode support.
$config['fullUnicode']                            = true;

# Site-wide feature.
$config['enableTfa']                              = false;
$config['enableApi']                              = false;
$config['enableOneClickUpgrade']                  = false;

# Cookie.
$config['cookie']['prefix']                       = 'xf_';

# Data and script locations.
$config['externalDataPath']                       = 'storage/data';
$config['externalDataUrl']                        = 'storage/data';
$config['internalDataPath']                       = 'storage/data.int';
$config['codeCachePath']                          = '%s/cache/code';
$config['tempDataPath']                           = '%s/temp';
$config['javaScriptUrl']                          = 'js';

# Auth.
$config['auth'] = [
  'algo' => PASSWORD_ARGON2ID
];

# Cache.
/*
$config['cache']['enabled']                       = true;
$config['cache']['provider']                      = 'Redis';
$config['cache']['config']                        = [
  'host' => '127.0.0.1',
  'password' => '',
  'database' => 1
];
*/

# Guest page caching.
/*
$config['pageCache']['enabled']                   = true;
$config['cache']['context']['page']['provider']   = 'Filesystem';
$config['cache']['context']['page']['config']     = [
  'directory' => ''
];
*/
```

## Регистрация пользователей

Параметры для регистрации пользователей.

#### Регулярное выражение

```
#(?!^[\d\-\_\s]+$)^(([a-zA-Z0-9\-\_\s]+)|(((\xD0[\x80-\xBF])|(\xD1[\x80-\xBF])|([0-9\-\_\s]))+))$#
```

## Теги

Параметры для ввода тегов.

#### Регулярное выражение

```
#(?!^[\d\-\_\s]+$)^(([a-zA-Z0-9\-\_\s]+)|(((\xD0[\x80-\xBF])|(\xD1[\x80-\xBF])|([0-9\-\_\s]))+))$#
```

## Группы пользователей

Настройки групп пользователей.

#### Стандартные группы

- Unregistered / Unconfirmed `ID(1)`
- Registered `ID(2)`
- Administrative `ID(3)`
- Moderating `ID(4)`