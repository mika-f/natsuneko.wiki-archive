---
title: シェーダー
description: 
published: true
date: 2023-07-18T16:32:43.441Z
tags: パーティクルライブ
editor: markdown
dateCreated: 2023-07-18T15:51:19.800Z
---

パーティクルライブでよく使われているシェーダーについて。
一部の人 (わたしや Reimhak さん) は自作しているが、基本的には有名どころが使われるケースが多い。


# 汎用シェーダー

特に用途を限定しない多機能シェーダー。

## Poiyomi Toon Shader

* https://github.com/poiyomi/PoiyomiToonShader
* https://www.poiyomi.com/

海外の有名な汎用シェーダー。アバター用のシェーダーとしても多機能だし、機能を応用することで視界ジャックをすることも可能。


## Mochies Unity Shaders

* https://github.com/MochiesCode/Mochies-Unity-Shaders


# 視界ジャックシェーダー

視界ジャックは、 3D モデルに対してシェーダーを描画するのでは無く、画面全体に対して描画を行うシェーダー。
実際は超巨大な球の内側に描画していたりするが、その中にエフェクトをかけられるシェーダーのことを視界ジャックシェーダーと呼んでいることが多い。

## パリピシェーダー (有料)

* https://booth.pm/ja/items/1095863

日本で一番有名な視界ジャックシェーダー。
比較的多機能で、 Reimhak さん本人が使っているので使用実績も多い。


## Leviant Shader (無料)

* https://github.com/Leviant/ScreenSpace_Ubershader

海外でかなり有名な視界ジャックシェーダー。
海外の場合は「視界ジャック」では無く「ScreeSpace」と呼ばれていることが多い。
ディストーションやノイズなど多種多様なエフェクトがある。
英語なので注意。


## June Shader (有料、無料版有り)

* https://booth.pm/ja/items/3537955
* https://www.luka.moe/june.html

上記 Leviant と同じく多数のエフェクトを搭載したシェーダー。 Lite 版は Leviant で代替可能ではあるが、有料版はかなり多くのエフェクトがあるので、もし視界ジャックでぶんぶん飛ばしたい人は課金するのもアリ。

# 歌詞シェーダー

パーティクルライブのうち、歌詞をメインとした演出を作成したい場合に多用するシェーダー。
歌詞のテキストを 3D モデルとして、それらに当てると様々な歌詞エフェクトが作成できるようになる。


## 歌詞シェーダー (有料)

* https://booth.pm/ja/items/1273522

安定の Reimhak さんのシェーダー。
Vket3 の `world.execute(me);` で使用されているシェーダーなので、使用実績もあり、参考になるものもある。
お値段もそこまでしないので、持っておくと良い。