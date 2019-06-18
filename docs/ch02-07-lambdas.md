# ラムダ式

ラムダ式とは関数を変数に代入して扱えるようにするものです。ラムダ式が必要になってくるシーンは関数を引数として受け取るような関数を使用するときです。例として `map()` という組み込み関数について考えてみます。`map()` はリストなどのコレクションの各要素に変更を加えたものを作成するための関数です。

!!! Tips
    引数として渡される関数のことをコールバックといいます。

```python
x = [1, 2, 3, 4, 5]
```

上記のリストの各要素を 2 乗して `[1, 4, 9, 16, 25]` というリストを `map()` で作成するには次のようにします。

```python
list(map(lambda e: e * e, x))
```

`map()` の第 1 引数にはラムダ式が渡されています。ラムダ式は機能的には通常の関数と同様の機能を提供しており

```python
lambda e: e * e
```

というラムダ式は下記の関数と等価なものになっています。

```python
def power(e):
    return e * e
```

`map()` は第 2 引数に渡されたコレクションの各要素をラムダ式に渡し、その戻り値を逐次返却していくという振る舞いをします。ちなみに `map()` には上記の `power()` のような通常の関数を渡すこともできます。

```python
list(map(power, x))
```

ラムダ式が通常の関数と異なる点は

- 名前を持たない（無名関数）
- 必要なときに即時に定義できる

という点です。`map()` に渡すためのちょっとした処理に対して、わざわざ関数定義をするのも面倒だといったケースではラムダ式が使われます。その他の例もいくつか挙げておきます。

```python
list(map(lambda e: 2 * e, x))           # [2, 4, 6, 8, 10]
list(map(lambda e: (e, 2 * e + 1), x))  # [(1, 3), (2, 5), (3, 7), (4, 9), (5, 11)]
```

`map()` の戻り値は **イテレータ** というオブジェクトが返ります。イテレータ自体はリストではないですが、ループ文に渡すことでリストと同じように変換結果の要素を取り出すことができます。

```python
for item in map(lambda e: e * e, x):
    print(item)     # 1, 4, 9, 16, 25
```

イテレータを `list()` に渡すとリストに変換してくれます。つまりループ文で要素を参照するだけであればリストに変換する必要はありません。インデックス参照などがしたい場合にリストに変換すると良いでしょう。`map()` のようにコレクションとコールバックを受け取りイテレータを返す関数は他にもいくつか用意されています。代表的なものには [itertools] があります。

[itertools]: https://docs.python.org/ja/3/library/itertools.html