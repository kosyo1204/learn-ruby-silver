# Objectクラス
equal?
  同一オブジェクトであればtrue、オブジェクトIDが異なる場合はfalseを返す。
eql? ==
  オブジェクトIDはチェックしない

# Integerクラス
プレフィックス
  0b: 2進数
  0 or 0o: 8進数
  0d or 指定なし: 10進数
  0x: 16進数
  プレフィックスの後に存在し得ない数値を指定すると、エラーを返す。
to_s
  引数を指定すると、基数とした文字列を返す。
  7.to_s(3) → '21'
upto
  引数を1ずつ増やした数を順番に配列として返す。

# Numericクラス
step(limit, step)
  stepずつ加算、limitまで。

# Stringクラス
to_i
  nilは0
  引数なし: 10進数表現された数字として解釈し、変換できるまでを変換対象とする。
    "0b0001".to_i -> 0
  引数あり: 0~36を指定できる。0を指定すれば、先頭のプレフィックスから基数を判断する。
    irb(main):069:0>   "0b1".to_i(0)
    => 1
    irb(main):070:0>   "0bb1".to_i(0)
    => 0
配列に変換したいとき
  to_aメソッドはない。
    splitやcharsメソッドを使用する。
oct
  文字列を8進数で解釈し、整数で返す。
  8進数で解釈できない場合は0で返す。
  接頭辞が2や16進数なら応じた値へ変換する。
  '80'.oct -> 0
  '70'.oct -> 56
  '10'.oct -> 8
  '0x10'.oct -> 16
hex
  文字列を16進数で解釈。解釈できないときはoct同様、0で返す。
strip, strip!
  文字列の先頭と末尾の空白文字を取り除く。
chomp
  末尾の改行コードを取り除く。非破壊的
chop
  末尾の文字を取り除く。\r\nなら2文字とも取り除く。非破壊的
sub sub!
  一つ目を2つ目に置き換えた文字列を返す。最初に見つけた文字列だけを置き換え。
  破壊的なメソッドではない。置換したものを代入していれば更新される。
scan
  引数で指定したパターンにマッチした部分を配列で返す。複数あれば全てを。
delete delete!
  引数に指定した文字を削除
concat <<
  レシーバと引数を結合。破壊的
index
  一つ目の文字を二つ目の引数位置から探し、最初に見つけた位置を返す。
  0の指定は可能。
  index("r", 1) 1文字目から探す。
  irb(main):015:0> a.index('R', 3)
  => 4
  irb(main):016:0> a.index('R', 4)
  => 4
  irb(main):017:0> a.index('R', 5)
  => 12
split
  指定した文字で区切る。()を含んで指定すると、区切る文字も含めて返す。
  "Spring,Summer,Autumn,Winter".split(/(,)/)
  → ["Spring", ",", "Summer", ",", "Autumn", ",", "Winter"]とカンマを含めて分解されます。
*
  引数の数だけ繰り返す。
%
  フォーマットされた文字列を返す。指示子が引数の値で置換される。
  %dは10進数で数値を出力する。
  指示子がなければそのまま返す。
  https://docs.ruby-lang.org/ja/latest/method/String/i/=25.html
  例 
  'hello%d' % 5 -> 5を数値として受け取る。%dは数値として指定。
  "i = %d" % 10       # => "i = 10"
  "i" % 5 -> "i"
範囲オブジェクト .. ...
  .. 終端を含む
  ... 含まない

# Arrayクラス
-
  引数に含まれる要素を取り除く。
  a1 = [1,2,3]
  a2 = [4,2,3]
  a1 - a2  →  [1]
to_h
  配列からハッシュを作れる。
  [[1, "data 1"], [2, "data 2"]].to_h
  → {1=>"data 1", 2=>"data 2"}
each_cons(cnt)
  cntずつブロックに渡す。1つずつ進む。
shift
  先頭の要素を破壊的に取り出す。引数があればその数だけ取り出し、配列で返す。
  なければnilを返す。
