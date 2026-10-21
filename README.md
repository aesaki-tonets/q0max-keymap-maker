# Q0 Max keymap.c メーカー

Keychron Q0 Max（ノブ付き）用の、レイヤーごとに色が変わるファーム（QMK、Keychron 2025q3 ブランチ）の keymap.c を作るツールです。

- キーの割り当て、ノブ、レイヤーの色、マクロ（M16〜、数の上限なし）をブラウザで編集できます。
- 作った keymap.c は**自分のパソコンに保存**します。次に使うときは、その keymap.c を読み込むと続きから編集できます。
- このリポジトリには keymap.c（個人のマクロ）を置きません。

## ツールを使う

- Web版：このリポジトリの GitHub Pages の URL を開く（Chrome か Edge）。
- ダウンロード版：`index.html` をダウンロードして、ダブルクリックで開く。インターネットにつながっていなくても動きます。

保存・読み込みは「保存・読み込み」欄の「keymap.c をファイルに保存」「keymap.c を読み込む」で行います。
QMK のソースのフォルダを選ぶと、そこへ直接保存・読み込みもできます（Chrome / Edge のみ）。

## ビルドして書き込む

### A. 自分のパソコンでビルド（QMK MSYS がある場合）

1. QMK MSYS で `qmk setup Keychron/qmk_firmware -b 2025q3 -H C:/qmk_keychron_2025q3`（初回だけ）。
2. ツールで keymap.c を `C:\qmk_keychron_2025q3\keyboards\keychron\q0_max\encoder\keymaps\layer_color\` に保存（rules.mk も無ければ作られます）。
3. ツールの「ビルドと書き込み」欄のコマンドを QMK MSYS で実行。

### B. GitHub でビルド（QMK MSYS が無い場合）

keymap.c は**自分用の非公開（Private）リポジトリ**にだけ置きます。

**最初の1回だけ**

1. このリポジトリの右上の「**Use this template**」→「Create a new repository」。
2. Repository name（例：`q0max-mine`）を入れ、**Private** を選んで「Create repository」。
3. ツールの「GitHub でビルドする」欄の「自分の非公開リポジトリ」に `ユーザー名/q0max-mine` を入れる（ブラウザが覚えます）。

**毎回**

1. ツールの「1. keymap.c をファイルに保存」。
2. 「2. アップロード画面を開く」→ 保存した keymap.c をドラッグ →「Commit changes」。
3. 「3. ビルドの様子（Actions）を開く」。黄色の丸＝実行中、緑のチェック＝成功（3〜5分）、赤い×＝失敗。
4. 緑になった行を開き、下の「Artifacts」の `q0max_layer_color_firmware` をダウンロード（zip の中に .bin）。

公開（Public）のリポジトリではビルドしません（公開リポジトリの Artifacts は誰でもダウンロードできるため、マクロの中身が漏れないようにしています）。

### 書き込み（.bin を使う場合）

1. Launcher で「エクスポート」しておく（書き込むと Launcher のマクロ M0〜M15 とキー割り当ては消えます）。
2. QMK Toolbox で .bin を開く。背面スイッチを真ん中（Cable）にして、0 のキーキャップ下のリセットボタンを押したまま USB を挿す。
3. 「STM32 DFU device connected」と出たら「Flash」。途中の「dfuERROR … firmware is corrupt」は正常。
4. Launcher で「インポート」して戻す。USB を抜いて 10 秒後に挿し直し、設定が残っているか確認。

純正に戻すときは、Launcher の「ファームウェアアップデート」から純正のファームを書き込みます。

## 注意

- 非公式のツールです。書き込みは自己責任で行ってください。
- 文字列のマクロは、パソコンの日本語入力をオフ（半角英数）にして使ってください。日本語の文字は打てません。
