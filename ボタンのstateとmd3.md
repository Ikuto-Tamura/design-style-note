いいですね、それやりましょう！  
Material Design 3（通称 M3）では、ボタンなどの**コンポーネントの状態（state）**に対して明確なルールがあります。これを理解することで、`hover` や `focus` をどう使うかがよりクリアになります。

---

## 🔶 Material Design 3 におけるボタンの状態（States）

M3 では、ボタンの状態を以下の 5 つに分類しています：

| 状態名       | 説明                                                                       |
| ------------ | -------------------------------------------------------------------------- |
| **Enabled**  | 通常状態（何もしていない状態）                                             |
| **Hovered**  | マウスカーソルが上にある状態（`:hover`）                                   |
| **Focused**  | キーボード操作などでフォーカスされている状態（`:focus`, `:focus-visible`） |
| **Pressed**  | クリックまたはタップされている状態（`:active`）                            |
| **Disabled** | 無効状態（`disabled` 属性）                                                |

---

## 🔸 状態ごとのデザイン原則（ボタンの例）

### 1. ✅ Enabled（通常）

- 背景・枠線・テキストカラーがデフォルトの状態
- Elevation（影）もデフォルト
- アニメーションなどは未発動

### 2. 🖱️ Hovered（ホバー）→ `:hover`

- **背景色が少し変わる**
- **影（elevation）が増える**（例: `elevation: 2 → 3`）
- **アニメーションで反応**することが多い

```css
button:hover {
  background-color: rgba(
    33,
    150,
    243,
    0.08
  ); /* Surface color + hover overlay */
}
```

### 3. 🎯 Focused（フォーカス）→ `:focus-visible` 推奨

- **フォーカスインジケータ**が表示される（例: outline や border）
- **アクセシビリティ上とても重要！**
- `:focus` だとマウスクリック時にも発火する → `:focus-visible` のほうが適切

```css
button:focus-visible {
  outline: 2px solid #2962ff;
  outline-offset: 2px;
}
```

### 4. 👇 Pressed（押下）→ `:active`

- **押している間のビジュアル**
- 背景がさらに濃くなるなど、押された感を出す
- elevation が下がる（影が弱まる）

```css
button:active {
  background-color: rgba(33, 150, 243, 0.12);
  box-shadow: none;
}
```

### 5. 🚫 Disabled

- 視覚的にグレーアウト（text, icon, bg）
- `cursor: not-allowed;` にすることも
- 操作できないと明確にわかるように

```css
button:disabled {
  background-color: rgba(0, 0, 0, 0.12);
  color: rgba(0, 0, 0, 0.38);
}
```

---

## 🧠 補足：M3 の「State Layer」って何？

Material Design 3 では状態を「**state layer**」というレイヤーで表現します。これは背景色のオーバーレイのようなものです。

- `hover` → **state layer opacity: 8%**
- `focus` → **state layer opacity: 12%**
- `pressed` → **state layer opacity: 12%**
- `dragged` → **state layer opacity: 16%**

これらをベース色（例: `primary` や `surface`）の上に半透明で重ねることで、状態を表現します。

---

## 🎨 実際の CSS 実装イメージ（M3 スタイル）

```css
button {
  background-color: #ffffff;
  color: #1d1d1f;
  border: none;
  padding: 12px 24px;
  border-radius: 8px;
  transition: background-color 0.2s, box-shadow 0.2s;
}

/* Hover */
button:hover {
  background-color: rgba(33, 150, 243, 0.08);
}

/* Focus (keyboard only) */
button:focus-visible {
  outline: 2px solid #2962ff;
  outline-offset: 2px;
}

/* Pressed */
button:active {
  background-color: rgba(33, 150, 243, 0.12);
}

/* Disabled */
button:disabled {
  background-color: rgba(0, 0, 0, 0.12);
  color: rgba(0, 0, 0, 0.38);
  cursor: not-allowed;
}
```

---

## ✨ まとめ：hover / focus / active の使い分け in M3

| 状態    | 疑似クラス       | 目的                               | ユーザー操作               |
| ------- | ---------------- | ---------------------------------- | -------------------------- |
| Hovered | `:hover`         | マウスが乗ったときの視覚効果       | マウスオン                 |
| Focused | `:focus-visible` | キーボード操作での明示的フォーカス | Tab キー操作など           |
| Pressed | `:active`        | 押下中の瞬間的な反応               | クリック・タップしている間 |

---

必要なら、M3 の公式仕様に基づいた実装ガイドラインや Figma のデザイン参考も案内できますよ。使ってる UI フレームワーク（MUI とか）あれば、それに合わせた例も出せます。
