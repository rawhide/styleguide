# RSpec

## ポイント
* describeを使いテストケースをグルーピングする
* contextを使い状態ごとにテストケースを書く
* subjectを使いテストの対象を明確にする(テストしたいものをsubjectにいれる)
* itに文字列を渡さない(DRYに)
* 重複したテストコードはshared_examplesでまとめる
* describe、context、itは基本英語で書く

## 基本

```
describe "テストする対象" do
  before(:all) do
    # 最初の1回だけ実行される
  end
 
  before(:each) do
    # 各テスト(it)のたびに実行される
  end

  context "テストする時の状況" do
    it { # テストケース1 }

    it { # テストケース2 }
  end
end
```

### describe メソッド
* テストする対象

```
describe User do # クラス,モジュール
describe ".method1" do # クラスメソッド
describe "#method2" do # インスタンスメソッド
```

### context メソッド
* テストする時の状況

```
context "empty" do # 空の場合
context "with login" do # ログインしている場合
```

### it メソッド
* テストの内容

```
it { expect(user).to be_valid }
```

## スタブ
* あるメソッドが呼ばれた時に特定の値を返して欲しい場合に使う
* [Object].stub(:[Method]).and_return([戻り値])

## モック
* メソッドがちゃんと呼ばれているかどうかをテストするために使う
* [Object].should_recieve(:[Method]).with([引数]).and_return([戻り値])

## テストデータの作り方

### spec内で使うデータ
```
let(:user) { FactoryGirl.build(:user)}
```

### DBのデータ
```
before { FactoryGirl.create(:user) }
```

## render_views

### 全体に設定する
```
＃ spec/spec_helper.rb

RSpec.configure do |config|
  config.render_views
end
```


### アクション毎に設定する

```
describe "GET index" do
  render_views
end
```