---
title: 'Зеркалирование репозиториев между несколькими хостингами'
description: ''
images:
  - 'https://images.unsplash.com/photo-1611854571485-982a1f4ba294'
cover:
  image:
    crop: 'entropy'
categories:
  - 'Dev'
tags:
  - 'git'
  - 'github'
  - 'gitlab'
  - 'mirror'
  - 'sync'
  - 'action'
authors:
  - 'KitsuneSolar'
licenses:
  - 'cc-by-sa-4.0'

date: '2021-07-06T20:40:43+03:00'
hash: '3834fbed71c8d97976c2236269f5ecea24083a24'
uuid: '3834fbed-71c8-5979-b6c2-236269f5ecea'
slug: '3834fbed-71c8-5979-b6c2-236269f5ecea'

comments: 1
feedback: 1
draft: 0
---

В предыдущей статье {{< uuid "8544b8ce-4586-578f-9633-e8ae43441a25" >}} я рассказал о том, как организовать синхронизацию между репозиториями GIT на разных хостингах, в частности, между GitHub и GitLab. В итоге, я решил сделать собственный GitHub Action, который позволяет полностью зеркалировать репозитории.

<!--more-->

{{< github-repo "pkgstore/github-action-mirror" >}}

## Использование

Для подключения зеркалирования, к примеру, с GitHub на GitLab, необходимо в исходном репозитории создать файл `.github/workflows/mirror.yml`, в котором указать следующее содержимое:

```yml
name: "Repository Mirror"

on:
  - push

jobs:
  mirror:
    runs-on: ubuntu-latest
    name: "Mirror"
    steps:
      - uses: pkgstore/github-action-mirror@main
        with:
          source_repo: "https://github.com/${{ github.repository }}.git"
          source_user: "${{ secrets.MIRROR_SOURCE_USER_GITHUB }}"
          source_token: "${{ secrets.MIRROR_SOURCE_TOKEN_GITHUB }}"
          target_repo: "https://gitlab.com/${{ github.repository }}.git"
          target_user: "${{ secrets.MIRROR_TARGET_USER_GITLAB }}"
          target_token: "${{ secrets.MIRROR_TARGET_TOKEN_GITLAB }}"
```

- `source_repo` - **URL** исходного репозитория.
- `source_user` - **пользователь** исходного репозитория.
- `source_token` - **токен пользователя** исходного репозитория.
- `target_repo` - **URL** зеркального репозитория.
- `target_user` - **пользователь** зеркального репозитория.
- `target_token` - **токен пользователя** зеркального репозитория.

В этом коде стоит обратить внимание на параметр `target_repo`. GitLab позволяет автоматически создавать репозиторий при зеркалировании, а так как у меня адреса репозиториев совпадают между GitHub и GitLab, мне гораздо проще выстроить конструкцию `https://gitlab.com/${{ github.repository }}.git`. Переменная `${{ github.repository }}` содержит имя пользователя / организации и название репозитория, и, при настройке зеркалирования репозитория на GitHub'е, зеркало репозитория автоматически создаётся на GitLab'е.