unshift prepend
  先頭に値を破壊的に追加する。引数がなければ何もしない。
pop
  末尾から要素を取り除いて返す。引数があればその数だけ取り出し、配列で返す。
push append
  末尾に追加する。引数がなければ何もしない。
compact compact!
  nilを取り除くメソッド。
flatten flatten!
  再帰的に平坦化する。平坦化が行わなければnilを返す。
zip
  レシーバと引数の要素からなる配列を生成して返す。productの弱体化
  https://docs.ruby-lang.org/ja/latest/method/Array/i/zip.html
  [1, 2].zip([3, 4]) => [[1, 3], [2, 4]]
product
  レシーバの配列と引数の配列から一つずつ要素を取り出し、新しい配列を作成する。
  レシーバの要素を起点とする。
  [1, 2].product([3, 4])
  → [[1, 3], [1, 4], [2, 3], [2, 4]]
transpose
  レシーバの配列を元に、行と列を入れ替えた配列を作り、返す。
  https://docs.ruby-lang.org/ja/latest/method/Array/i/transpose.html
partition
  ブロックの要素を満たす部分、満たさない部分に分割し、
  真の配列と偽の配列を二つに分けて返す。
delete 破壊的メソッド。
  引数で指定した値を等しい要素を全て削除する。削除した場合は削除した要素を、そうでなければnilを返す。
  stirngは非破壊、arrayとhashは破壊的。
delete_if reject!
  ブロックを渡し、真の要素を全て削除する。
  delete_ifは常にselfを返す。reject!は削除しなければnilを返す。
upcase upcase!
  大文字
sort sort!
  並べ替え。<=>で実施。比較できなければArgumentError

# Hashクラス
初期化
  Hash[] or Hash.new or Hash({})
  Hash[]やHash()はエラー。
to_a
  キーと値を2要素の配列に並べた配列を返す。
  h = {a: 100, b: 200}
  h.to_a  // [[:a, 100], [:b, 200]]
values_at
  指定したキーの値を配列で返す。
member?
  指定したキーを持つか否か
  true/false
fetch
  keyに関連づけられる値を返す。
merge merge!
update
  指定した内容へ更新。破壊的。
clear
  ハッシュの中身を空にする。破壊的メソッド。
delete 破壊的メソッド
default ハッシュのデフォルト値を返す。
  hash = {}
  hash.default = "default"
  puts hash["non_existent_key"] # => "default"

default_proc ハッシュのデフォルト値を返す、Procオブジェクトを返す。ブロック形式のデフォルト値を持たない場合、nilを返す。
  hash = Hash.new { |h, k| h[k] = "default for #{k}" }
  puts hash["key1"] # => "default for key1"
  puts hash["key2"] # => "default for key2"

store
  []=と同じ。
  https://docs.ruby-lang.org/ja/latest/method/Hash/i/=5b=5d=3d.html

ハッシュのキーにオブジェクトを指定できる。
通常、シンボルと文字列を指定する。
キーを:klassとすると、シンボルで登録されてしまう。

# Enumerableクラス
abs2
  絶対値の2乗を返す。
succ
  次の整数を返す。
  0.succ ->1
each_with_index{|n, i| puts n}
  2つ目にindex
collect map
  ブロックの結果をまとめた配列を返す。
select filter select! fileter! find_all
  該当する全ての要素を配列にして返す。真がなければ空配列を返す。
  (1..10).find_all { |i| i % 3 == 0 }     # => [3, 6, 9]
find
  ブロックの条件に一致する最初の要素を返す。
any?
  trueになったらstop
