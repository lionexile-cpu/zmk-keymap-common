# zmk-keymap-common

jisaku_1(40キー)とaerogu34(34キー)で共有するZMKキーマップ定義。

## 仕組み

- `include/fue/keymap34.dtsi` に全レイヤーのキー割り当て・コンボ・JIS定義・ホールドタップ設定を集約
- 各キーボードのリポジトリが `config/west.yml` でこのリポジトリをZephyrモジュールとして取り込み、
  各 `.keymap` は共通定義を自機のマトリクスへ展開するだけの薄いラッパー
  - [zmk-config-jisaku1](https://github.com/lionexile-cpu/zmk-config-jisaku1)（40キー: 最下段外側3キー×2は&none）
  - [zmk-keyboard-aerogu34](https://github.com/lionexile-cpu/zmk-keyboard-aerogu34)（34キー）

## キーマップの変え方

1. `include/fue/keymap34.dtsi` を編集してmainへコミット
2. 両キーボードのリポジトリでGitHub Actionsを実行（Actionsタブ → Run workflow）
3. Artifactsから `.uf2` をダウンロードして各キーボードに書き込み

※ DYA Studioで実機編集したキーマップは本体の設定領域に保存され、ファーム書き込み後も優先される。
初期キーマップを反映させるには `settings_reset.uf2` を書いてからファームを書き込む。

## 共通論理レイアウト（キー位置0〜33）

```
  0  1  2  3  4     5  6  7  8  9
 10 11 12 13 14    15 16 17 18 19
 20 21 22 23 24    25 26 27 28 29
          30 31    32 33
```

- レイヤー: 0=Default / 1=Function / 2=Number / 3=Scroll / 4=Mouse
- コンボ: Tab=S+D, Shift+Tab=D+F, BT_CLR=Q+T(Scroll), Bootloader=W+E+R(Scroll),
  sys_reset=X+C+V(Scroll), soft_off=U+I+O(Scroll), Win/Alt=下段端キーの同時押し
