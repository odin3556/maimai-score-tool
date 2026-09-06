# maimai スコア取得ブックマークレット

maimaiでらっくすNET（`maimaidx.jp`）／ maimai DX International Version（`maimaidx-eng.com`）から
自分のスコアデータを取得し、`maimai-player-data_*.json` としてダウンロードするためのブックマークレットです。

## 中身

このブックマークレット自体は、[音ゲーツール置き場（reiwa.f5.si）](https://reiwa.f5.si/) が公開している
データ取得スクリプト `maimai_collect.js` を読み込んで実行するだけのローダーです。

```
javascript:(function(){var e=document.createElement("script");e.src="https://reiwa.f5.si/bookmarklets/maimai_collect.js?"+String(Math.floor((new Date()).getTime()/1e3));document.body.appendChild(e);})();
```

- 取得スクリプト: `https://reiwa.f5.si/bookmarklets/maimai_collect.js`
- 譜面定数表: `https://reiwa.f5.si/maimai_record.json`（otoge-db 由来）

本ツールはこれらの外部リソースに依存しています。取得スクリプト・定数表の著作権および提供方針は
配布元（音ゲーツール置き場）に帰属します。

## 使い方

1. `bookmarklet.txt` の1行をコピーし、新しいブックマークのURL欄に貼り付けて登録する
   （または本ツールの「設定・データ取得」タブのリンクをブックマークバーへドラッグ）。
2. `maimaidx.jp` にログインし、Aimeカードを選択した状態にする。
3. 登録したブックマークをクリックする。進捗ダイアログが出て、完了すると
   `maimai-player-data_*.json` がダウンロードされる。
4. そのJSONを本ツールの「レーティングチェッカー」タブに読み込む。

## 取得されるJSONの形

```json
{
  "honor": "称号",
  "name": "プレイヤー名",
  "rating": 15000,
  "updatedAt": "2026-09-07T12:00:00+09:00",
  "d_version": "1.1.0",
  "score":         [ { "title": "...", "difficulty": "Master", "score": 1005000, "lamp": "AP", "isdx": true, "dxs": { "score": 0, "max": 0 } } ],
  "new":           [ { "title": "...", "difficulty": "Master", "score": 1002000, "lamp": "", "isdx": true } ],
  "best":          [ ... ],
  "new_candidate": [ ... ],
  "best_candidate":[ ... ]
}
```

- `score` の `score` は 達成率 × 10000（例: `100.5000%` → `1005000`）。
- `best` はRATING対象曲（旧曲ベスト35）、`new` はRATING対象曲（新曲ベスト15）。
  `*_candidate` は次点の候補曲。これらの取得には有料プラン加入が必要な場合があります。
- このJSONには**譜面定数が含まれない**ため、本ツールは `maimai_record.json` を別途取得して結合します。
