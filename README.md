# zmk-config-AroundFortyRB

Around Forty RB 用の ZMK firmware 設定です。
zmkの薙刀式v16を実装しています。

## 現在の main ブランチ

- ZMK firmware v0.3.0 に対応しています。
- PMW3610 トラックボール用に `badjeff/zmk-pmw3610-driver` を使用しています。
- RGB LED widget 用に `caksoylar/zmk-rgbled-widget` を使用しています。
- ZMK Studio に対応しています。右手側が central で、USB UART snippet を有効にしています。
- `Mac-Base` をデフォルトレイヤー、`Win-Base` を Windows 用レイヤーとして用意しています。
- 薙刀式入力用に `eswai/zmk-naginata` を `west.yml` から取り込んでいます。

利用ガイド:

https://note.com/razily/n/n0b3c5ff58d92

## Build

GitHub Actions では以下の firmware を生成します。

- `AroundForty-RB_R rgbled_adapter`: 右手側。central / ZMK Studio 接続側です。
- `AroundForty-RB_L rgbled_adapter`: 左手側。peripheral 側です。
- `settings_reset`: 設定初期化用 firmware です。

ペアリング情報やレイヤー状態を確実に初期化したい場合は、先に `settings_reset` の UF2 を書き込んでから左右の firmware を入れ直します。

## Keymap

主なレイヤーは以下です。

- `Mac-Base`: デフォルトの macOS 用ベースレイヤーです。
- `Win-Base`: Windows 用ベースレイヤーです。
- `Mac-Fnc` / `Win-Fnc`: ショートカットや記号入力用レイヤーです。
- `Mac-Common` / `Win-Common`: カーソル、ページ移動、マウスボタンなどの共通操作レイヤーです。
- `Num_Scroll`: 数字、記号、カーソル操作用レイヤーです。
- `V_Scroll`: 縦スクロール用レイヤーです。
- `Settings`: Bluetooth、reset、bootloader、ZMK Studio unlock 用レイヤーです。
- `AML`: 右手ホーム周辺のマウスボタン補助レイヤーです。
- `NAGINATA`: 薙刀式入力レイヤーです。

## Settings Layer

Bluetooth profile selection は左右どちらの上段からでも使えます。

- `Q W E R T`: `BT_SEL 0..4`
- `Y U I O P`: `BT_SEL 0..4`

その他、`BT_CLR`、`BT_CLR_ALL`、`sys_reset`、`studio_unlock`、`bootloader` を Settings レイヤーに配置しています。

## Naginata

薙刀式レイヤーは `NAGINATA_LAYER` として追加しています。

- `H + J`: 薙刀式 ON
- `F + G`: 薙刀式 OFF
- `V + M`: Enter

薙刀式レイヤーは既存レイヤーより上位にあるため、`Num_Scroll`、`Mac-Fnc`、`Settings`、`Mac-Common` へ入るキーは `base_mo` / `base_lt` で包んでいます。これにより、薙刀式レイヤー中でも下位の utility レイヤーへ一時的に入れるようにしています。
