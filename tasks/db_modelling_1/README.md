# 課題１〜３

## 課題１

DB スキーマの設計を、下記のテーブルとカラムにまとめた。

### DB スキーマ：テーブル

- セットメニュー（詰め合わせ）： Combo Sushi
- お好みすし（単品）： Sushi
- 注文者： Orderer

### DB スキーマ：カラム

- Combo Sushi テーブル

| ID (String) | 種類 (String Enums) Category | ネタの名前 (String) Name | 値段 (Int) Price | 個数 (Int) Count | ぬき (Boolean) No Wasabi |
| ----------- | ---------------------------- | ------------------------ | ---------------- | ---------------- | ------------------------ |
| combo-1     | 盛り込み                     | はな                     | 8,650            | 1                | false                    |
| combo-7     | にぎり                       | みさき                   | 1,940            | 4                | false                    |
| combo-11    | 鮨やの丼＆おすすめ           | 海鮮ちらし               | 1,280            | 6                | true                     |
| combo-13    | 地元に生まれた味             | 鮨八宝巻                 | 1,280            | 6                | false                    |

- Sushi テーブル

| ID (String) | ネタの名前 (String) Name | 値段 (Int) Price | 皿数 (Int) Count | ぬき (Boolean) No Wasabi |
| ----------- | ------------------------ | ---------------- | ---------------- | ------------------------ |
| tamago      | 玉子                     | 100              | 2                | false                    |
| yudegeso    | ゆでげそ                 | 150              | 2                | false                    |
| ebi         | えび                     | 180              | 2                | false                    |
| namasa-mon  | 生サーモン               | 220              | 2                | false                    |
| aji         | あじ                     | 260              | 2                | false                    |

- Orderer テーブル

| お名前 (String) Name | お電話（String) Phone Number | お支払い (Boolean) Paid |
| -------------------- | ---------------------------- | ----------------------- |
| John Doe             | 1234-5618                    | true                    |

### ER 図的なもの１

![ER 図的なもの１](./diagram_1.svg "ER 図的なもの１")

#### ER 図の表記について

- 長方形：Entities
- 楕円：Simple Attributes
  - 太めのボーダー付き：Multivalued Attributes
- ひし形：Relationships
- 細線：Partial participation
- 太線：Total participation
- 1, N：カーディナリティ

### 任意課題

TODO: あとでやる

#### 概念モデル

#### 論理モデル

#### 物理モデル

---

## 課題２

仕様変更への対応を行い、ER 図に反映した。

### シャリの大小も選べるようにする

Combo Sushi テーブル、Sushi テーブルに、シャリの大小の属性を追加する。

選択肢が 2 つであることと、Boolean よりコンテキストに合う（今後シャリのサイズのバリエーションが増える場合などにも対応できる）ことから、Enum が適切だと考える。

```prisma
enum ShariSize {
  Large
  Small
}
```

### 寿司ネタが毎月何個売れているのかを知れるようにする

Combo Sushi テーブルに、Sushi テーブル内のネタ ID からなる配列の属性として加えることで、Combo Sushi の販売個数の内訳の、各ネタの販売数量も知ることができるので、全体での集計も可能となると考える。この場合の加える属性は、他が Simple attributes なことに対して、 Multivalued attributes に分類できる。

```prisma
model Sushi {
  id String @id @default(uuid())
}

model ComboSushi {
  items: Sushi[]
}
```

### ER 図的なもの２

![ER 図的なもの２](./diagram_2.svg "ER 図的なもの２")

---

## 課題３

考えうる追加仕様

- 表示価格を、税込・税抜のどちらかを一斉選択できるように
  - 後方互換性考慮した場合、After-tax Price を attribute に追加する
  - 後方互換性考慮しなくてもよい場合、Price を Simple attribute から Composite attribute にする
- お支払い方法の追加で、クレカや電子マネー決済が選択できるように
  - 後方互換性考慮した場合、Paid を残して、PaymentMethod の Enum にして、None, CreditCard, EMoney と選べるようにする
  - 後方互換性考慮しなくてもよい場合、Paid を PaymentMethod に置き換える

---

## Note

### Database schema

A schema is the blueprint of a database.

- Names of tables
- Columns of each table
- Datatype
- Functions
- Other objects

are included in the schema.

We use the schema diagram to display the schema of a database.
