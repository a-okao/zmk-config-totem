<picture>
  <source media="(prefers-color-scheme: dark)" srcset="/docs/images/TOTEM_logo_dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="/docs/images/TOTEM_logo_bright.svg">
  <img alt="TOTEM logo font" src="/docs/images/TOTEM_logo_bright.svg">
</picture>

# TOTEM 分割キーボード用 ZMK 設定

[こちら](https://github.com/GEIGEIGEIST/totem)で、ハードウェアファイルとビルドガイドを確認できます。\
[こちら](https://github.com/GEIGEIGEIST/qmk-config-totem)で、TOTEM 用の QMK 設定を確認できます。

TOTEM は、[ZMK](https://zmk.dev/) または [QMK](https://docs.qmk.fm/) で動作する 38 キーのカラムスタッガード分割キーボードです。SEEED XIAO BLE または RP2040 での使用を想定しています。


![TOTEM layout](/docs/images/TOTEM_layout.svg)



## 使い方

- このリポジトリをフォークします
- 自分のリポジトリを `git clone` して、PC 上にローカルコピーを作成します（[コマンドライン](https://www.atlassian.com/git/tutorials)または [GitHub Desktop](https://desktop.github.com/) を使用できます）
- `totem.keymap` ファイルを調整します（すべてのキーコードは [ZMK ドキュメント](https://zmk.dev/docs/codes/)で確認できます）
- 自分のフォークへ `git push` します
- GitHub 上のフォークしたリポジトリページで「Actions」に移動します
- 下へスクロールし、最新ファームウェアが含まれる `firmware.zip` アーカイブを展開します
- TOTEM の左半分を PC に接続し、リセットを 2 回押します
- キーボードがマスストレージデバイスとして表示されます
- アーカイブ内の `totem_left-seeeduino_xiao_ble-zmk.uf2` ファイルを、そのストレージデバイスへドラッグ＆ドロップします
- 右半分も同様に、`totem_right-seeeduino_xiao_ble-zmk.uf2` ファイルで同じ手順を繰り返します