inject
  ブロックを使って繰り返し計算を行う。
  引数は初期値となる。引数を省略した場合は要素１がブロック引数の1番目となる。
  引数にarrayを指定すると、そのarrayに対して処理を行う。

  irb(main):047:0> [1, 2, 3].inject{|x, y| x + y ** 2} rescue p $!
  => 14
  irb(main):048:0> [1, 2, 3].inject(0){|x, y| x + y ** 2} rescue p $!
  => 14
  irb(main):051:0> [1, 2, 3].inject([]){|x, y| x << y ** 2} rescue p $!
  => [1, 4, 9]
  irb(main):057:0> p [1, 2, 3].inject do|x, y| x + y ** 2 end rescue p $!
  #<LocalJumpError: no block given>
    pがなければ14。injectの後にスペースがあるため、p [...].injectまでが解釈され、ブロックを渡せずエラーとなる。

# Procオブジェクト（手続き）
  ブロックをオブジェクト化するためのもの。
  Procを使えばブロックを変数に代入したり、他のメソッドに渡したり、再利用できる。
  クロージャとして表現する。
  ※変数にブロックを代入することもできるが、クロージャとして使うならProcが適切。
  Procオブジェクト内の変数は、インスタンスごとに異なる。共有されない。

# Dateクラス
strftime 引数は一つだけ。
https://docs.ruby-lang.org/ja/latest/method/Time/i/strftime.html
  %F %Y-%m-%d 2024-04-14 Date.today.to_s
  %m month
  %M Minute
  %d date
  %D datetime %m/%d/%y
  %y 下２桁
  %Y 4桁
  %x 日付 (%Dと同等)

# Dirクラス
Dir.pwd パスを返す。
Dir.delete 空のディレクトリを削除。
Dir.rmdir 同上

# Fileクラス
File.dirname 引数の文字列の/より前の文字列を返す。
File.chmod 引数に指定したファイルのモードを示す。（権限）
File.delete ファイルを削除。

rewind
  ファイルポインタを先頭に移動。a+モードだと意味なく、末尾に追記される。

## モード
r 読み込みモード
r+ 読み書きモード。文の先頭から。
w 書き込みモード。既存のファイルがあればファイルの中身を空にする。空にしてから書き込み。
w+ 読み書きモード。既存はカラになる。空にしてから書き込み。
a 追記モード。文末に追記。
a+ 読み書きモード。読み込みは常に先頭。書き込みは常に末尾。

ファイル作成  w, a
ファイル追記  w, a wだとリセットされてから追記。

open('textfile.txt', XXXX) do |f|
  data = f.read.upcase
  f.rewind
  f.puts data
end

実行前の textfile.txt 内容
recode 1
recode 2
recode 3

実行後の textfile.txt 内容
RECODE 1
RECODE 2
RECODE 3

'r+'のみ。a+だと、末尾に書き込まれる。
recode 1
recode 2
recode 3
RECODE 1
RECODE 2
RECODE 3

# IOクラス
read(file_name, str_count, start_pos)
  第1引数で読み込むファイル、2でバイト数、3で開始位置
  IO.read('hoge.txt', 3, offset = 1)
  UTF-8においてASCII文字は1バイト換算。日本語等は2バイト以上が必要。
eof?
  ファイルポインタが終端ならtrue
readlines
  ファイルから全てを読み込む
seek(移動幅, 最初)
  IO::SEEK_SET ファイルの先頭から（デフォルト）
  IO::SEEK_CUR 現在のファイルポインタから。
write, readlines

# 例外エラークラス
raise
  第1引数: 発生させる例外クラス。インスタンスも指定できる。
  第2引数: メッセージ。

  引数を省略した場合はRuntimeErrorが発生。

rescue
  例外クラスを指定しない場合
    StandardErrorとそのサブクラスを補足する。
  =>で例外オブジェクトを参照できる。

  StandardErrorを継承しないクラスのインスタンスをraiseメソッドの引数に指定
    TypeErrorが発生し、「exception class/object expected」と表示。

