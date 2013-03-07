# RAWHIDE. Style Guide

TODO: kawashima あとで書きなおす

## Table of Contents
* [基本方針](#section1)
* [ファイル](#section2)
  * [レイアウトファイル](#section2-1)
  * [部分テンプレート](#section2-2)
* [命名規約](#section3)
  * [クラス・モジュール名](#section3-1)
  * [メソッド名](#section3-2)
  * [定数名](#section3-3)
  * [変数名](#section3-4)
* [ガイドライン](#section4)
  * [インデント](#section4-1)
  * [コメント](#section4-2)
  * [メソッド定義](#section4-3)
  * [ブロック](#section4-4)
  * [条件分岐](#section4-5)
  * [繰り返し](#section4-6)
  * [例外](#section4-7)
  * [ファイルの入出力](#section4-8)
  * [gem](#section4-9)
* [データベース設計](#section5)
  * [データベース名](#section5-1)
  * [日付型カラム名](#section5-2)
  * [タイプコードカラム名](#section5-3)
  * [booleanカラム名](#section5-4)
* [テスト](#section6)


###### section1
## 基本方針
このコーティング規約は、株式会社 RAWHIDE.でのプロジェクトにおいての標準ルールであり、コーティングする際のルール・推奨などを提供するものである。

この規約の根底にあるのは「読みやすくメンテナンスしやすいコードを書く」ことである。

よって、場合によってはこの規約から外れることも時には重要である。その際には自分の考えを整理し、チームメンバーに相談すること。

###### section2
## ファイル

###### section2-1
### レイアウトファイル

###### section2-2
### 部分テンプレート

###### section3
## 命名規約

###### section3-1
### クラス・モジュール名

###### section3-2
### メソッド名

###### section3-3
### 定数名

###### section3-4
### 変数名

###### section4
## ガイドライン

###### section4-1
### インデント
インデントは半角スペース２コ。ハードタブの使用は禁止する。

```ruby
__if x > 0
____if y > 0
______puts "x > 0 && y > 0"
____end
__end
```

###### section4-2
### コメント

###### section4-3
### メソッド定義

###### section4-4
### ブロック

###### section4-5
### 条件分岐

###### section4-6
### 繰り返し

###### section4-7
### 例外

###### section4-8
### ファイル

###### section4-9
### RubyGems

###### section5
## データベース設計

###### section5-1
### データベース名

###### section5-2
### 日付型カラム名

###### section5-3
### タイプコードカラム名

###### section5-4
### booleanカラム名

###### section6
## テスト


