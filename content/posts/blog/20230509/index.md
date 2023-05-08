---
title: "github actionsが動いてなかった"
date: 2023-05-09
categories: ["hugo"]
tags: ["blog", "github actions"]
---

## OSのイメージを変えたら進んだ

そもそも、github actionsが動くはずのコンテナがgetできてない雰囲気だったので、`.github/workflows/gh-pages.yml` の runs-on の指定を `ubuntu-latest` にしてみたら、先に進めた。

```
変更前）
    runs-on: ubuntu-18.04
変更後）
    runs-on: ubuntu-latest
```

## git commit ができていなそう

Deployのステージで落ちている。  
エラーメッセージは、どうみても権限関係である。

```
/usr/bin/git push origin gh-pages
remote: Permission to htako/blog.git denied to github-actions[bot].
fatal: unable to access 'https://github.com/htako/blog.git/': The requested URL returned error: 403
Error: Action failed with "The process '/usr/bin/git' failed with exit code 128"
```

よくよく調べていくと、この画面にあたった。  

{{<figure src="./20230509_001.png" width="100%">}}

ここで

* `Allow htako, and select non-htako, actions and reusable workflows` を選択
* `Allow specified actions and reusable workflows` のテキストエリアに実行したいアクションを記述

が必要らしかった。  
今回は、Deployのステージにある `peaceiris/actions-gh-pages@v3` で権限が足りない。  
よって、ちょっと広めにとって `peaceiris/*` を入力してみた。  
そうしたら、ジョブが最後まで通るじゃないですか。

## そして勘違いしていた

`main` ブランチでpushしたら `main` ブランチにコンテンツができてそれが公開できるのだと思っていたら、この github actions はそうではなくて、`main` ブランチにpushしたら、そのソースからブランチにコンテンツだけのブランチ `gh-pages` を作るものだった。  
なので、github pagesで公開すべきブランチは `main` ではなくて `gh-pages` になる。  
ようやくこのジョブの構造が理解できてきた。
