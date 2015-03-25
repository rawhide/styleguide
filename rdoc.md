# RDoc

## クラス

```ruby
#
# = ☆ クラスの概要
#
# ☆ クラスの説明
#
```

## メソッド

```ruby
#
# == ☆ メソッドの概要
#
# ☆ メソッドの説明
#
# === Examples
#
#   ☆ メソッドの使用例
#
# === Parameters
#
# [☆ 仮引数名 (☆ 仮引数の型)] ☆ 仮引数の説明
#
# === Returns
#
# [☆ 返り値の型] ☆ 返り値の説明
#
```

## 例

```ruby
#
# = MyClass is class
#
# MyClass is my class.
# MyClass is my class.
# MyClass is my class.
#
class MyClass
  #
  # == my_method is method
  #
  # my_method is my method.
  #
  # === Examples
  #
  #   my = MyClass.new
  #   my.my_method :activate, force: true
  #
  # === Parameters
  #
  # [type (String|Symbol)] メソッドのタイプ
  # [options (Hash)] オプション。任意。
  #
  # === Returns
  #
  # [String] 処理結果を返します。
  #
  def my_method(type, options)
     ...
    'done'
  end

  #
  # === Returns
  #
  # [Array[String]] 処理結果を配列で返します。
  #
  def my_method2
    ['return1', 'return2']
  end
end
```
