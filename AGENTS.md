# AGENTS.md（cut-prompter を使うエージェントが最初に読む）

このリポジトリは、動画生成 AI に渡す短いカット（2〜10 秒）の **画像プロンプト（開始フレーム・終了フレーム）と動画プロンプトを書くだけ** の手順です。
画像や動画の生成・送信はしません。返事はユーザーの言葉で、短く書いてください。

ユーザーに「動画のプロンプトを作って」「このシーンの開始フレームとプロンプト」「口パクのカットのプロンプト」などと頼まれたら、
**`skills/cut-prompter/SKILL.md` を読み、そのとおりに進めます**（Claude Code ではスキルとして入れると、自動で使われます）。

| 場所 | 中身 |
|---|---|
| `skills/cut-prompter/SKILL.md` | 進め方と出力の形（ここから読む） |
| `skills/cut-prompter/reference/frame-modes.md` | 開始フレーム／終了フレーム／両方／画像なし の選び方 |
| `skills/cut-prompter/reference/image-prompt.md` | 画像プロンプトの書き方 |
| `skills/cut-prompter/reference/video-prompt.md` | 動画プロンプト（ふつうのモデル）の書き方 |
| `skills/cut-prompter/reference/lipsync.md` | 動画プロンプト（声から口パクを作るモデル）の書き方 |
| `skills/cut-prompter/reference/model-notes.md` | モデルごとの注意（わかっているもの） |
| `skills/cut-prompter/reference/references.md` | キャラ・シーンの資料の使い方 |

## 文書の正しさについて

この手順は完全な正しさを保証しません。使っていて、手順どおりだとうまくいかない・モデルの今の動きと合わない所に気づいたら、
何がどう違うかをユーザーに伝えて確認し、許可をもらってから、手順と違うやり方で進めたり、手順を直したりします。
