# parallel-edit

1 つの文書を、複数の Claude Code セッションで並列に編集するための plugin です。各セッションが従う決まりを、作業役と見直し役の 2 つのスキルとして提供します。セッション間の連絡には [cross-session messaging](https://code.claude.com/docs/en/cross-session-messaging) を使います。

## インストール

```bash
claude plugin marketplace add megmogmog1965/megmogmog1965-claude-code-parallel-edit
claude plugin install parallel-edit@megmogmog1965-claude-code-parallel-edit
```

## 使い方

1. 最初のセッションに名前を付け、作業役のスキルを読み込ませます。文書のパスと担当範囲は省略できます。省略すると、会話の中で編集している文書と、人間と議論する論点が使われます。

   ```text
   /rename session-01
   /parallel-edit:worker ./docs/spec.md "3 章"
   ```

2. 新しいターミナルのタブで、このセッションを名前で指定して分岐させ、別の名前と担当を渡します。必要な数だけ繰り返します。

   ```bash
   claude --resume session-01 --fork-session
   ```

   ```text
   /rename session-02
   /parallel-edit:worker ./docs/spec.md "4 章"
   ```

3. 見直し役を置く場合は、新しいセッションで見直し役のスキルを読み込ませます。見直し役は、15 分ごとの見直しを自分で予約します。

   ```text
   /rename session-review
   /parallel-edit:review ./docs/spec.md
   ```

## ライセンス

MIT
