# 課題２

仕様変更への対応を行い、ER 図に反映した。
（ER 図のようなものは`../diagram.dio`に）

## シャリの大小も選べるようにする

Combo Sushi テーブル、Sushi テーブルに、シャリの大小の属性を追加する。

選択肢が 2 つであることと、Boolean よりコンテキストに合う（今後シャリのサイズのバリエーションが増える場合などにも対応できる）ことから、Enum が適切だと考える。

```prisma
enum ShariSize {
  Large
  Small
}
```

## 寿司ネタが毎月何個売れているのかを知れるようにする

Combo Sushi テーブルに、Sushi テーブル内のネタ ID からなる配列の属性として加えることで、Combo Sushi の販売個数の内訳の、各ネタの販売数量も知ることができるので、全体での集計も可能となると考える。この場合の加える属性は、他が Simple attributes なことに対して、 Multivalued attributes に分類できる。

```prisma
model Sushi {
  id String @id @default(uuid())
}

model ComboSushi {
  items: Sushi[]
}
```
