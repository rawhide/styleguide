# RAWHIDE. Style Guide

*漢なら、黙って一枚、README*

## Table of Contents
* [基本方針](#section1)
* [ファイル](#section2)
  * [部分テンプレート](#section2-2)
* [命名規約](#section3)
  * [クラス・モジュール名](#section3-1)
  * [メソッド名](#section3-2)
  * [定数名](#section3-3)
  * [変数名](#section3-4)
  * [シンボル](#section3-5)
* [ガイドライン](#section4)
  * [インデント](#section4-1)
  * [コメント](#section4-2)
  * [メソッド定義](#section4-3)
  * [ブロック](#section4-4)
  * [条件分岐](#section4-5)
  * [繰り返し](#section4-6)
  * [例外](#section4-7)
  * [ファイルの入出力](#section4-8)
  * [RubyGems](#section4-9)
  * [ERB::Util.html_escape](#section4-10)
  * [メタプログラミング](#section4-11)
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
- 食べ物や包丁を武器につかわない。

### 目的
- 「読みやすくメンテナンスしやすいコードを書く」ことの価値観をチームで共有できる。
- コーディング規約という共通基盤を通して、プログラマーのスキルアップをはかることができる。

### 使い方
- 異臭をはなつ部分は、issueで議論しましょう。決まったものからこちらに移していきましょう。
- 場合によってはこの規約から外れることも時には重要であり、その際はなにかしらの説明を用意するようにしましょう。

###### section2
## ファイル
- 以下は Rails プロジェクトにおいてのルールである。基本的には Rails のルールにしたがうようにしましょう。

###### section2-2
### 部分テンプレート
- コントローラにまたがる部分テンプレートは RAILS_ROOT/app/views/share に配置するようにしましょう。

###### section3
## 命名規約
- 名前は単なるラベルではなく、読み手に意味を伝えるべきものである。よって名前は意味のあるものであるべきです。命名する対象の変数のスコープの広さにに比例してわかりやすさ重視にしましょう。
```ruby
  #定数
  Teinenpi #○
  TNP      #×

  #クラス/モジュール名
  class Joshikousei; end; #○
  class Jk; end;          #×

  #メソッド名
  def joshikousei?; end; #○
  def jk?                #×

  #インスタンス変数
  @joshikousei #○
  @jk          #△

  #ローカル変数
  @girls.each do |g| #○
    g.joshikousei?   #○
  end
```

名前が長い場合に、入力の手間が増えるという問題があるが、それはIDEやエディタで対応できることなのでここでは問題にせずにいきましょう！

###### section3-1
### クラス・モジュール名
- クラス、モジュール名は、各単語の一文字めを大文字にし、'_'などの区切り文字は使用しません。
- TPPなどの略語の場合は全て大文字のままにしましょう（省略してるよーって意味が伝わるように）。
- 例外クラスでは特別な事情がない限り末尾に「Error」をつけましょう。
- よほどの意図がない限り、複数名を使用するはやめましょう。

**正解**
```ruby
NurseCall
TTPClient
AKBMember
OreOreError
```

**誤り**
```ruby
Nurse_Room
TPP_CLIENT
AKBMembers
CsvReader
```

###### section3-2
### メソッド名
- メソッド名は、全て小文字とし単語の区切りに`_`をつかいましょう。
- 真偽値を返すメソッド名は、動詞または形容詞に`?`を付けましょう。
- 破壊的なメソッドと非破壊的なメソッドの両方を提供する場合、破壊的なメソッドには`!`をつけましょう。
- それ以外で!を使用する場合は、メソッド作成者が利用者に対して、「あぶないぞー！！」っと意思表示したいときにつけましょう。

**正解**
```ruby
add_boy
pretty?
noripi?
dance
dance!
```

**誤り**
```ruby
addBoy
Add_Boy
is_noripi
was_noripi?
```

###### section3-3
### 定数名
クラス、モジュール名以外の定数名はすべて大文字とし、単語の区切りに'_'を用いるようにしましょう。

**正解**
```ruby
HONKY_TONKY_CRAZY_I_LOVE_YOU
```

###### section3-4
### 変数名
- 変数名は全て小文字とし、単語の区切りに'_'を用いるようにしましょう。
- また、スコープが狭いループ変数には、i,j,k という名前、スコープが狭い変数名は、クラス名を省略したものを使用してもオッケー！！！
- 気持ちはとてもわかりますが、hogeとか、fooとかやめときましょう。

- (例：eo = ExampleObjext.new

```ruby
tmp
local_variable
@instance_variable
$global_variable
```

###### section3-5
### シンボル
- アローは使用せずに書きましょう。

**正解**
```ruby
foo:1, bar:2
```

**誤り**
```ruby
:foo => 1, :bar => :2
```


###### section4
### ガイドライン

###### section4-1
### インデント
インデントは半角スペース２コ。ハードタブの使用は禁止です。あとで本当にきっついです。できる限りエディタでセットしておきましょう。

```ruby
__if girl > 0
____if girl.pefurme? > 0
______puts "ferver!!!!!"
____end
__end
```

###### section4-2
### コメント
- コメントは原則書かないように心がけましょう。それよりも書き手はコメントがなくても意図が伝わるようなコードを書くようにこころがけましょう。
- コーディング標準や規約に反する場合や、またプログラマー個人の意図がソースに介入している場所に限り、わかりやすいコメントを残すようにしましょう。
- プログラマーの腕のみせどころは、丁寧なコメントを多く書くことではなく、いかにわかりやすいコードを書くかです。よって、コメントを残す場合には「なにを」ではなく「なぜ」を書くようにしましょう。

###### section4-3
### メソッド定義
- 1) メソッド定義の場合は、引数がある場合は、()をつける
- 2) メソッドの呼び出しの場合は、読みやすさを重視する。

```ruby

# 1) の正解
def foo(x, y); end;

# 1) の誤り
def foo x, y; end;

# 2) の正解
obj.hoge 1, 2
obj.hoge(1, 2) &&  obj.hoge(3, 4)

# 2) の誤り
obj.hoge 1, 2 && obj.hoge obj.hoge(3, 4), 5 #=>単純に読みづらいので、()をつけよう
```

### 可変パラメータ //TODO:issue

###### section4-4
### ブロック
- ブロックは基本的にdo・・・endを使用しましょう。ただし１行の時は{}を使いましょう。
- またメソッドチェーンの場合も{}を使用しましょう。

**正解**
```ruby
foo(x,y) do
  ・・・
end

akb48.each{|a| a.dance!}

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
- if式のthenは省略しましょう。
- if!xのような場合は、unlessを使用しましょう。
- 条件が十分に簡単で、一行でかける場合は、修飾子として使ってもいいっす。
- 三項演算子も読みやすい範囲で使っていきましょう。

**正解**
```ruby
if self.perfume?
  puts "yes i am."
else
  puts "no i'm not."
end

unless self.perfume?
  puts "yes i am."
else
  
 i'm not."
end

puts "yes i am." if self.perfume?

puts self.perfume? ? "yes i am." : "no i'm not."

```

**誤り**
```ruby
if self.tashiro? then
  puts "yes i m."
end

puts "hoge" if foo && bar && baz && quux
```

**正解**
```ruby
case bust
when 80
  puts "fum fum"
when 96
  puts "hou hou"
end
```

**誤り**
```ruby
if bust == 80
  puts "fum fum"
elsif == 96
  puts "hou hou"
end

case bust
when 80 then
  puts "fum fum"
when 96 then
  puts "hou hou"
end
```

###### section4-6
### 繰り返し
- while の do は省略しましょう。
- while !x のような場合は、util x に置き換えましょう。 //TODO:ここ例題が正しいか検討が必要

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

- また、無限ループには loop を使用しましょう。

**正解**
```ruby
loop do
  puts "dance!dance!dance!"
end
```

**誤り**
```ruby
while true
  puts "dance!dance!dance!"
end
```

###### section4-7
### 例外
- 例外発生の基本方針はそれが「異常事態」かどうかで判断するようにしましょう。
- 明示的に例外を発生させないとプログラムが異常終了してしまう場合に使用しましょう。
- 例えば、ActiveRecord での save!メソッドは使わず、save メソッドを使用しましょう（バリデーションに引っかかるのは例外ではなく、想定された動作なので）。

### メソッドレベルでのensure
- //TODO: issue

###### section4-8
### ファイル
- ファイルの入出力は特別な事情がない限り、ファイルクローズなどの処理の記述忘れをしないためにも、ブロックを使いましょう。

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
  f.close #忘れる可能性あり！！
end
```

###### section4-9
### RubyGems
- Rails アプリで使用する gems は RAILS_ROOT/Gemfileに記述すること。
- 特に指示がない限りバージョンは明記しておくこと。

```ruby
gem 'rails', '3.2.12'
```

###### section4-10
### ERB::Util.html_escape //TODO:検討が必要
- Web アプリにおいて、出力文字列のエスケープは XSS に対する最も基本的な対処法です。
- Rails には ERB::Util.html_escape の alias である h ヘルパーが実装されています。
- 特別な事情がない限り View への文字列の出力には h ヘルパーを必ず使いましょう。

```ruby
<%= h @comment %>
```

###### section4-11
### メタプログラミング
- メタプログラミングをおこなう上では、運用/保守に入った際に他人が読んでもわかりやすいことを心がけるようにしましょう。

#### method_missing
superを使い、親のメソッドミッシングを呼び出すようにしましょう。
**正解**
```ruby
def method_missing(name)
  if @attributes.key? name
    #メソッドとしての処理
  else
    super
  end
end
```

**誤り**
```ruby
def method_missing(name)
  if @attributes.key? name
    # メソッドとしての処理
  end
  # 例外が発生しないため、わからないよー＞＜
end
```

- また、method_missingで追加したメソッドについては、下記の様にどのレベルまでrespond_to?に対応するかは都度チームで決定し拡張しましょう。
```ruby
def respond_to?(name)
  @attributes.key?(method) || super
end
```

//TOOD:issue
### eval
### class_eval
### instance_eval
### 特異メソッド
### クリーンルームの使用
### フラットスコープの使用
### コンテキスト探査機

###### section5
## データベース設計

###### section5-1
### データベース名
- development, product 環境ともに project_name で統一しましょう。
- test環境、またその他の環境に関しては project_name_environment で統一しましょう。

###### section5-2
### 日付型カラム名
- DATE型はカラム名を```*_on```とする。
- DATETIME型はカラム名を```*_at```とする。
- 作成日、更新日は```created_at```、```updated_at```とする。
- マイグレーションでt.timestampは利用しないこと。

```ruby
create_table :users do |t|

t.timestamp :moged_at # <= これはナシ
t.timestamp :ahoge_on # <= これはナシ

t.datetime :published_at
t.date :operated_on

t.timestamps # created_at, updated_at
end
```

###### section5-3
### タイプコードカラム名
//TODO:

###### section5-4
### booleanカラム名
//TODO:

###### section6
## テスト
- プロダクトコードに書く前に、テストコードを書きましょう。
- テストツールにはRSpecをつかいましょう。
- テストは自動化しましょう。

###### section7 //TODO:ここに必要か？＆内容を検討
## 原則
- プログラムの設計において先人たちの知恵を借りることは大事である。
- 盲目的に原則を信じるのではなく、「なぜ」かを意識すること。
- また様々な原則・デザインパターンの学習に努めること。

###### section7-1
### スコープは適切に
- スコープは限りなく狭くすること。
- 本当に必要だと思ったときのみ、グローバルなスコープを用いること。

###### section7-2
### DRY(Don't Your Self)
- 同じ処理を二度と書かないこと。

###### section7-3
### OCP(Open-Closed Principle)
- 拡張に対して開いていなければならず、修正に対して閉じていなければならない。
- 「拡張に対して閉じている」と言うのは、モジュールの拡張が可能ということでもあり、「修正に対して閉じている」と言うのは、モジュールの内部実装を修正してもそのインターフェースは安定しているということである。

###### section8
## 参考文献
- プログラミング言語Ruby[ISBN978-4-87311-394-4]
- 達人プログラマー[ISBN4-89471-274-1]
- プログラミング作法[ISBN4-7561-3649-4]
- Kenji Hiranabe, コーディング標準(オリジナル)
-- http://objectclub.esm.co.jp/eXtremeProgramming/CodingStd.doc
- Ruby コーディング規約
-- http://shugo.net/ruby-codeconv/codeconv.html

