## このリポジトリについて

本リポジトリは、[GEIGEIGEIST/zmk-config-totem](https://github.com/GEIGEIGEIST/zmk-config-totem) をフォーク元としています。フォーク元リポジトリの内容を日本語に翻訳し、キーマップの変更方法、特に Keymap Editor を使ったキーマップ変更手順がわかるように説明を追加したものです。

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



## キーマップの変更方法

キーマップは、以下のどちらかの方法で変更できます。
どちらの方法でも、リポジトリのForkとGitHub ActionsでのビルドにGitHubアカウントが必要です。

- [TOTEM標準の方法で変更する](docs/keymap-standard.md)
- [Keymap Editorで変更する](docs/keymap-editor.md)（おすすめ）

## 参考

- [GEIGEIGEIST/zmk-config-totem](https://github.com/GEIGEIGEIST/zmk-config-totem): TOTEM向けZMK設定の元リポジトリ
- [GEIGEIGEIST/TOTEM](https://github.com/GEIGEIGEIST/TOTEM): TOTEM本体のハードウェア情報とビルドガイド
- [Keymap Editor](https://github.com/nickcoutsos/keymap-editor): ブラウザでZMKキーマップを編集するツール
- [roBa buildguide_v2.md](https://github.com/kumamuk-git/roBa/blob/main/doc/v2/buildguide_v2.md): roBaのZMK/Keymap Editorを使ったビルドガイド
- [Zonkey向けKeymap Editor入門記事](https://note.com/goya_k/n/n442a326047e5): Keymap Editorの画面操作を追いやすい入門記事
- [urob/zmk-config](https://github.com/urob/zmk-config): 高度なZMK設定例がまとまっている参考リポジトリ
- [ZMK User Setup](https://zmk.dev/docs/user-setup): ZMKユーザー設定リポジトリ作成の公式ドキュメント
- [ZMK Keymaps](https://zmk.dev/docs/keymaps): ZMKキーマップ全般の公式ドキュメント
- [ZMK Layer Behaviors](https://zmk.dev/docs/keymaps/behaviors/layers): ZMKのレイヤー操作Behaviorの公式ドキュメント
