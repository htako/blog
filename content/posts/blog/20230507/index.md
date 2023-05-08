---
title: "書き始め"
date: 2023-05-07
categories: ["hugo"]
tags: ["blog"]
---

## github pages

こちらでいろいろ試してみようかなと思う。  
かなり散文的になる見込み。

## 事始め

ここからforkさせていただいたものを使っています。

https://github.com/kat0h/hugo-blog-template

いったん元記事は削除しないで、新しい記事を書くときにそのままテンプレート的に使おうと思います。

git clone をしたけど最初エラーが出て、

```
WARN 2023/05/07 10:23:23 found no layout file for "HTML" for kind "home": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
```

なんでだろと思っていたんですが、themesファイルがサブモジュールになっていたのに気づいて解決。  
サブモジュールを後から取得するコマンド。

```
git submodule update -i
```

## 最初の記事で気づいたこと

改行は入れないといけない。  
markdown記法だからスペース2つで改行してくれる。  
スペース2つって使いやすいんですかね。エディタで見えないから、結構入れ忘れそうな気がする。改行ってプレビューで見直しても結構見逃すイメージ。  
慣れの問題な気もする。ちゃんとエディタの表示をONにしておかなければ。  

## 後々確認

hugo serve した後に編集したものは反映されない。  
プレビューしたときには即座に反映された方が良さげなので、そのあたりコマンド詳細を確認する。

