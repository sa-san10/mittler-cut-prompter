# 動画プロンプト（声から口パクを作るモデル）の書き方

声（音声ファイル）を一緒に渡して、口の動きを声に合わせるモデル向けです（例：MiniMax H3 の Reference to Video。`model-notes.md`）。ふつうのモデルより決まりが多いので、書く前に全部読んでください。

## まず使うかどうか

- **歌のカット** に向いています。
- **アニメのせりふ（しゃべり）は、このモデルを使わない方がうまくいくことが多い** です。ふつうのモデル（`video-prompt.md`）で絵を先に作り、声はあとで口に合わせる（アフレコ）ほうが、演技も画質も安定します。ユーザーがせりふのカットで口パクのモデルを指定したら、この点を出力の頭のコメントに 1 行で書いてから、指定どおりに書きます。
- 口パクのモデルは、ふつうのモデルより画が硬く・暗くなりやすいことがあります。口パクが要らないカットは、ふつうのモデルにします。

## 決まり

- **開始フレームが必要・終了フレームは使わない**：開始フレームを `<Picture 1>` として書きます。
- **1 本の声＝1 人**：歌う（話す）人を `(S1)` にします。1 本の声に 2 人の声が入っていると、誰の口を動かすかも時刻も効かなくなります。掛け合いは 1 人ずつのカットに分けます（後ろのカットの開始フレームは、前のカットの最後のコマ）。
- **声の途中の長い無音を避ける**：約 0.4 秒をこえる無音があると、声をそのまま写さずに作り直されやすくなります。無音は声のほうで詰めるか、そこでカットを分けるよう、出力の頭のコメントでユーザーに伝えます。
- **演技は控えめに**：演技を大きく・細かく書くほど、口の合いが落ちます。口をきっちり合わせるカットでは「歌う・話す＋少しの動き」にとどめます。
- **時刻の軸**：モデル（の実行の仕組み）によっては、声の前に無音が足されます（例：0.5 秒）。わかっているなら、プロンプトの時刻はその分ずらして書きます（声の頭が 0.5 秒後に始まる）。わからなければ出力の頭のコメントで確かめるよう書きます。
- **声の長さ**：モデルの上限・下限があります（`model-notes.md`）。カットの長さは声の長さに合わせます。
- **伴奏なしの声**：歌なら、ボーカルだけ（伴奏を外したもの）を渡すよう、コメントでユーザーに伝えます。

## 構成（英語・6 つの節）

```
subject_definitions:
<Picture 1> is the exact first frame of [Shot 1] at 00:00.000.
(<Picture 2> is the identity reference of (S1): her face, eyes, makeup and hairstyle must match <Picture 2> and <Picture 1> exactly.)   ← 顔の参照画像を足すときだけ
(S1) is <位置> : <見た目を具体的に。髪・服・持ち物>. Her face: <目・まつ毛・メイク・鼻・唇・あご・肌>.
(S2) is <位置>: <見た目>. (S2) does not sing.            ← ほかに映る人がいれば人数分
<Audio 1>: fully_copy - <Audio 1> is reused 1:1 as the target video's complete final audio track, (S1) sings a song.

summary:
<このカットを 1 文で>

retention_analysis:
Keep (S1)'s face, hair, clothes and props exactly as in <Picture 1>. (Use <Picture 2> only for (S1)'s face and hairstyle identity; do not copy its background, full-body pose or framing. <Picture 2> is not a reference for (S2).) Keep <背景の主な物> as they are.

detailed_description:
[Shot 1] The shot begins from <Picture 1> as the exact first frame at 00:00.000.
<Audio 1> is the Japanese song with the lyrics <d>[Japanese]"<歌詞>"</d>. The mouth of (S1) movements are precisely synchronized with the Japanese lyrics.
From 00:00.000 to <歌い出し> (S1) <歌う前の小さな動き>; her mouth stays still.
From <歌い出し> to <歌い終わり> (S1) sings the line with clear, natural Japanese mouth shapes for every syllable; <少しの演技>.
After <歌い終わり> she closes her mouth softly and holds the feeling.
(S2) <動き>; keeps the mouth closed and the expression from <Picture 1>; never sings or talks.
<手と持ち物：The hand holding the microphone keeps five fingers; the microphone stays below her lips so her lips stay visible.>
Camera: <固定・ゆっくり寄るなど>; no zoom.
Lighting: <光>.
Look: <画風の行。ふつうのモデルのプロンプトと同じ言葉をそのまま>.
Do not add any new text, captions, logos or watermarks.

overall_soundscape:
<Audio 1> only, copied exactly as the complete final audio track. No additional speech, ambience, crowd noise, instrument sound, or sound effects.

non_diegetic_music:
<Audio 1> only.
```

- 話すカット（歌でない）なら `sings a song` を `speaks the lines`、`Japanese song` を `Japanese speech` に変えます。
- 歌い出しの前と歌い終わりの後には、必ず「口を動かさない」区間を書きます（書かないと勝手に口が動きます）。
- 開始フレームで口が大きく開いている人（笑顔・驚き）は、「口を閉じる」より「唇とあごを動かさない」と書きます（無理に閉じさせると顔が変わるため）。
- 顔がとても小さい引きの絵は、口が甘くなりやすいです。歌う人を大きく映す構図を、開始フレームの画像プロンプトで選びます。

## 開始フレームの画像プロンプトで気をつけること

- 歌う人の口は、軽く閉じるか少し開けた状態にします。
- マイクを持つなら、マイクは唇より下・唇が見える位置にします。
- 歌わない人は、口を閉じた落ち着いた表情にします。
