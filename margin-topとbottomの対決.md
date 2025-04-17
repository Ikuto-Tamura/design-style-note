めっちゃいい質問攻めです！それぞれ、実務でも迷いがちなポイントなので、丁寧に答えていきますね。

---

### ❶ **margin は `margin-bottom` がベスト？**

✅ **Yes、基本的には `margin-bottom` を使うのがベスト** です。

#### なぜか？

- フォームや縦積みの UI では「下に余白をつける」ことで、順番に自然な空きができる。
- 上下に `margin` を設定すると、重複（collapse）してしまうことがあり、不安定になりやすい。

#### 例：

```css
.input-group {
  margin-bottom: 1rem;
}
```

⚠️ **例外**：要素の最下部には `margin-bottom` ではなく、**親要素の `padding-bottom`** で空けるほうが安定します。

---

### ❷ **`margin` は `px` と `rem` どっちがいい？**

✅ **UI 全体で一貫性を持たせたいなら、基本は `rem` 推奨** です。

- `1rem` = ルートのフォントサイズ（通常 16px）
- ユーザーがブラウザでフォントサイズを変更しても、`rem` だと柔軟に対応できる
- Material Design 3 でも、spacing は 4px 刻みベースだけど、設計時には `rem` 化されていることが多い

#### 実務でのおすすめルール：

- `padding` や `margin` などの**余白** → `rem`
- **ボーダー幅やアイコンサイズなどピクセル単位で見た目が大事なもの** → `px`

---

### ❸ **`box-shadow` の `opacity` はどう決める？**

`box-shadow` の透明度（= alpha 値）は、**「奥行きのレベル」や「注目度」**によって決めます。

#### Material Design 3 のベストプラクティス例（Elevation 1〜5）：

```css
/* Elevation 1 */
box-shadow: 0px 1px 3px rgba(0, 0, 0, 0.12);

/* Elevation 2 */
box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.16);

/* Elevation 3 */
box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.19);
```

#### ポイント：

- **色は黒 (`rgba(0,0,0,...)`)** を基本にする（影は光が遮られてできる）
- **opacity は 0.12〜0.25 程度**がベース
- 強調したいカードは `0.2〜0.3` くらいにしても OK（押し出す感じ）

---

### ❹ **`container` と `card` の `width` は一致すべき？**

🟡 **必ずしも一致させる必要はない**です。役割が違います。

- **`container`**：画面の中央寄せや背景調整用 → 基本は**幅 100%**に近い
- **`card`**：中身のボックス → **固定幅 or max-width** を指定して、視認性をコントロール

#### 実務でよくあるパターン：

```css
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: var(--md-sys-color-background);
}

.login-card {
  width: 100%;
  max-width: 400px;
  padding: 2rem;
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}
```

→ これでスマホでもはみ出さず、PC ではちょうどよく中央に表示されます。

---

もっと詰めたい場合は、UI 実装の見本やコード化もすぐできますので、気軽にどうぞ！\
もし Figma のデザインなどがあるなら、それに寄せた実装サンプルも作れます。
