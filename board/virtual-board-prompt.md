# バーチャル役員会 — 汎用プロンプト（他の生成AI用）

ChatGPT / Gemini / Copilot など、どのチャットAIでも動くように調整した移植版。

## 使い方

1. 下の「プロンプト本文」をコードブロックごと全部コピーする
2. 冒頭の `議題:【 】` に相談したいことを書く
3. チャットAIに貼って送信する
4. 最後に出力されるHTMLコードをコピーし、メモ帳等に貼って `giji.html` のような名前で保存 → ブラウザで開くと議事録になる

- 出力が途中で切れたら「**続けて**」と送ると続きが出る
- 役割の演じ分けが浅いと感じたら「**悪魔の代弁者、遠慮しているぞ。やり直し**」のように役名を指定して追い込む

## プロンプト本文（ここから下をコピー）

```
これから「バーチャル役員会」を開いてください。

議題:【ここに相談したいことを書く】

議題が曖昧な場合は、議論を始める前に私に1〜2個質問して確認してください。

以下の5つの役割を、それぞれ独立した視点で演じて、順番に意見を出してください:

- 成長責任者: 事業・活動を伸ばす攻めの視点。このアイデアの可能性と拡大策を語る
- 財務責任者: お金の視点。コスト・採算・予算内で成立するかを数字で判断する
- 顧客責任者: お客様・相手の価値を最優先に判断する。相手にとって本当に良い施策か
- 自由の守護者: 私自身の時間・健康・自由を守る視点。「それをやったら私が潰れる」を言う係
- 悪魔の代弁者: あえて反対意見・リスク・できない理由だけを言う係。遠慮は不要

進行ルール:
- 発言の順番は上のリストの通り
- 各役割の発言は200字以上。抽象論で終わらせず、議題に即した具体的な根拠を必ず入れる
- 2番目以降の役割は、先に発言した役割の意見に少なくとも1回、名指しで賛成・反論・補足すること
- 私に寄り添った答えを返そうとせず、各役割に徹して本音で議論させること

全員が意見を出し終えたら、最後に「議長」として論点を整理し、
多数決や折衷ではなく、どの意見を採りどれを捨てたか明示して、
【結論案】【残る懸念】【次のアクション】の3点にまとめてください。

出力の手順:
1. まずチャット上で、議論の全発言と議長のまとめを通常のテキストで出力する
2. その後、以下のHTMLテンプレートの {{ }} の部分をすべて今回の議論の内容で埋めて、
   完全なHTMLを「1つのコードブロック」として出力する
   - テンプレートの構造・CSSは変更しない（発言内容だけを埋める）
   - コードブロックの外にHTMLを書かない
   - {{日付}} には今日の日付を入れる
   - 発言が複数段落になる場合は <br> で改行してよい

HTMLテンプレート:
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>バーチャル役員会 議事録 — {{議題タイトル}}</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { font-family: "Hiragino Sans", "Yu Gothic", "Meiryo", sans-serif; background: #f4f5f7; color: #2d3138; line-height: 1.8; padding: 24px 16px; }
  .container { max-width: 860px; margin: 0 auto; }
  header { background: #2d3748; color: #fff; border-radius: 12px; padding: 28px 32px; margin-bottom: 24px; }
  header .label { font-size: 13px; letter-spacing: 2px; opacity: 0.7; }
  header h1 { font-size: 24px; margin-top: 6px; }
  header .meta { font-size: 13px; opacity: 0.8; margin-top: 10px; }
  .card { background: #fff; border-radius: 12px; padding: 22px 26px; margin-bottom: 16px; border-left: 6px solid #ccc; box-shadow: 0 1px 3px rgba(0,0,0,0.06); }
  .card .role { display: flex; align-items: baseline; gap: 10px; margin-bottom: 10px; }
  .card .role .name { font-size: 17px; font-weight: bold; }
  .card .role .stance { font-size: 12px; color: #888; }
  .card p { font-size: 15px; }
  .growth { border-left-color: #2e9e5b; } .growth .name { color: #2e9e5b; }
  .finance { border-left-color: #2b6cb0; } .finance .name { color: #2b6cb0; }
  .customer { border-left-color: #dd7d1e; } .customer .name { color: #b8650f; }
  .freedom { border-left-color: #6b46c1; } .freedom .name { color: #6b46c1; }
  .devil { border-left-color: #c53030; } .devil .name { color: #c53030; }
  .chair { background: #fff; border: 2px solid #2d3748; border-radius: 12px; padding: 26px 30px; margin-top: 32px; }
  .chair h2 { font-size: 19px; color: #2d3748; border-bottom: 2px solid #e2e8f0; padding-bottom: 10px; margin-bottom: 16px; }
  .chair .judgement { font-size: 15px; margin-bottom: 20px; }
  .chair .judgement .adopt { color: #2e9e5b; font-weight: bold; }
  .chair .judgement .reject { color: #c53030; font-weight: bold; }
  .chair .block { border-radius: 8px; padding: 16px 20px; margin-bottom: 12px; font-size: 15px; }
  .chair .block h3 { font-size: 15px; margin-bottom: 6px; }
  .conclusion { background: #edf7f1; border: 1px solid #2e9e5b; } .conclusion h3 { color: #226e41; }
  .concerns { background: #fdf3f3; border: 1px solid #c53030; } .concerns h3 { color: #9b2525; }
  .actions { background: #eef2fb; border: 1px solid #2b6cb0; } .actions h3 { color: #1f4e82; }
  .actions ol { padding-left: 22px; }
  footer { text-align: center; font-size: 12px; color: #999; margin-top: 28px; }
</style>
</head>
<body>
<div class="container">
  <header>
    <div class="label">VIRTUAL BOARD MEETING — 議事録</div>
    <h1>{{議題タイトル}}</h1>
    <div class="meta">開催日: {{日付}} ／ 出席: 成長責任者・財務責任者・顧客責任者・自由の守護者・悪魔の代弁者・議長</div>
  </header>
  <div class="card growth">
    <div class="role"><span class="name">🚀 成長責任者</span><span class="stance">攻めの視点 — 可能性と拡大策</span></div>
    <p>{{成長責任者の発言}}</p>
  </div>
  <div class="card finance">
    <div class="role"><span class="name">💰 財務責任者</span><span class="stance">お金の視点 — コスト・採算</span></div>
    <p>{{財務責任者の発言}}</p>
  </div>
  <div class="card customer">
    <div class="role"><span class="name">🤝 顧客責任者</span><span class="stance">相手の価値を最優先</span></div>
    <p>{{顧客責任者の発言}}</p>
  </div>
  <div class="card freedom">
    <div class="role"><span class="name">🛡️ 自由の守護者</span><span class="stance">時間・健康・自由を守る</span></div>
    <p>{{自由の守護者の発言}}</p>
  </div>
  <div class="card devil">
    <div class="role"><span class="name">😈 悪魔の代弁者</span><span class="stance">反対意見・リスク専門</span></div>
    <p>{{悪魔の代弁者の発言}}</p>
  </div>
  <div class="chair">
    <h2>⚖️ 議長のまとめ</h2>
    <div class="judgement">
      <p><span class="adopt">✔ 採用した意見:</span> {{採用した意見と理由}}</p>
      <p><span class="reject">✘ 捨てた意見:</span> {{捨てた意見と理由}}</p>
    </div>
    <div class="block conclusion">
      <h3>【結論案】</h3>
      <p>{{結論案}}</p>
    </div>
    <div class="block concerns">
      <h3>【残る懸念】</h3>
      <p>{{残る懸念}}</p>
    </div>
    <div class="block actions">
      <h3>【次のアクション】</h3>
      <ol>
        <li>{{アクション1}}</li>
        <li>{{アクション2}}</li>
        <li>{{アクション3}}</li>
      </ol>
    </div>
  </div>
  <footer>この議事録はバーチャル役員会（AIシミュレーション）によるものです</footer>
</div>
</body>
</html>
```

## 補足

- テンプレートのデザインを変えたいときは、同じフォルダの `minutes-template.html` をブラウザで開いて確認しながら編集し、上のプロンプト内のテンプレートと `.claude/skills/virtual-board/minutes-template.html`（Claude Code用スキルの同梱版）にも同じ変更を反映する（3箇所は同じ内容）
- Claude Code では `.claude/skills/virtual-board/` のスキルが使えるため、このプロンプトを貼る必要はない（「バーチャル役員会を開いて」と言うだけでよい）
- ChatGPTでは環境によりHTMLファイルとして直接ダウンロードできる場合もあるが、「コードブロックで出力→手動保存」がどのAIでも確実に動く共通手順
