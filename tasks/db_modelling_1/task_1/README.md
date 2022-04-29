# 課題１

DB スキーマの設計を、下記のテーブルとカラムにまとめた。
（ER 図のようなものは`../diagram.dio`に）

## DB スキーマ：テーブル

- セットメニュー（詰め合わせ）： Combo Sushi
- お好みすし（単品）： Sushi
- 注文者： Orderer

## DB スキーマ：カラム

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

| お名前 (String) Name | お電話（String) Phone Number | お支払い (Boolean) Payment |
| -------------------- | ---------------------------- | -------------------------- |
| John Doe             | 1234-5618                    | true                       |

## ER 図の表記について

- 長方形：Entities
- 楕円：Simple Attributes
  - 太めのボーダー付き：Multivalued Attributes
- ひし形：Relationships
- 細線：Partial participation
- 太線：Total participation
- 1, N：カーディナリティ

---

## 任意課題

TODO: あとでやる

## 概念モデル

### 論理モデル

### 物理モデル
