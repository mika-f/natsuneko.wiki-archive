---
title: UnityPackage 用と UPM 用と VPM 用とでプロジェクトディレクトリを共有する
description: 
published: true
date: 2023-07-31T10:38:45.100Z
tags: 
editor: markdown
dateCreated: 2023-07-31T10:38:45.100Z
---


現状、 UnityPackage と UPM と VPM とでは、それぞれ異なった形式のディレクトリ構成が必要になります。
UPM の場合は、 Git Repo URL からディレクトリを指定できる、かつ OpenUPM の場合も同様のことが出来るので気にする必要はありませんが、 UnityPackage と VPM とではこのようなことが出来ません。
ここでは、 Unity 標準のプロジェクト構成を保ったまま、 VPM パッケージを作成、管理する方法について紹介します。

# 前提

* GitHub
* GitHub Actions

# ワークフロー

[`natsuneko-laboratory/create-vpmpackage`](https://github.com/natsuneko-laboratory/create-vpmpackage) を使うことで解決可能です。

例：

```yaml
name: "Release VPMPackage by Pushing Tag"

on:
  push:
    tags:
      - v\d+\.\d+\.\d+
  workflow_dispatch:

jobs:
  setup:
    runs-on: ubuntu-latest
    outputs:
      identifier: ${{ steps.vars.outputs.identifier }}
      name: ${{ steps.vars.outputs.name }}
      version: ${{ steps.vars.outputs.version }}
    steps:
      - id: vars
        env:
          NAME: AnimatorControllerToolPostProcessing
          IDENTIFIER: cat.natsuneko.animator-controller-tool-postprocessing
        run: |
          VERSION=$(echo ${{ github.ref }} | sed -e 's/refs\/tags\///' | sed -e 's/refs\/heads\///')
          echo "version=$VERSION" >> $GITHUB_OUTPUT
          echo "name=$NAME" >> $GITHUB_OUTPUT
          echo "identifier=$IDENTIFIER" >> $GITHUB_OUTPUT

  packaging:
    runs-on: ubuntu-latest
    needs: [setup]
    steps:
      - uses: actions/checkout@v2
        with:
          lfs: false

      - run: |
          mkdir ./dist
      - uses: natsuneko-laboratory/create-vpmpackage@v1.0.0
        with:
          package: Assets/NatsunekoLaboratory/${{ needs.setup.outputs.name }}/package.json
          output: dist/${{ needs.setup.outputs.identifier }}-${{ needs.setup.outputs.version }}.zip

      - uses: actions/upload-artifact@v2
        with:
          name: ${{ needs.setup.outputs.name }}
          path: ./dist
```