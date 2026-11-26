# Mittler Cut Prompter

English | [日本語](#日本語)

An agent skill that writes **only the prompts** for one short shot (2–10 seconds) of AI video generation:
the image prompt for the **start frame** and/or **end frame**, and the **video prompt**.
It does not generate images or videos and sends nothing anywhere.

It comes from [Mittler](https://github.com/sa-san10/mittler), a video editor for VS Code made to be used with an AI agent, and packs what worked there for writing shot prompts.

- Four ways to hand frames to the video model: **start frame only** (recommended), **end frame only**, **start and end**, or **no image** (text only).
- A separate branch for **audio-driven lip-sync models** (the voice is given with the shot), with the rules that made lip sync work: one voice per speaker, avoid long silences, keep the acting small.
- Uses the user's **character and scene references** when given, and turns them into concrete words so the look stays the same across shots.
- Timed acting (`0.0-0.4s: …`), what must stay still, camera, light, style and negatives — the structure that worked for short shots.
- Notes for the models the author used (MiniMax H3 image-to-video and reference-to-video). For other models, follow their official guides first.

> **Alpha.** The documents are written mostly in Japanese, by and for AI agents. Mistakes in them are bugs: please report them as issues.

## Use

**Claude Code**: copy `skills/cut-prompter/` to `~/.claude/skills/cut-prompter/` (or to `.claude/skills/` in your project). Then ask, for example, "Write the start frame and video prompt for a 4-second shot where she looks up at the light".

**Other agents**: open this folder and tell the agent to follow `AGENTS.md`, or paste `skills/cut-prompter/SKILL.md` and the files in `reference/` into its instructions.

Output format:

````markdown
<!-- 4.0 s, start frame only, 16:9, regular model -->

## 画像プロンプト（開始フレーム）
```
...
```

## 動画プロンプト
```
...
```
````

## License

MIT (see `LICENSE`).

---

## 日本語

動画生成 AI に渡す短いカット（2〜10 秒）の、**画像プロンプト（開始フレーム・終了フレーム）と動画プロンプトだけ** を書くエージェント向けのスキルです。生成・送信はしません。

[Mittler](https://github.com/sa-san10/mittler)（AI エージェントと一緒に使う VS Code の動画エディタ）で、短いカットのプロンプトの書き方としてうまくいったことをまとめたものです。

- 絵の渡し方は 4 通り：**開始フレームだけ**（おすすめ）／**終了フレームだけ**／**開始と終了の両方**／**画像なし**
- **声から口パクを作る動画モデル** 向けの分岐（1 本の声＝1 人・長い無音を避ける・演技は控えめ）
- ユーザーの **キャラ・シーンの資料** があれば、見た目を言葉に起こして、カットどうしの見た目をそろえる
- 時刻ごとの演技・動かないもの・カメラ・光・画風・禁止の、短いカットで通った構成
- 作者が使ったモデル（MiniMax H3 の Image to Video・Reference to Video）の注意。ほかのモデルは公式の手引きを優先

**使い方**：Claude Code なら `skills/cut-prompter/` を `~/.claude/skills/cut-prompter/`（または作品の `.claude/skills/`）に写して、「この場面の開始フレームと動画プロンプトを作って」と頼みます。ほかのエージェントでは、このフォルダを開いて `AGENTS.md` に従うよう伝えます。

> **アルファ版**：文書の多くは AI が AI 向けに書いたものです。まちがいはバグとして Issue で知らせてください。

ライセンスは MIT です。
