学んだこと

# Objectクラス
equal?
  同一オブジェクトであればtrue、オブジェクトIDが異なる場合はfalseを返す。
eql? ==
  オブジェクトIDはチェックしない

# Integerクラス
upto
  引数を1ずつ増やした数を順番に配列として返す。


# Stringクラス
strip, strip!
  文字列の先頭と末尾の空白文字を取り除く。
chomp
  末尾の改行コードを取り除く。
chop
  末尾の文字を取り除く。\r\nなら2文字とも取り除く。
sub
  一つ目を2つ目に置き換えた文字列を返す。
  最初に見つけた文字列だけを置き換え。
scan
  引数で指定したパターンにマッチした部分を配列で返す。複数あれば全てを。
delete delete!
  引数に指定した文字を削除
concat
  レシーバと引数を結合。破壊的
index
  一つ目の文字を二つ目の引数位置から探し、最初に見つけた位置を返す。


# Arrayクラス
shift
  先頭の要素を破壊的に取り出す。引数があればその数だけ取り出し、配列で返す。
  なければnilを返す。
unshift prepend
  先頭に値を破壊的に追加する。引数がなければ何もしない。
pop
  末尾から要素を取り除いて返す。引数があればその数だけ取り出し、配列で返す。
push
  末尾に追加する。引数がなければ何もしない。
compact compact!
  nilを取り除くメソッド。
flatten flatten!
  再帰的に平坦化する。平坦化が行わなければnilを返す。
product
  レシーバの配列と引数の配列から一つずつ要素を取り出し、新しい配列を作成する。
  レシーバの要素を起点とする。
transpose
  レシーバの配列を元に、行と列を入れ替えた配列を作り、返す。
  https://docs.ruby-lang.org/ja/latest/method/Array/i/transpose.html
partition
  ブロックの要素を満たす部分、満たさない部分に分割し、
  真の配列と偽の配列を二つに分けて返す。
delete
  引数で指定した値を等しい要素を全て削除する。削除した場合は削除した要素を、そうでなければnilを返す。
delete_if reject!
  ブロックを渡し、真の要素を全て削除する。
  delete_ifは常にselfを返す。reject!は削除しなければnilを返す。
upcase upcase!
  大文字


# Hashクラス
to_a
  キーと値を2要素の配列に並べた配列を返す。
  h = {a: 100, b: 200}
  h.to_a  // [[:a, 100], [:b, 200]]
values_at
  指定したキーの値を配列で返す。
member?
  指定したキーを持つか否かtrue/false
update
  指定した内容へ更新
clear
  ハッシュの中身を空にする。破壊的メソッド。

# Enumerableクラス
collect map
  ブロックの結果をまとめた配列を返す。
select filter select! fileter! find_all
  該当する全ての要素を配列にして返す。真がなければ空配列を返す。
find
  ブロックの条件に一致する最初の要素を返す。

# IOクラス
.read 第1引数で読み込むファイル、2で文字数、3で開始位置。

# 演算子の優先度
論理演算子は低い。算術演算子は高い。
== よりも || の方が低い。
https://docs.ruby-lang.org/ja/2.1.0/doc/spec=2foperator.html

# 可変長引数
*aはArrayクラスのオブジェクトを返す。
2つ定義することはできない。以下はsyntax errorとなる。
def bar(*n1, n2, *n3)
  puts n1
  puts n2
end

bar 5, 6, 7, 8

なお、関数を呼び出すときの引数に()は不要。

# Dateクラス
strftime 引数は一つだけ。
  %F %Y-%m-%d 2024-04-14 Date.today.to_s
  %m month
  %M Minute
  %d date
  %D datetime %m/%d/%y
  %y 下２桁
  %Y 4桁

# 進数
16進数は0xから始まる。0~Fで表現。それ以外は例外エラー
8進数は0から始まり0~7


seek

File
chmod モード変更
dirname ディレクトリの名前を返す。
delete ファイル削除

rescueに例外クラスの指定がなければStandardErrorのサブクラスを全て補足する。