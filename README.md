## Table of Contents
* [基本方針](#section-0)
  * [概要](#section-0-0)
  * [目的](#section-0-1)
  * [使い方](#section-0-2)
  * [見て読みやすく](#section-0-3)
  * [読んで解りやすく](#section-0-4)
  * [スコープは適切に](#section-0-5)
  * [DRY(Don't Your Self)](#section-0-6)
  * [OCP(Open-Closed Principle)](#section-0-7)
  * [一般的に多く使われているrubyistにまねる](#section-0-8)
  * [変化を受け入れろ！](#section-0-9)
* [ファイル](#section-1)
  * [概要](#section-1-0)
  * [ファイルレイアウト](#section-1-1)
  * [部分テンプレート](#section-1-2)
* [命名規約](#section-2)
  * [概要](#section-2-0)
  * [クラス・モジュール名](#section-2-1)
* [命名規則](#section-3)
  * [メソッド名](#section-3-0)
      * [自己破壊メソッド](#section-3-0-0)
  * [定数名](#section-3-1)
  * [変数名](#section-3-2)
  * [シンボル](#section-3-3)
* [ガイドライン](#section-4)
  * [インデント](#section-4-0)
  * [コメント](#section-4-1)
  * [代入](#section-4-2)
  * [文字列](#section-4-3)
  * [メソッド定義](#section-4-4)
  * [可変パラメータ](#section-4-5)
  * [ブロック](#section-4-6)
  * [条件分岐](#section-4-7)
  * [繰り返し](#section-4-8)
  * [例外](#section-4-9)
  * [メソッドレベルでのensure](#section-4-10)
  * [ファイル](#section-4-11)
  * [RubyGems](#section-4-12)
  * [メタプログラミング-概要](#section-4-13)
  * [メタプログラミング-method_missing](#section-4-14)
  * [return](#section-4-15)
  * [self](#section-4-16)
  * [Symbol.to_procの活用（Ruby1.9）](#section-4-17)
  * [lambdaとprocの活用 (使い分け)](#section-4-18)
  * [例外のrescueの使い方](#section-4-19)
* [データベース設計](#section-5)
  * [データベース名](#section-5-0)
  * [日付型カラム名](#section-5-1)
  * [タイプコードカラム名](#section-5-2)
  * [booleanカラム名](#section-5-3)
* [テスト](#section-6)
  * [概要](#section-6-0)
* [参考文献](#section-7)
  * [一覧](#section-7-0)

##### section-0
## 基本方針
##### section-0-0
### 概要
- レディーに悲しい思いはさせない。
- 食べ物や包丁を武器につかわない。

##### section-0-1
### 目的
- 「読みやすくメンテナンスしやすいコードを書く」ことの価値観をチームで共有できる。
- コーディング規約という共通基盤を通して、プログラマーのスキルアップをはかることができる。

##### section-0-2
### 使い方
- 異臭をはなつ部分は、issueで議論しましょう。決まったものからこちらに移していきましょう。
- 場合によってはこの規約から外れることも時には重要であり、その際はなにかしらの説明を用意するようにしましょう。

##### section-0-3
### 見て読みやすく
- 見て読みやすく



##### section-0-4
### 読んで解りやすく
- 読んで解りやすく



##### section-0-5
### スコープは適切に
- スコープは限りなく狭くすること。
- 本当に必要だと思ったときのみ、グローバルなスコープを用いること。



##### section-0-6
### DRY(Don't Your Self)
- 同じ処理を二度と書かないこと。



##### section-0-7
### OCP(Open-Closed Principle)
- 拡張に対して開いていなければならず、修正に対して閉じていなければならない。
- 「拡張に対して閉じている」と言うのは、モジュールの拡張が可能ということでもあり、「修正に対して閉じている」と言うのは、モジュールの内部実装を修正してもそのインターフェースは安定しているということである。



##### section-0-8
### 一般的に多く使われているrubyistにまねる
- プログラムの設計において先人たちの知恵を借りることは大事である。
- 盲目的に原則を信じるのではなく、「なぜ」かを意識すること。
- また様々な原則・デザインパターンの学習に努めること。



##### section-0-9
### 変化を受け入れろ！
- 変化を受け入れろ！




##### section-1
## ファイル
##### section-1-0
### 概要
- 以下は Rails プロジェクトにおいてのルールである。基本的には Rails のルールにしたがうようにしましょう。

##### section-1-1
### ファイルレイアウト
- RAILS_ROOT/app/views/layouts はレイアウトファイルのみを入れましょう。
- 全体を通して使用するレイアウトファイルは application.html.erb という名前で作成しましょう。

##### section-1-2
### 部分テンプレート
- コントローラにまたがる部分テンプレートは RAILS_ROOT/app/views/share に配置するようにしましょう。


##### section-2
## 命名規約
##### section-2-0
### 概要
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

##### section-2-1
### クラス・モジュール名
- クラス、モジュール名は、各単語の一文字めを大文字にし、'_'などの区切り文字は使用しません。
- TPPなどの略語の場合は全て大文字のままにしましょう（省略してるよーって意味が伝わるように）。
- 例外クラスでは特別な事情がない限り末尾に「Error」をつけましょう。
- よほどの意図がない限り、複数名を使用するはやめましょう。

```ruby
#正解
NurseCall
TTPClient
AKBMember
OreOreError

#誤り
Nurse_Room
TPP_CLIENT
AKBMembers
CsvReader
```


##### section-3
## 命名規則
##### section-3-0
### メソッド名
- メソッド名は、全て小文字とし単語の区切りに_をつかいましょう。
- 真偽値を返すメソッド名は、動詞または形容詞に?を付けましょう。
- 破壊的なメソッドと非破壊的なメソッドの両方を提供する場合、破壊的なメソッドには!をつけましょう。
- それ以外で!を使用する場合は、メソッド作成者が利用者に対して、「あぶないぞー！！」っと意思表示したいときにつけましょう。

```ruby
#正解
add_boy
pretty?
noripi?
dance
dance!

#誤り
addBoy
Add_Boy
is_noripi
was_noripi?
```
##### section-3-0-0
#### 自己破壊メソッド

- 例外発生や、自己の状態を書き換える場合は、積極的にエクスクラメーションを使いましょう。

```ruby
#例)
def make_hoge!
  self.foo= "hoge"
end
```
メソッド名には、使うときに注意が必要だということを示すために、末尾に感嘆符をつけることができる。
この命名習慣は、オブジェクト自身を破壊的に書き換えるミューテータメソッドと下のオブジェクトのコピーに変更を加えたものを返すメソッドとを区別するために使われることが多い




##### section-3-1
### 定数名
- クラス、モジュール名以外の定数名はすべて大文字とし、単語の区切りに'_'を用いるようにしましょう。

```ruby
#正解
HONKY_TONKY_CRAZY_I_LOVE_YOU
```

##### section-3-2
### 変数名
- 変数名は全て小文字とし、単語の区切りに'_'を用いるようにしましょう。
- スコープが狭いループ変数には、i,j,k という名前、スコープが狭い変数名は、クラス名を省略したものを使用してもオッケー！！！
- 気持ちはとてもわかりますが、hogeとか、fooとかやめときましょう。

```ruby
#(例：eo = ExampleObjext.new

tmp
local_variable
@instance_variable
$global_variable
```

##### section-3-3
### シンボル



##### section-4
## ガイドライン
##### section-4-0
### インデント
- インデントは半角スペース２コ。ハードタブの使用は禁止です。あとで本当にきっついです。できる限りエディタでセットしておきましょう。

```ruby
__if girl > 0
____if girl.pefurme? > 0
______puts "ferver!!!!!"
____end
__end
```

##### section-4-1
### コメント
- コメントは原則書かないように心がけましょう。それよりも書き手はコメントがなくても意図が伝わるようなコードを書くようにこころがけましょう。
- コーディング標準や規約に反する場合や、またプログラマー個人の意図がソースに介入している場所に限り、わかりやすいコメントを残すようにしましょう。
- プログラマーの腕のみせどころは、丁寧なコメントを多く書くことではなく、いかにわかりやすいコードを書くかです。よって、コメントを残す場合には「なにを」ではなく「なぜ」を書くようにしましょう。

##### section-4-2
### 代入
- 代入に規制はないが、読みやすさを重視して書きましょう。

```ruby
#正解
a = 'hoge' 
a ||= 'moge' 
a ||= true ? 'foo' : 'bar'

#誤り
a = 1 if a.nil? #×冗長なので×
```


##### section-4-3
### 文字列

-

```ruby
#いい例
"#{i}さん、#{b}さん、#{a}さん"

#いい例)ダブルクオート
%(#{i}さん、#{t}さん、#{o}さん、"ITO")

#悪い例
i + "さん、" + b + ”さん、" + a + "さん"
```



##### section-4-4
### メソッド定義
- メソッドの定義の仮引数リストには括弧を付けるようにしましょう。
- 引数がない場合は、括弧をつけないようにしましょう。

```ruby
#正解
def foo(x, y)
  ・・・
end

#誤り
def foo x, y
  ・・・
end

def foo()
  ・・・
end
```

##### section-4-5
### 可変パラメータ


##### section-4-6
### ブロック
- ブロックは基本的にdo・・・endを使用しましょう。ただし１行の時は{}を使いましょう。
- またメソッドチェーンの場合も{}を使用しましょう。

```ruby
#正解
foo(x,y) do
  ・・・
end

akb48.each{|a| a.dance!}

bar.map{|i| i.to_s}.each{|i| puts i}

#誤り
foo(x,y) {
  ・・・
}

foo.map do |i|
  i.to_s
end.each do |i|
  puts i
end
```

##### section-4-7
### 条件分岐
- if式のthenは省略しましょう。
- if !xのような場合は、unlessを使用しましょう。
-  unlessのelseは、ifを使う。unlessは、ifのelseを使う。
- 条件が十分に簡単で、一行でかける場合は、修飾子として使ってもいい。
- 三項演算子も読みやすい範囲で使っていきましょう。

```ruby
#正解
if self.perfume?
  "yes i am."
else
  "no i'm not."
end

# 1行で書けるときのみ
p 'present' unless hoge.blank?

puts "yes i am." if self.perfume?

puts self.perfume? ? "yes i am." : "no i'm not."

#誤り
if self.tashiro? then
  puts "yes i m."
end

unless hoge.blank?
  p 'present'
else
  p 'blank'
end

puts "hoge" if foo && bar && baz && quux

#正解
case bust
when 80
  puts "fum fum"
when 96
  puts "hou hou"
end

#誤り
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
when 120 then
  puts "haa haa"
end
```

##### section-4-8
### 繰り返し
while の do は省略しましょう。
while !x のような場合は、util x に置き換えましょう。 

```ruby
#正解
while cond
  puts "puts is false"
end

util cond
  puts "cond is false"
end

#誤り
while cond do
  puts "cond is true"
end
```

また、無限ループには loop を使用しましょう。

```ruby
#正解
loop do
  puts "dance!dance!dance!"
end

#誤り
while true
  puts "dance!dance!dance!"
end
```

##### section-4-9
### 例外
- 例外発生の基本方針はそれが「異常事態」かどうかで判断するようにしましょう。
- 明示的に例外を発生させないとプログラムが異常終了してしまう場合に使用しましょう。
- 例えば、ActiveRecord での save!メソッドは使わず、save メソッドを使用しましょう（バリデーションに引っかかるのは例外ではなく、想定された動作なので）。

##### section-4-10
### メソッドレベルでのensure


##### section-4-11
### ファイル
- ファイルの入出力は特別な事情がない限り、ファイルクローズなどの処理の記述忘れをしないためにも、ブロックを使いましょう。

```ruby
#正解
open("sample.txt", "r") do |f|
  puts f.gets
end

#誤り
begin
  f = open("sample.txt", "r")
  puts f.gets
ensure
  f.close #忘れる可能性あり！！
end
```

##### section-4-12
### RubyGems
- Rails アプリで使用する gems は RAILS_ROOT/Gemfileに記述すること。
- 特に指示がない限りバージョンは明記しておくこと。
- gem 'rails', '3.2.12'

##### section-4-13
### メタプログラミング-概要
- メタプログラミングをおこなう上では、運用/保守に入った際に他人が読んでもわかりやすいことを心がけるようにしましょう。

##### section-4-14
### メタプログラミング-method_missing
- superを使い、親のメソッドミッシングを呼び出すようにしましょう。 

```ruby
#正解
def method_missing(name)
  if @attributes.key? name
    #メソッドとしての処理
  else
    super
  end
end

#誤り
def method_missing(name)
  if @attributes.key? name
    # メソッドとしての処理
  end
  # 例外が発生しないため、わからないよー＞＜
end
```

また、method_missingで追加したメソッドについては、下記の様にどのレベルまでrespond_to?に対応するかは都度チームで決定し拡張しましょう。 ruby def respond_to?(name) @attributes.key?(method) || super end

##### section-4-15
### return

- 必要のあるreturnは書く。（redirect_toとか）
- 必要のないreturnは省略しても良い。

```ruby
#普通のruby

#推奨)
class Gay
  def say
     "I was gay"
  end
end

#非推奨)
class Gay
  def say
     return "I was gay"
  end
end

#Railsのcontrollerの場合...

#推奨)
class HogesController < ApplicationController
  def index
     redirect_to piyos_path and return
  end
end

class HogesController < ApplicationController
  def index
     redirect_to piyos_path
     return
  end
end

#非推奨)
class HogesController < ApplicationController
  def index
     redirect_to piyos_path
  end
end
```

redirect_to の後の return は基本的に書かなくても大丈夫だが、2重に return される時があるので、書いたほうが良い。



##### section-4-16
### self

- インスタンス変数には@をつける。
- インスタンスメソッドにはself.をつける。

```ruby
# 例)
class Hoge
  attr_accessor :title

  def hoge
    #ローカル変数
    title = 'hoge'
    puts title #=> hoge

    #インスタンス変数(attr_accessor)
    self.title = 'moge'
    puts self.title #=> moge
    puts title #=> hoge

    #インスタンス変数(attr_accessor)
    @title = 'foo'
    puts @title #=> foo
    puts self.title #=> foo

    #メソッドの場合
    pp = 'pp'
    pp  #変数ppが評価される
    self.pp #=> oo メソッドppが評価される
  end

  def pp
    puts 'oo'
  end
end
```



##### section-4-17
### Symbol.to_procの活用（Ruby1.9）

- to_proc相当の機能は、Ruby 1.9 ではSymbolクラスへと統合されました。

```ruby
#正解)　どちらも読みやすい
words.map &:upcase
words.map(&:upcase)  

#誤り）わかりずらい（と、いうかエラー）
words.map &:upcase + words.map &:capitalize

#従来）
words.map{|w| w.upcase} + words.map{|w| w.capitalize} 

# 例)だんぜん読みやすくなりました！）
words.map(&:upcase) + words.map(&:capitalize)

#従来
sum = points.inject(0) {|sum, i| sum+i}
#to_sym
sum = points.inject(0, &:+)
```



##### section-4-18
### lambdaとprocの活用 (使い分け)

- procよりもlambdaを積極的に使う
- lambdaリテラルを使う
- 下記の点で、できればlambdaを使う様にしましょう！

１）引数に厳格（ArgmentErrorを投げる）
２）returnがメソッドと同じ感覚で使える（LocalJumpErrorを投げない）

```ruby
#引数の扱いの違い
a = lambda do |x,y|
end

b = proc do |x,y|
end

a.call #アウト（メソッド定義に近い）
b.call #セーフ（よろしくやってくれる）

#returnの違い
def hoge
p = proc { return }
p.call
p 'hoge' #LocalJumpError procのリターンはhogeメソッドから出てしまうため、この行は実行されない。
end

def hoge
p = lambda { return }
p.call
p. 'hoge' #lambdaのリターンはブロックからのリターンのため、この行は実行される。
end

#1.9以降のラムダリテラル
a = ->(x,y) do
end

#x,y=引数 i,n=ローカル変数定義
a = ->(x,y; i=0) do
end

#1.9以降procの呼び出し方法
f.call(x,y) #今まで通り
f[x,y]
f.(x,y)
```



##### section-4-19
### 例外のrescueの使い方

- rescueを使う時は、何をキャッチしているのかを明確にするため、例外オブジェクトを明記する。

```ruby
#正解
def moge
  raise HogeError
rescue HogeError
  puts $!
end

#もっと正解)基本的にはこちらを使用しましょう。
def foo
  raise HogeError
rescue HogeError => ex
  puts ex
end

#誤り
def hoge
  raise HogeError
rescue
  puts $!
end
```




##### section-5
## データベース設計
##### section-5-0
### データベース名
- development, product 環境ともに project_name で統一しましょう。
- test環境、またその他の環境に関しては project_name_environment で統一しましょう。

##### section-5-1
### 日付型カラム名
- DATE型はカラム名を*_onとする。
- DATETIME型はカラム名を*_atとする。
- 作成日、更新日はcreated_at、updated_atとする。
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

##### section-5-2
### タイプコードカラム名


##### section-5-3
### booleanカラム名



##### section-6
## テスト
##### section-6-0
### 概要
- プロダクトコードに書く前に、テストコードを書きましょう。
- テストツールにはRSpecをつかいましょう。
- テストは自動化しましょう。


##### section-7
## 参考文献
##### section-7-0
### 一覧
- プログラミング言語Ruby[ISBN978-4-87311-394-4]
- 達人プログラマー[ISBN4-89471-274-1]
- プログラミング作法[ISBN4-7561-3649-4]
- Kenji Hiranabe, コーディング標準(オリジナル) -- http://objectclub.esm.co.jp/eXtremeProgramming/CodingStd.doc
- Ruby コーディング規約 -- http://shugo.net/ruby-codeconv/codeconv.html



