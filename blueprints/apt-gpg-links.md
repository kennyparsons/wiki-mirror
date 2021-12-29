---
title: APT GPG Updates
description: 
published: true
date: 2021-12-29T18:18:15.390Z
tags: 
editor: markdown
dateCreated: 2021-12-29T18:18:15.390Z
---

# APT GPG Updates
```bash
cd /etc/apt/trusted.gpg.d && \
  for i in *.gpg; \
  do \
  mv "${i}" /usr/share/keyrings/"${i%%.*}"-archive-keyring.gpg; \
  done
```