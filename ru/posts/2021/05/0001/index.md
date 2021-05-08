---
title: 'Синхронизация репозитория от GitHub к GitLab'
description: ''
images:
  - 'https://images.unsplash.com/photo-1531030874896-fdef6826f2f7'
categories:
  - 'Dev'
tags:
  - 'git'
  - 'github'
  - 'gitlab'
  - 'sync'
  - 'actions'
authors:
  - 'KitsuneSolar'
licenses:
  - 'cc-by-sa-4.0'

date: '2021-05-09T00:06:18+03:00'
hash: '8544b8ce4586478f5633e8ae43441a25c9bb8bde'
uuid: '8544b8ce-4586-578f-9633-e8ae43441a25'
slug: '8544b8ce-4586-578f-9633-e8ae43441a25'

comments: 1
feedback: 1
draft: 0
---

Понадобилось мне на днях синхронизировать некоторые свои репозитории между GitHub и GitLab. Сам GitLab имеет встроенные средства зеркалирования репозиториев от себя к другому git-хранилищу. GitHub же не обладает такой функцией. Но эту функцию можно воссоздать при помощи GitHub Actions.

<!--more-->

Для начала необходимо создать "секреты" с такими переменными:

- `GITLAB_SYNC_REPO_URL` - ссылка на пустой репозиторий GitLab.
- `GITLAB_SYNC_USER_NAME` - имя пользователя GitLab.
- `GITLAB_SYNC_USER_TOKEN` - токен пользователя GitLab. Токен создаётся в настройках аккаунта GitLab.

Далее, в корне репозитория нужно создать файл `.github/workflows/gitlab-sync.yml` со следующим содержанием:

```yml
name: GitLab Sync

on:
  - push
  - delete

jobs:
  sync:
    runs-on: ubuntu-latest
    name: Git Repo Sync
    steps:
      - uses: actions/checkout@v2
        with:
          fetch-depth: 0
      - uses: wangchucheng/git-repo-sync@v0.1.0
        with:
          # Such as https://github.com/wangchucheng/git-repo-sync.git
          target-url: ${{ secrets.GITLAB_SYNC_REPO_URL }}
          # Such as wangchucheng
          target-username: ${{ secrets.GITLAB_SYNC_USER_NAME }}
          # You can store token in your project's 'Setting > Secrets' and reference the name here. Such as ${{ secrets.ACCESS_TOKEN }}
          target-token: ${{ secrets.GITLAB_SYNC_USER_TOKEN }}
```

На этом всё. Теперь при коммите в репозиторий GutHub будет запускаться Action и автоматически синхронизировать изменения с репозиторием на GitLab.