# TOTEM標準の方法でキーマップを変更する

`config/totem.keymap` を直接編集し、GitHub Actionsでファームウェアをビルドする方法です。

## 手順

1. このリポジトリをフォークします。
2. 自分のリポジトリを `git clone` して、PC 上にローカルコピーを作成します。
3. `config/totem.keymap` を編集します。
4. 自分のフォークへ `git push` します。
5. GitHub 上のフォークしたリポジトリページで `Actions` に移動します。
6. 最新ファームウェアが含まれる `firmware.zip` をダウンロードして展開します。
7. TOTEM の左半分を PC に接続し、リセットを2回押します。
8. キーボードがマスストレージデバイスとして表示されます。
9. `totem_left-seeeduino_xiao_ble-zmk.uf2` を、そのストレージデバイスへドラッグ&ドロップします。

キーコードは [ZMK Keycodes](https://zmk.dev/docs/codes/) を確認してください。

## 書き込む側

通常のキーマップ変更では、左手側だけに `totem_left-seeeduino_xiao_ble-zmk.uf2` を書き込めば反映されます。

ZMKの分割キーボードでは、central側がキーマップ処理を行います。このTOTEM設定では左手側がcentralに設定されているため、`config/totem.keymap` のキー配置を変更しただけなら左手側の更新で足ります。

ただし、以下のようなファームウェアの根幹に関わる変更を行った場合は、左右両方に書き込んでください。

- Bluetoothやsplit通信に関わる設定を変更した場合
- `config/*.conf` を変更した場合
- `build.yaml` やshield定義を変更した場合
- `config/boards/shields/totem/` 以下を変更した場合
- 左右両方に適用されるZMK設定を変更した場合

その場合は、左手側に `totem_left-seeeduino_xiao_ble-zmk.uf2`、右手側に `totem_right-seeeduino_xiao_ble-zmk.uf2` を書き込みます。

## 編集対象

編集対象は `config/totem.keymap` のみです。

`build.yaml`、`config/boards/shields/totem/` 以下のファイル、その他の設定ファイルは通常編集しないでください。これらを変更すると、ビルド対象やキーボード定義が変わり、ファームウェアが正しく生成されない場合があります。

参考: https://zmk.dev/docs/features/split-keyboards
