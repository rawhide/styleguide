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
  * [gems](#section4-9)
  * [ERB::Util.html_escape](#section4-10)
* [データベース設計](#section5)
  * [データベース名](#section5-1)
  * [日付型カラム名](#section5-2)
  * [タイプコードカラム名](#section5-3)
  * [booleanカラム名](#section5-4)
* [テスト](#section6)
* [原則](#section7)
  * [スコープは適切に](#section7-1)
  * [DRY(Don't Your Self)](#section7-2)
  * [OCP(Open-Closed Principle)](#section7-3)
* [参考文献](#section8)

###### section1
## 基本方針
- レディーに悲しい思いはさせない。

このスタイルガイドは、株式会社 RAWHIDE.でのプロジェクトにおいての標準ルールであり、コーティングおよび設計する際のルール・推奨などを提供するものである。

この規約の根底にあるのは「読みやすくメンテナンスしやすいコードを書く」ことである。

よって、場合によってはこの規約から外れることも時には重要である。その際には自分の考えを整理し、チームメンバーに相談すること。

###### section2
## ファイル
以下は Rails プロジェクトにおいてのルールである。基本的には Rails のルールに従うこと。

###### section2-1
### レイアウトファイル
RAILS_ROOT/app/views/layouts はレイアウトファイルのみを入れる。

全体を通して使用するレイアウトファイルは application.html.erb という名前で作成する。

###### section2-2
### 部分テンプレート
コントローラにまたがる部分テンプレートは RAILS_ROOT/app/views/share に配置。

あるコントローラのみで使用する部分テンプレートは RAILS_ROOT/app/controller_name に配置する。

###### section3
## 命名規約
名前は単なるラベルではなく、読み手に意味を伝えるべきものである。よって名前は意味のあるものでなくてはならない。

また、原則として基本的に単語の省略は行わない。特にグローバル変数などのスコープが拾い物に大しては厳禁である。

名前が長い場合に、入力の手間が増えるという問題があるが、それはIDEやエディタで対応できることなのでここでは問題にしない。

###### section3-1
### クラス・モジュール名
クラス、モジュール名は、各単語の一文字めを大文字にし、'_'などの区切り文字は使用しない。

HTTPなどの略語の場合は全て大文字んおままとする。

例外クラスでは特別な事情がない限り末尾に「Error」とつける。

**正解**
```ruby
ExampleClass
HTTPClient
PermissionError
```

**誤り**
```ruby
Example_Class
EXAMPLE_CLASS
HTTP_Client
```

###### section3-2
### メソッド名
メソッド名は、全て小文字とし単語の区切りに`_`を用いる。

真偽値を返すメソッド名は、動詞または形容詞に`?`を付け、形容詞に`is_`は付けない。

破壊的なメソッドと非破壊的なメソッドの両方を提供する場合、破壊的なメソッドには`!`を付ける。

**正解**
```ruby
add_something
visible?
split
split!
```

**誤り**
```ruby
addSomething
Add_Something
is_visible
is_visible?
```

###### section3-3
### 定数名
クラス、モジュール名以外の定数名はすべて大文字とし、単語の区切りに'_'を用いる。

**正解**
```ruby
EXAMPLE_CONSTANT
```

###### section3-4
### 変数名
変数名は全て小文字とし、単語の区切りに'_'を用いる。

また、スコープが狭いループ変数には、i,j,k という名前、スコープが狭い変数名は、クラス名を省略したものを使用してよい。

- (例：eo = ExampleObjext.new

```ruby
tmp
local_variable
@instance_variable
$global_variable
```

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
コメントは原則書かない。なぜならコードの読みにくさを補助するものではないためである。

書き手はコメントがなくても意図が伝わるようなコードを書くべきである。

よてコードは読めばわかることや、当たり前のことをわざわざコメントとして残す必要はない。

コーディング標準や規約に反する場合、またプログラマー個人の意図がソースに介入している場所に限り、わかりやすいコメントを残す。

まt,あコメントを残す場合には「なにを」ではなく「なぜ」を書くこと。

###### section4-3
### メソッド定義
メソッドの定義の仮引数リストには括弧を付ける。

引数がない場合は、括弧を省略する。

**正解**
```ruby
def foo(x, y)
  ・・・
end
```

**誤り**
```ruby
def foo x, y
  ・・・
end

def foo()
  ・・・
end
```
###### section4-4
### ブロック
ブロックは基本的にdo・・・endを使用する。ただし１行の時は{}を使う。

またメソッドチェーンの場合も{}を使用する。

**正解**
```ruby
foo(x,y) do
  ・・・
end

bar.each{|i| i.to_s}

bar.map{|i| i.to_s}.each{|i| puts i}
```

**誤り**
```ruby
foo(x,y) {
  ・・・
end

foo.map do |i|
  i.to_s
end.each do |i|
  puts i
end
```

###### section4-5
### 条件分岐
if式のthenは省略する。

if!xのような場合は、unlessを使用する。

条件が十分に簡単で、一行でかける場合は、修飾子として使ってもよい。

**正解**
```ruby
if x > 0
  puts "x > 0"
else
  puts "x <= 0"
end

unless x > 0
  puts "x <= 0"
else
  puts "x > 0"
end

puts "x is true" if x
```

**誤り**
```ruby
if x > 0 then
  puts "x > 0"
end

puts "hoge" if foo && bar && baz && quux
```

**正解**
```ruby
case x
when 1
  puts "x is 1"
when 2
  puts "x is 2"
end
```

**誤り**
```ruby
if x == 1
  puts "x is 1"
elseif == 2
  puts "x is 2"
end

case x
when 1 then
  puts "x is 1"
when 2 then
  puts "x is 2"
end
```

###### section4-6
### 繰り返し
while の do は省略する。

while !x のような場合は、util x に置き換える。

**正解**
```ruby
while cond
  puts "puts is false"
end

util cond
  puts "cond is false"
end
```

**誤り**
```ruby
while cond do
  puts "cond is true"
end
```

また、無限ループには loop を使用する。

**正解**
```ruby
loop do
  puts "looping"
end
```

**誤り**
```ruby
while true
  puts "looping"
end
```

###### section4-7
### 例外
例外発生の基本方針はそれが「異常事態」かどうかで判断する。

明示的に例外を発生させないとプログラムが以上終了する場合などに用いる。

例えば ActiveRecord での save!メソッドは使わず、save メソッドを使用する。

バリデーションに引っかかるのは例外ではなく、想定された動作である。

rescue を全て消しても、通常に動作する。

###### section4-8
### ファイル
ファイルの入出力は特別な事情がない限りブロックを使うこと。

**正解**
```ruby
open("sample.txt", "r") do |f|
  puts f.gets
end
```

**誤り**
```ruby
begin
  f = open("sample.txt", "r")
  puts f.gets
ensure
  f.close
end
```

###### section4-9
### RubyGems
Rails アプリで使用する gems は RAILS_ROOT/config/environment.rb に指定すること。

```ruby
config.gem 'rspec', ;lib => false
```

また、gem は rake gems:unpack を使用し、RAILS_ROOT/vender/gems に格納すること。

###### section4-10
### ERB::Util.html_escape
Web アプリにおいて、出力文字列のエスケープは XSS に対する最も基本的な対処法である。

Rails には ERB::Util.html_escape の alias である h ヘルパーが実装されている。

特別な事情がない限り View への文字列の出力には h ヘルパーを必ず用いること。

```ruby
<%= h @output_str %>
```

###### section5
## データベース設計

###### section5-1
### データベース名
development, product 環境ともに project_name で統一。

test 環境、またその他の環境に関しては project_name_environment で統一。

###### section5-2
### 日付型カラム名
****_at で統一。

年日時のみであっても ****_on は使わない。

###### section5-3
### タイプコードカラム名

###### section5-4
### booleanカラム名

###### section6
## テスト
プロダクトコードに書く前に、テストコードを書くこと(テストファースト)

テストツールには RSpec を標準とする。

テストは自動化し、バグの早期発見に努める。

###### section7
## 原則
プログラムの設計において先人たちの知恵を借りることは大事である。

盲目的に原則を信じるのではなく、「なぜ」かを意識すること。

また様々な原則・デザインパターンの学習に努めること。

###### section7-1
### スコープは適切に
スコープは限りなく狭くすること。

本当に必要だと思ったときのみ、グローバルなスコープを用いること。

###### section7-2
### DRY(Don't Your Self)
同じ処理を二度と書かないこと。

###### section7-3
### OCP(Open-Closed Principle)
拡張に対して開いていなければならず、修正に対して閉じていなければならない。

「拡張に対して閉じている」と言うのは、モジュールの拡張が可能ということでもあり、「修正に対して閉じている」と言うのは、モジュールの内部実装を修正してもそのインターフェースは安定しているということである。

###### section8
## 参考文献
達人プログラマー[ISBN4-89471-274-1]

プログラミング作法[ISBN4-7561-3649-4]

Kenji Hiranabe, コーディング標準(オリジナル)
http://objectclub.esm.co.jp/eXtremeProgramming/CodingStd.doc

Ruby コーディング規約
http://shugo.net/ruby-codeconv/codeconv.html

