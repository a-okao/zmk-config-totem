# Keymap Editorでキーマップを変更する

[roBa のビルドガイド](https://github.com/kumamuk-git/roBa/blob/main/doc/v2/buildguide_v2.md)や[Zonkey の Keymap Editor 入門記事](https://note.com/goya_k/n/n442a326047e5)と同じく、「自分の GitHub フォークを Keymap Editor で編集し、GitHub Actions でUF2を作る」流れで使います。

上記のサイトも今回の手順とほぼ同じ流れで説明されています。途中で画面操作に迷った場合は、そちらも参考にしつつ、Keymap EditorやZMKの最新情報は各自で確認してください。

## 初回準備

1. GitHub にログインし、このリポジトリを自分のアカウントへ Fork します。
2. Fork したリポジトリの `Actions` タブを開きます。
3. 初回だけ `I understand my workflows, go ahead and enable them` のような確認が出る場合があります。その場合は Actions を有効化します。
4. [Keymap Editor](https://nickcoutsos.github.io/keymap-editor/)を開きます。
5. `GitHub` を選び、Keymap Editor に GitHub アクセスを許可します。
6. リポジトリ一覧から Fork した `zmk-config-totem` を開きます。

## 変更前に確認する

Keymap Editorを開いたら、まず現在のキーマップを確認します。

1. レイヤーを切り替えながら、各キーに何が割り当てられているかを見ます。
2. 親指キーなど、`&lt` や `&mo` が入っているキーを確認します。
3. Bluetooth設定やリセット系のキーがある `SYS` レイヤーを確認します。
4. 変更したいキーと、変更後に使うレイヤー番号を決めます。

先に全体を確認しておくと、レイヤー移動用のキーを消してしまう事故を避けやすくなります。

## キーマップを変更する

1. キーをクリックします。
2. 右側の編集欄で割り当てたい動作を選びます。
3. 文字キーは `&kp A`、`&kp ENTER`、`&kp BSPC` のような `Key Press` を使います。
4. 押している間だけレイヤーを有効にするキーは `&mo 1` のような `Momentary Layer` を使います。
5. タップでキー入力、長押しでレイヤー切り替えにするキーは `&lt 1 SPACE` のような `Layer-Tap` を使います。
6. タップでキー入力、長押しで修飾キーにするキーは `&mt LSHIFT A` のような `Mod-Tap` を使います。
7. 何もしないキーは `&none`、下のレイヤーへ処理を渡すキーは `&trans` を使います。

ZMKでは、`&kp`、`&lt`、`&mo`、`&trans` のような先頭の部分をBehaviorとして扱います。Keymap Editorでは、キーそのものだけでなく、このBehaviorの種類を意識して変更します。

このリポジトリのレイヤー番号は、`config/totem.keymap` に並んでいる順で決まります。

- `0`: `BASE`
- `1`: `NUM`
- `2`: `NAV`
- `3`: `SYM`
- `4`: `SYS`

例えば `BASE` の親指キーにある `&lt 1 LANG2` は、「タップすると `LANG2`、長押しすると `NUM` レイヤー」を意味します。`&lt 3 SPACE` は、「タップすると Space、長押しすると `SYM` レイヤー」です。

日本語入力切り替えやJIS配列の記号は、OS側のキーボード設定によって表示名と実際の入力がずれる場合があります。記号キーを変更したときは、ファームウェアを書き込んだ後に実機で入力結果を確認してください。

## 保存してビルドする

1. Keymap Editor 右上の保存ボタンで変更を保存します。
2. 保存時に commit message を求められた場合は、`Update keymap` など分かりやすい名前にします。
3. Fork したリポジトリの GitHub ページへ戻ります。
4. `Actions` タブで新しいビルドが始まっていることを確認します。
5. ビルドが成功したら、最新の workflow run を開き、Artifacts から `firmware.zip` をダウンロードします。
6. `firmware.zip` を展開します。

## UF2を書き込む

1. 左手側の TOTEM を USB で PC に接続します。
2. リセットボタンを素早く2回押し、ブートローダーモードにします。
3. マスストレージとして表示されたドライブへ、`totem_left-seeeduino_xiao_ble-zmk.uf2` をドラッグ&ドロップします。

通常のキーマップ変更では、左手側だけに書き込めば反映されます。

ZMKの分割キーボードでは、central側がキーマップ処理を行います。このTOTEM設定では左手側がcentralに設定されているため、Keymap Editorでキー配置を変更しただけなら左手側の更新で足ります。

ただし、Bluetooth設定、split通信、左右両方に適用されるZMK設定など、ファームウェアの根幹に関わる変更を行った場合は、左右両方に書き込んでください。その場合は、左手側に `totem_left-seeeduino_xiao_ble-zmk.uf2`、右手側に `totem_right-seeeduino_xiao_ble-zmk.uf2` を書き込みます。

Keymap Editorを使う場合、通常はリポジトリ内のファイルを直接編集しません。ブラウザ上のUIでキーを変更し、Keymap Editorが変更内容をGitHubへ保存します。

## おまけ: バッテリー残量を確認する

[zmk-battery-center](https://github.com/kot149/zmk-battery-center) を使うと、ZMKキーボードのバッテリー残量をPCのシステムトレイから確認できます。分割キーボードのcentral側とperipheral側、つまり左右それぞれのバッテリー残量表示に対応しています。TOTEMは左手が親機（central）、右手が子機（peripheral）となります。

## 注意点

- Keymap Editor で保存する前に、変更対象が自分の Fork になっていることを確認してください。
- `config/boards/shields/totem/totem.keymap` は通常の編集対象ではありません。
- Keymap Editor は複雑な C プリプロセッサマクロを多用した keymap の再保存が苦手です。この設定では、エディタで扱いやすいようにレイヤーの `bindings` を素直な devicetree 形式で保っています。
- キーコード名に迷ったら [ZMK Keycodes](https://zmk.dev/docs/codes/) を確認してください。
- `&mo`、`&lt`、`&tog` などのレイヤー操作は、レイヤー番号がずれると意図しない層が開きます。レイヤーを並べ替える場合は、各キーに入っている番号も見直してください。
- Bluetooth 接続先を消す `BT_CLR` やリセット系のキーは、誤操作を避けるため `SYS` など普段触らないレイヤーに置くのがおすすめです。

## 参考

- [Keymap Editor](https://github.com/nickcoutsos/keymap-editor): ブラウザでZMKキーマップを編集するツール
- [roBa buildguide_v2.md](https://github.com/kumamuk-git/roBa/blob/main/doc/v2/buildguide_v2.md): roBaのZMK/Keymap Editorを使ったビルドガイド
- [Zonkey向けKeymap Editor入門記事](https://note.com/goya_k/n/n442a326047e5): Keymap Editorの画面操作を追いやすい入門記事
- [urob/zmk-config](https://github.com/urob/zmk-config): 高度なZMK設定例がまとまっている参考リポジトリ
- [zmk-battery-center](https://github.com/kot149/zmk-battery-center): ZMKキーボードの左右バッテリー残量を確認できるツール
- [ZMK User Setup](https://zmk.dev/docs/user-setup): ZMKユーザー設定リポジトリ作成の公式ドキュメント
- [ZMK Keymaps](https://zmk.dev/docs/keymaps): ZMKキーマップ全般の公式ドキュメント
- [ZMK Layer Behaviors](https://zmk.dev/docs/keymaps/behaviors/layers): ZMKのレイヤー操作Behaviorの公式ドキュメント
- [ZMK Split Keyboards](https://zmk.dev/docs/features/split-keyboards): ZMK分割キーボードのcentral/peripheral構成の公式ドキュメント
