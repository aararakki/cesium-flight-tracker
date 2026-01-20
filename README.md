# CesiumJS Flight Tracker（公式チュートリアル Step1〜Step7 完全再現 / GitHub Pages / CDN / ビルド不要）

このリポジトリは、Cesium公式チュートリアル **Build a Flight Tracker**（Step 1〜Step 7）を、
**Glitchを使わず**に **CDN方式（ビルド不要）**で **GitHub Pages**（github.io）へ公開するための教材テンプレートです。

- ✅ Cesium World Terrain + OSM Buildings
- ✅ 時系列データ（flightData）を再生（timeline/clock）
- ✅ Cesium ion の 3D飛行機モデルを表示し、進行方向に向けて追従（Step 6/7）
- ✅ flightData は **外部JSON（flightData.json）** として分離

> 重要：公式サイトの `flightData = JSON.parse(\`...\`)` 内の配列データは非常に長いため、本テンプレートでは `flightData.json` に貼り付けて使います。（貼り付け位置は本READMEに図解付きで案内します）

---

## 1) 事前準備（Cesium ion トークン）

1. Cesium ion にログイン
2. **Access Tokens** で default token をコピー
3. `index.html` の以下を差し替え：

```js
Cesium.Ion.defaultAccessToken = "YOUR_CESIUM_ION_ACCESS_TOKEN";
```

---

## 2) Step 6：飛行機モデルを Cesium ion にアップロード

1. 公式チュートリアルの「airplane model（Cesium_Air.glb）」を入手
2. Cesium ion ダッシュボードへアップロード
3. 種別は **3D Model (Convert to glTF)** を選択
4. 生成された **Asset ID** を控える
5. `index.html` の以下を差し替え：

```js
const airplaneAssetId = 123456; // ←あなたのAsset ID
```

---

## 3) 公式 flightData を flightData.json に「完全貼り込み」

### 3-1. どこからコピーする？
Cesium公式チュートリアル「Build a Flight Tracker」の Step 4 にある次の部分です：

```js
const flightData = JSON.parse(`
  [
    { "longitude": ..., "latitude": ..., "height": ... },
    ...
  ]
`);
```

### 3-2. どこに貼る？
このリポジトリの `flightData.json` を開き、**`[` から `]` までの配列全体**を、丸ごと置き換えて保存します。

- ✅ OK： `[` で始まり `]` で終わる「JSON配列」
- ❌ NG： `JSON.parse(` やバッククォート `` ` `` を含める（入れない）

---

## 4) GitHub Pages で公開（Glitch不要）

### 4-1. Pagesを有効化
GitHub → **Settings** → **Pages**

- Source: `Deploy from a branch`
- Branch: `main` / `(root)`

公開URL例：
`https://username.github.io/cesium-flight-tracker/`

---

## 5) ローカルで確認したい場合（任意）

CORSやパスの確認のため、簡易サーバを使うと安心です。

### Python（例）
```bash
python -m http.server 8000
```
→ `http://localhost:8000/` にアクセス

---

## 6) よくあるトラブル

- 画面が真っ白：トークン未設定/誤り
- 飛行機が出ない：Asset ID 未設定、ion側処理未完了
- JSONが読めない：flightData.json の構文エラー（カンマ、括弧など）

---

## 7) ライセンス
Cesium Learn のサンプルコードは Apache 2.0 です（公式表記に従う）。

---

## 収録ファイル

- `index.html`：CDN版の完成コード（Step1〜7相当）
- `style.css`：全画面表示
- `flightData.json`：ここに公式 flightData を貼り付ける
- `docs/`：講義配布用PDF（図解）
