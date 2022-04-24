# 課題１

DB スキーマの設計（ER 図のようなものは`./diagram.dio`に）

## テーブル

- お好みすし（単品）： Single Sushi
- セットメニュー（詰め合わせ）： Combo Sushi
- 注文者： Orderer

## カラム

- Combo Sushi

| ID (String) | 種類 (String Enums) Category | 名称 (String) Name | 値段 (Int) Price | 個数 (Int) Count | ぬき (Boolean) No Wasabi |
| ----------- | ---------------------------- | ------------------ | ---------------- | ---------------- | ------------------------ |
| combo-1     | 盛り込み                     | はな               | 8,650            | 1                | false                    |
| combo-7     | にぎり                       | みさき             | 1,940            | 4                | false                    |
| combo-11    | 鮨やの丼＆おすすめ           | 海鮮ちらし         | 1,280            | 6                | true                     |
| combo-13    | 地元に生まれた味             | 鮨八宝巻           | 1,280            | 6                | false                    |

- Single Sushi

| ID (String) | 名称 (String) Name | 値段 (Int) Price | 皿数 (Int) Count | ぬき (Boolean) No Wasabi |
| ----------- | ------------------ | ---------------- | ---------------- | ------------------------ |
| tamago      | 玉子               | 100              | 2                | false                    |
| yudegeso    | ゆでげそ           | 150              | 2                | false                    |
| ebi         | えび               | 180              | 2                | false                    |
| namasa-mon  | 生サーモン         | 220              | 2                | false                    |
| aji         | あじ               | 260              | 2                | false                    |

- Orderer

| お名前 (String) Name | お電話（String) Phone Number | お支払い (Boolean) Payment |
| -------------------- | ---------------------------- | -------------------------- |
| John Doe             | 1234-5618                    | true                       |

---

## 任意課題
