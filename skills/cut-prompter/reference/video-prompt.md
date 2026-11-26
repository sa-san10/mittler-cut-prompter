# 動画プロンプト（ふつうの動画モデル）の書き方

絵（開始フレームなど）と文から動きを作るモデル向けです。声から口パクを作るモデルは `lipsync.md`。

基本は **開始フレームだけ** を渡して、**動きを時刻ごとに細かく書く** 形です。動画モデルは書かれていない動きを勝手に足したり、止まったりしやすいので、何がいつどれだけ動くかを書きます。

## 構成（英語で、この順に書く）

1. **最初の状態**：ショット・場所・人物（見分けられる特徴：髪型・髪飾り・服・年齢と体つき）・視線・光源。開始フレームがあるなら `The shot begins from the first frame and continues it exactly.` を入れます。
2. **時刻ごとの演技**：`Acting, beat by beat (the shot is N.N seconds):` に続けて、`0.0-0.4s: …` の行を時刻の順に、カットの頭から終わりまですき間なく並べます。
   - 1 つの区切りは 0.2〜0.8 秒が目安。速い動き・まばたき・手の向きが変わる所は細かく区切ります。
   - 区切りごとに、体の向きと重心・頭の角度・視線・まばたき・口・眉・手と指（どちらの手・どの指・何をつまむか）・息・髪と服の揺れ・小物の動き・光の変化を、**何がどれだけ動くか** で書きます（`a few millimeters`・`about one centimeter`・`eases to a stop`）。
   - 出てほしい動きはすべて書きます（例：踊りなら `keeps dancing without stopping`。書かないと途中で止まります）。
3. **動かないものの明言**：背景・家具・小物の形と数、人と手の数を言い切ります（`stay perfectly still and keep exactly their shapes`・`only this one person`・`she has two hands with five fingers each`）。
4. **カメラ**：固定・ゆっくり寄る（push-in）・パンなど。動かさないなら `static camera, no pan, no zoom, no cut`。
5. **光**：向きと色は最初のままか、どう変わるか。
6. **画風と見た目の維持**：画風・顔・目の色・髪・服を最初のまま（アニメなら `no 3D rendering, no photorealism`）。
7. **禁止**：`no stutter, no freeze, no morphing`・`no text, captions, logos or watermarks`、そのカットで崩れやすいもの（涙・余計な人や手・顔に落ちる暗い影など）。

## 例（4 秒・開始フレームのみ。② の一部）

```
0.0-0.4s: she stands perfectly still, lips slightly parted, eyes wide, looking at the bright window.
0.4-1.1s: she takes a slow breath in; her shoulders rise about one centimeter; the reflections in her eyes tremble.
1.1-1.3s: she blinks once, slowly.
1.3-2.4s: her eyebrows lift gently and her lips close into the faintest smile; a loose lock of hair at her cheek stirs.
2.4-4.0s: she lifts her chin a few millimeters toward the light and holds the smile; her hands stay at her sides.
```

## 絵の渡し方ごとの違い

- **終了フレームあり**：最後の区切りで終了フレームの状態に着くように書き、`The shot ends exactly on the last frame.` を入れます。途中の動きは控えめになりやすいので、必要な動きははっきり書きます。
- **開始と終了の両方**：始まりと終わりの両方の状態を書き、その間の動きを時刻で書きます。
- **画像なし**：最初の状態を、画像プロンプトと同じくらい具体的に書きます（人物の見た目・場所・光・画風）。

## 長さ

- 2〜10 秒。動画モデルの多くは、長くなるほど生成に時間がかかり、崩れやすくなります。6 秒をこえるなら、分けられないかを先に考えます（`frame-modes.md` の「続きのカット」）。
- 時刻は、生成する動画の頭からの秒で書きます（曲や全体の時間ではありません）。

## 崩れたときの直し方（ユーザーに聞かれたら）

崩れた所を名指しで足します（人物の見た目がずれる → 年齢・体つき・手の形を言い切る／背景が変わる → その物の位置と形を言い切る）。同じ文のまま種だけ変えて何本も作るより、文を直したほうが早いです。
