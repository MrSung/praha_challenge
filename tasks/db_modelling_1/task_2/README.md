# 課題２

仕様変更への対応

## シャリの大小も選べるようにする

Combo Sushi テーブル、Sushi テーブルに、シャリの大小の属性を追加する。

選択肢が 2 つであることと、Boolean よりコンテキストに合うことから、Enum が適切だと考える。

```prisma
enum ShariSize {
  Large
  Small
}
```

## 寿司ネタが毎月何個売れているのかを知れるようにする

Combo Sushi テーブルに、Sushi テーブル内のネタ ID からなる配列の属性として加えることで、Combo Sushi の販売個数の内訳の、各ネタの販売数量も知ることができるので、全体での集計も可能となると考える。

```prisma
model Sushi {
  id String
}

model ComboSushi {
  items: Sushi[]
}
```
