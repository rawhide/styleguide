# Table of Contents

* [ルーティング](#section-1)
  * [member/collection ルーツ](#section-1-1)
* [コントローラー](#section-2)
  * [責務](#section-2-1)
  * [命名規則](#section-2-2)
  * [Flash](#section-2-3)
  * [ファイルのダウンロード](#section-2-4)
* [モデル](#section-3)
  * [命名規則](#section-3-1)
  * [定義順序](#section-3-2)
  * [バリデーション](#section-3-3)
    * [Sexy Validation](#section-3-3-1)
    * [カスタムバリデーション](#section-3-3-2)
  * [scope](#section-3-4)
* [ビュー](#section-4)
  * [ファイルレイアウト](#section-4-1)
  * [部分テンプレート](#section-4-2)
* [ヘルパー](#section-5)
* [マイグレーション](#section-6)
  * [命名規則](#section-6-1)
* [Mailer](#section-7)
  * [命名規則](#section-7-1)
* [サービスクラス](#section-8)
  * [命名規則](#section-8-1)
* [フォームクラス](#section-9)
  * [命名規則](#section-9-1)
* [Gem](#section-100)

<a name="section-1"></a>
# ルーティング

<a name="section-1-1"></a>
## member/collection ルーツ

* RESTfulリソースに対してアクションを追加する場合は member および collection を使用します。

```ruby
# bad
resources :users
get 'users/search'
patch 'users/:id/activate'

# good
resources :users do
  get 'search', on: :collection
  patch 'activate', on: :member
end
```

* 複数の member/collection ルーツが存在する場合はブロックを使いましょう。

```ruby
resources :users do
  collection do
    get 'search'
    ...
  end

  member do
    patch 'activate'
    ...
  end
end
```

<a name="section-2"></a>
# コントローラー

* ビジネスロジックを書かないようにしましょう。
* 独自アクションを増やし過ぎないようにしましょう。コントローラーが増えるのは悪いことではないです。
* アクション以外のメソッドはprivateメソッドにしましょう。

<a name="section-2-1"></a>
## 責務

* ビューのレンダリング。
* ビューに渡すインスタンス変数の設定。
* モデルの処理の呼び出し。

<a name="section-2-2"></a>
## 命名規則

コントローラー名(ここではControllerは除く)は複数形にしましょう。

<a name="section-2-3"></a>
## Flash

### 現在のリクエストでのみ有効なメッセージを設定する場合

```ruby
# renderの場合に使いましょう。
flash.now[:notice]
```

### 次のリクエストまで有効なメッセージを設定する場合

```ruby
# redirect_toの場合に使いましょう。
flash[:notice]
# 以下のような書き方もできます。
redirect_to root_url, notice: 'message'
```

<a name="section-2-4"></a>
## ファイルのダウンロード

* 既に存在するファイルをダウンロードさせる場合は **send_file** を使いましょう
* 動的に生成したデータ(文字列等)をダウンロードさせる場合は **send_data** を使いましょう

<a name="section-3"></a>
# モデル

<a name="section-3-1"></a>
## 命名規則

モデル名は単数形にしましょう。

<a name="section-3-2"></a>
## 定義順序

モデル内では以下の様な順序でメソッド等を定義するようにしましょう。

```ruby
class User < ActiveRecord::Base
  GENDER = %w(male female)

  attr_accessor :full_name

  # associations
  belongs_to :country
  has_one :profile
  has_many :favorites

  has_many :memberships
  has_many :groups, through: :memberships

  accepts_nested_attributes_for :profile

  # validations
  validates :email, presence: true

  scope :active, -> do
    where(status: :active)
  end

  # callbacks
  before_save :hash_password

  # class methods
  def self.my_classmethod
  end

  # public methods
  def my_public_method
  end

  # private methods
  private

    def my_private_method
    end
end
```

<a name="section-3-3"></a>
## バリデーション

<a name="section-3-3-1"></a>
### Sexy Validation

Sexy Validationを使用するようにしましょう。

```ruby
# bad
validates_presence_of :name
# good
validates :name, presence: true
```

<a name="section-3-3-2"></a>
### カスタムバリデーション

* 独自バリデーションが2つ以上ある場合はカスタムバリデーションにしましょう。
* クラス名は「XxxValidator」、ファイル名は「app/validators/xxx_validator.rb」にしましょう。

```ruby
# bad
class User
  validates :email, format: { with: /\A([^@\s]+)@((?:[-a-z0-9]+\.)+[a-z]{2,})\z/i }
end
class Company
  validates :email, format: { with: /\A([^@\s]+)@((?:[-a-z0-9]+\.)+[a-z]{2,})\z/i }
end

# good
class EmailValidator < ActiveModel::EachValidator
  def validate_each(record, attribute, value)
    record.errors[attribute] << (options[:message] || 'is not a valid email') unless value =~ /\A([^@\s]+)@((?:[-a-z0-9]+\.)+[a-z]{2,})\z/i
  end
end

class User
  validates :email, email: true
end
class Company
  validates :email, email: true
end
```

<a name="section-3-4"></a>
## scope

遅延初期化のためにscopeではlambdaを使うようにしましょう。

```ruby
# ng
scope :active, where(active: true)
# ok
scope :active, lambda { where(active: true) } # lambda 記法
# good
scope :active, -> { where(active: true) } # lambda の新しい記法
```

<a name="section-4"></a>
# ビュー

* 重複コードがある場合はパーシャルやレイアウトを使うようにしましょう。

<a name="section-4-1"></a>
## ファイルレイアウト

* app/views/layouts はレイアウトファイルのみを入れましょう。
* 全体を通して使用するレイアウトファイルは application.html.erb という名前で作成しましょう。


<a name="section-4-2"></a>
## 部分テンプレート

* コントローラーをまたぐ部分テンプレートは app/views/shared に配置するようにしましょう。

<a name="section-5"></a>
# ヘルパー

* グローバルにアクセスできるメソッドを定義してしまうので使わないようにしましょう。
* ページタイトルやナビゲーションなどの用途では使ってもよいです。

<a name="section-6"></a>
# マイグレーション

* schema.rbはgit管理しましょう。
* CI連携プロジェクト、本番稼働しているプロジェクトではコミット済みのマイグレーションファイルを直接編集してはいけません。カラムを変更、追加する場合は、新しくマイグレーションクラスを作成しましょう。
* マイグレーションファイル内ではモデルクラスを使用してはいけません。モデルは常に変更され続けています。
* up、downメソッドの代わりに、changeメソッドを使用しましょう。

```ruby
# ok
class AddAgeToUsers < ActiveRecord::Migration
  def up
    add_column :users, :age, :integer
  end

  def down
    remove_column :users, :age
  end
end

# better
class AddAgeToUsers < ActiveRecord::Migration
  def change
    add_column :users, :age, :string
  end
end
```

<a name="section-6-1"></a>
## 命名規則

| 種別 | クラス名 | ケース |
|-----|-----------|----|
| テーブル作成 | CreateUsers | usersテーブルを作成する場合 |
| テーブル削除 | DropUsers | usersテーブルを削除する場合 |
| カラム追加 | AddAgeToUsers | usersテーブルにageカラムを追加する場合 |
| カラム削除 | RemoveAgeFromUsers | usersテーブルからageカラムを削除する場合 |
| カラム名変更 | RenameFromSexToGenderOnUsers | usersテーブルのsexカラムをgenderカラムに変更する |
| カラム情報変更 | ChangeAuthenticationColumnsOnUsers | usersテーブルの認証系のカラムを変更する場合 |
| INDEX作成 | AddIndexesToUsers | usersテーブルにインデックスを作成する場合 |
| INDEX作成 | AddIndexTokenToUsers | usersテーブルにtokenカラムのインデックスを作成する場合 |
| INDEX削除 | RemoveIndexTokenFromUsers | usersテーブルのtokenカラムのインデックスを削除する場合 |
| VIEW作成 | CreateActivityView | Activityビューを作成する場合 |
| VIEW再作成 | RepaireActivityView | Activityビューを作り直す場合 |


<a name="section-7"></a>
# Mailer

<a name="section-7-1"></a>
## 命名規則

クラス名は「XxxMailer」、ファイル名は「app/mailers/xxx_mailer.rb」にしましょう。

<a name="section-8"></a>
# サービスクラス

* 以下に当てはまる場合はサービスクラスを使うようにしましょう。
  - 複数テーブルに対してInsert/Updateが発生する場合。
  - DB登録、外部システムとの連携を同時に行う場合。
* [service_generator](https://github.com/rawhide/service_generator) gem を使いましょう。

<a name="section-8-1"></a>
## 命名規則

クラス名は「XxxService」、ファイル名は「app/services/xxx_service.rb」にしましょう。

<a name="section-9"></a>
# フォームクラス

* 複雑なパラメータの加工、画面のみのバリデーションがある場合はフォームクラスを使うようにしましょう。
* [form_generator](https://github.com/rawhide/form_generator) gem を使いましょう。

<a name="section-9-1"></a>
## 命名規則

クラス名は「XxxForm」、ファイル名は「app/forms/xxx_form.rb」にしましょう。

<a name="section-100"></a>
# Gem

gemを探すときは [https://www.ruby-toolbox.com/](https://www.ruby-toolbox.com/) を参考にしましょう。

* ユーザ認証
  - [devise](https://github.com/plataformatec/devise) - 必要なものはだいたい用意されています。
  - [authlogic](https://github.com/binarylogic/authlogic) - シンプル。
* 検索
  - [ransack](https://github.com/activerecord-hackery/ransack) - 検索機能を実装するためのgemです。
* ページネーション
  - [kaminari](https://github.com/amatsuda/kaminari) - これ一択。
* ファイルアップロード
  - [carrierwave](https://github.com/carrierwaveuploader/carrierwave)
* 定数管理
  - [settingslogic](https://github.com/binarylogic/settingslogic)
* Enum管理
  - [code_holder](https://github.com/rawhide/code_holder)
  - [enumerize](https://github.com/brainspec/enumerize)
* application server
  - [unicorn](https://github.com/defunkt/unicorn) - 重い。
  - [passenger](https://github.com/phusion/passenger) - Apache、Nginxを再コンパイルしないといけません。
* エラー管理
  - [airbrake](https://github.com/airbrake/airbrake)
* 単体テスト
  - [rspec-rails](https://github.com/rspec/rspec-rails)
  - [database_cleaner](https://github.com/DatabaseCleaner/database_cleaner)
  - [factory_girl_rails](https://github.com/thoughtbot/factory_girl_rails)
  - [fuubar](https://github.com/thekompanee/fuubar) - テストの進捗状況を可視化してくれます。
* パフォーマンス・チューニング
  - [rack-mini-profiler](https://github.com/MiniProfiler/rack-mini-profiler)
* 権限管理
  - [cancancan](https://github.com/CanCanCommunity/cancancan) - 権限を行うgemです。
* API
  - [grape](https://github.com/intridea/grape) - RESTful な API を生成するためのマイクロフレームワークです。
  - [grape-entity](https://github.com/intridea/grape-entity) - JSONフォーマットを実装することができます。
* 管理画面
  - [rails_admin](https://github.com/sferik/rails_admin) - 管理画面を自動生成してくれます。
* 非同期処理
  - [sidekiq](https://github.com/mperham/sidekiq) - 非同期処理を行うgemです。バックエンドにRedisが必要です。
  - [delayed_job](https://github.com/collectiveidea/delayed_job) - 非同期処理を行うgemです。バックエンドはRDBMS、MongoDB、Redisなどが選択可能です。
* テンプレートエンジン
  - [haml-rails](https://github.com/indirect/haml-rails) - HTML/XHTMLを生成するためのマークアップ言語です。
  - [slim-rails](https://github.com/slim-template/slim-rails)  - Hamlとほとんど同じです。
* アセット
  - [sass-rails](https://github.com/rails/sass-rails) - CSSを楽にかける拡張言語です。
* 狀態遷移
  - [state_machine](https://github.com/pluginaweek/state_machine)
* 論理削除
  - [paranoia](https://github.com/radar/paranoia)
