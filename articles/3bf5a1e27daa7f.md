---
title: "Prisma トラブルシューティング"
emoji: "🐙"
type: "tech"
topics: []
published: false
---

メモ

# Prisma Studioがエラーで起動できない

## 概要

`RangeError: Invalid string length` が出て起動できない

[RangeError: Invalid string length · Issue #895 · prisma/studio](https://github.com/prisma/studio/issues/895)


## 解決方法

ワークアラウンドな方法

1. Chrome Developer Toolを開く
2. Application → IndexedDB からPrisma Studioを選択し、削除する
3. Prisma Studioを立ち上げ直す

↑Issueに書いてあるコメントの通り
https://github.com/prisma/studio/issues/895#issuecomment-1083051249

![](https://storage.googleapis.com/zenn-user-upload/cdfa9cd8dc10-20230907.png)