# 演算子の優先度
算術演算子1 * / %
算術演算子2 + -
積 &
和 |
比較演算子1 < <= > >=
比較演算子2 == !=
論理演算子1 &&
論理演算子2 ||
3項演算子   ?:
https://docs.ruby-lang.org/ja/2.1.0/doc/spec=2foperator.html

  例
  a = [1, 2, 3, 5, 8]
  b = [1, 3, 6, 7, 8]
  c = false || true ? true && false ? a | b : a & b : b ;
  ->  true ? true ? [a | b] : [a & b] : b
  ->  true ? [a | b]
  -> [1, 3, 8]

# 可変長引数
*aはArrayクラスのオブジェクトを返す。
2つ定義することはできない。以下はsyntax errorとなる。
def bar(*n1, n2, *n3)
  puts n1
  puts n2
end

bar 5, 6, 7, 8

なお、関数を呼び出すときの引数に()は不要。

# 変数定義
ローカル変数は1文字以上。
定数は上書きするとき、警告が生じる。
メソッド内では定数を定義できない。宣言された場合、syntax errorとなる。

# 多重代入
変数に対して代入する値が少ないとき、変数にnilが格納。
値が多いとき、余った値は無視される。
1つの変数に複数の値を代入するとき、配列として代入される。

x, y, z = 1, 2 # zにはnilが格納される
x # => 1
y # => 2
z # => nil
x, y, z = 1, 2, 3, 4 # 4は無視される

x # => 1
y # => 2
z # => 3
x = 1, 2, 3, 4 # 1つの変数に複数の値を代入する場合配列として代入される

x # => [1, 2, 3, 4]
(x, y), z = 1, 2, 3 # 変数yにはnilが代入され、3は無視される

x # => 1
y # => nil
z # => 2
(x, y), z = [1, 2], 3 # 変数yには2が代入る

x # => 1
y # => 2
z # => 3


# %記法 https://docs.ruby-lang.org/ja/latest/doc/spec=2fliteral.html#percent
%(a b) -> 'a b'
  文字列にする
%!(a) -> "a" , %q(b) -> "b"
  ダブルクォーと文字列。
%W(a b) -> ['a', 'b']
  文字列の配列にする。大文字ならバックスラッシュ、式展開が有効
%s(a) -> :a
  シンボルにする。
  %s(a b) -> :"a b"
  {%s(a b) => 1} => {:"a b"=>1}
%i(a b) -> [:a, :b]
  シンボルの配列。大文字ならバックスラッシュ、式展開が有効

# メソッドの呼び出し
メソッド名と引数の間に空白がある場合
  foo (2) * 2 -> foo((2)*2)と解釈される。

rescueに例外クラスの指定がなければStandardErrorのサブクラスを全て補足する。

# ヒアドキュメント
<<識別子 から識別子行の直前までを文字列として扱う。
<<-識別子とすることで、終端行をインデントできる。これ以外は不可。
<<~とするとインデントを取り除く。
<<だとインデントを加えられr図、エラーになる。

irb(main):023:0" s = <<EOF
irb(main):024:0"       Hello,
irb(main):025:0"       Ruby
irb(main):026:0"       EOF
(irb):23: can't find string "EOF" anywhere before EOF (SyntaxError)

irb(main):027:0" s = <<-EOF
irb(main):028:0"       Hello,
irb(main):029:0"       Ruby
irb(main):030:0>       EOF
=> "      Hello,\n      Ruby\n"

irb(main):031:0" s = <<~EOF
irb(main):032:0"       Hello,
irb(main):033:0"       Ruby    
irb(main):034:0>       EOF
=> "Hello,\nRuby\n"

<<識別子 識別子の間に '識別子'があっても文字列としてみなされる。

## 開始ラベルによって解釈の方法が異なる。
"識別子"、識別子　式展開が有効
'識別子' 式展開不可
`識別子` コマンド出力


a: 1, b: 2, c:3
rescue => ex
正規表現
[Yy]es
Yes|yes
[Yy][e][s]
find
Array.delete(2)
Hash.merge 破壊的？
array[1, 3]
a=1..3
  a.to_a
str#chars
str#each_char
array.tally
https://docs.ruby-lang.org/ja/latest/method/Enumerable/i/tally.html