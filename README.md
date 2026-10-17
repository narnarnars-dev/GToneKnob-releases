# GToneKnob

ギターのボリュームとトーンを 10 にして録った DI 音に、あとからギター本体のボリュームノブやトーンノブを回したような効果をかけるオーディオプラグインです。

An audio plugin that applies the effect of turning your guitar's volume and tone knobs to DI tracks recorded with both knobs at 10. [English summary below](#english).

## ダウンロード

[Releases](../../releases) から、お使いの OS の zip をダウンロードしてください。

| OS | ファイル | 形式 |
|---|---|---|
| macOS 11 以降（Apple Silicon / Intel） | `GToneKnob-x.y.z-mac.zip` | AU / VST3 / Standalone |
| Windows 10 / 11（64 ビット） | `GToneKnob-x.y.z-windows.zip` | VST3 / Standalone |

- インストール方法は、zip に入っている `README.txt` に書いてあります。
- Releases の「Source code」は GitHub が自動で付けるもので、このページの README しか入っていません。ダウンロードする必要はありません。

## テスト版について

- 現在はテスト版です。動作や音について気づいたことがあれば教えてください。
- 署名・公証をしていないため、macOS ではインストール後にターミナルで1行のコマンドを実行する必要があります。Windows ではアプリの起動時に SmartScreen の警告が出ることがあります。

## 使い方

1. ギターのボリュームとトーンを **10** にして、DI 音（アンプを通さない音）を録ります。
2. その DI トラックに GToneKnob を挿し、後ろにアンプシミュレーターなどをつなぎます。
3. Pickup / Pot / Taper / Tone Cap / Cable を、録音したときのギターと環境に合わせます。
4. Volume と Tone を、ギター本体のノブのつもりで回します。

GToneKnob は、ピックアップ・ポット・コンデンサー・ケーブルからなるギターの回路を計算でまねて、「ノブを 10 から動かしたときの変化」だけを録音にかけます。単純な EQ ではないので、ピックアップや配線の設定によって効き方が変わります。

> **大事な前提**
> Volume と Tone 以外のパラメーターは、音色を作るためのつまみではなく、**録音したときのギターに合わせるための設定**です。
> たとえば、ハムバッカーで録った音で Single Coil を選んでも、シングルコイルの音にはなりません。変わるのはノブの効き方だけです。
> どの設定でも、Volume と Tone が 10 なら音はまったく変わりません。

## パラメーター

| パラメーター | 選択肢 / 範囲 | デフォルト |
|---|---|---|
| Volume | 0〜10 | 10 |
| Tone | 0〜10 | 10 |
| Pickup | Single Coil / Humbucker / P-90 | Single Coil |
| Pot | 250k / 500k | 250k |
| Taper | Audio (A) / Linear (B) | Audio (A) |
| Tone Cap | 0.015 / 0.022 / 0.033 / 0.047 / 0.1 µF | 0.022 µF |
| Cable | 50〜2000 pF | 500 pF |

### Volume / Tone

ギター本体のボリュームノブとトーンノブにあたります。ストラトのノブと同じく約300°回転し、数字の刻まれたスカートがノブと一緒に回ります。上に固定された三角マークの位置で値を読みます。ダブルクリックで 10 に戻ります。

**Tone** を下げると、実機と同じように高域が削れます。0 付近では、中域がこもった、いわゆるウーマントーンの音になります。

**Volume** を下げると、実機と同じように次のことが起きます。

- **音量が下がる**：Audio (A) カーブの 250k ポットなら、8 で約 −8 dB、6 で約 −16 dB、4 で約 −25 dB です。0 では完全に無音になります。
- **高域の質感が変わる**：3 kHz 前後のプレゼンス帯域が数 dB 落ち、音が少し丸くなります。

音量の低下は補正しません。そのため、後ろのアンプシミュレーターの歪み方も、実機でボリュームを絞ったときと同じように変わります。

### Pickup

録音に使ったピックアップの種類を選びます。

| 種類 | 特徴 |
|---|---|
| Single Coil | ストラトなどのシングルコイル。共振のピークが高く、明るい |
| Humbucker | レスポールなどのハムバッカー。共振のピークが低め |
| P-90 | P-90。共振のピークがいちばん低い |

共振のピークの位置が違うと、同じトーン位置でも削れ方が変わります。実際のピックアップはモデルによって値にかなり幅があるので、近いものを選んでください。

### Pot

ボリュームポットとトーンポットの抵抗値です。ギターの仕様書に「250kΩ」「500kΩ」などと書かれています。

一般に、シングルコイルのギターには 250k、ハムバッカーのギターには 500k が使われることが多いです。

### Taper

ノブの角度に対して、ポットの抵抗値がどう変わるかを表すカーブです。ボリュームとトーンの両方に適用されます。

- **Audio (A)**：回転全体にわたって、なだらかに効きます。多くのギターはこちらです。
- **Linear (B)**：中央あたりまではほとんど変わらず、2〜3 より下で急に効きます。

### Tone Cap

トーン回路のコンデンサーの容量です。

容量が大きいほど、トーンを絞ったときに削れ始める周波数が低くなり、こもり方が強くなります。一般に、シングルコイルには 0.022µF や 0.047µF、ハムバッカーには 0.022µF がよく使われます。

### Cable

ギターからオーディオインターフェースまでのケーブルの容量です。

シールドケーブルは、1m あたり約 100pF が目安です（3m で約 300pF、5m で約 500pF）。ケーブルの音は録音にすでに含まれているので、この値はノブを下げたときの効き方にだけ影響します。とくに Volume を下げたときの高域の落ち方が、この値で大きく変わります。

---

## English

GToneKnob models a passive guitar circuit (pickup, pots, tone capacitor, cable) and applies only the change caused by moving the knobs away from 10. Record your DI with the guitar's volume and tone at 10, insert GToneKnob before your amp sim, set the guitar parameters to match the guitar you recorded with, then use Volume and Tone like the knobs on the guitar.

| Parameter | Range | What it does |
|---|---|---|
| Volume | 0–10 | Guitar volume knob. Lowers the level as a real pot does (0 is silent) and softens the presence range |
| Tone | 0–10 | Guitar tone knob. Rolls off the highs; near 0 gives a "woman tone" |
| Pickup | Single Coil / Humbucker / P-90 | The pickup you recorded with |
| Pot | 250k / 500k | Value of the volume and tone pots |
| Taper | Audio (A) / Linear (B) | Pot curve: A is gradual, B acts mostly below 2–3 |
| Tone Cap | 0.015–0.1 µF | Tone capacitor; larger values roll off lower |
| Cable | 50–2000 pF | Cable capacitance (about 100 pF per metre) |

Only Volume and Tone shape the sound. The other parameters describe your guitar and change how the knobs respond. With Volume and Tone at 10, the signal is unchanged.

Download the zip for your OS from [Releases](../../releases); installation steps are in `README.txt` inside the zip. These are unsigned test builds. The "Source code" files on the Releases page are added by GitHub automatically and contain only this README.
