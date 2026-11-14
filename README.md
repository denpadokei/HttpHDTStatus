# HttpHDTStatus

[![Build and Release](https://github.com/denpadokei/HttpHDTStatus/actions/workflows/build-and-release.yml/badge.svg)](https://github.com/denpadokei/HttpHDTStatus/actions/workflows/build-and-release.yml)

HeadDistanceTravelled から HMD の移動距離・位置・回転を取得し、HttpSiraStatus のステータスに追加して送信する MOD です。オーバーレイや外部ツールで頭の移動量を表示できます。

## 機能

- HeadDistanceTravelled の距離更新イベントを購読し、HMD の移動距離を受け取ります
- HMD の座標 (`x` / `y` / `z`) を `Position` として送信します
- HMD のオイラー角 (`x` / `y` / `z`) を `Rotation` として送信します
- HeadDistanceTravelled が持つ移動距離を `Distance` として送信します
- HttpSiraStatus の `Other` に `HeadDistanceTravelled` オブジェクトを追加します
- 距離が更新されるたびに `Other` の変更としてステータスを送信します
- プレイヤーシーンにのみインストールされるため、ゲームプレイ中に動作します

## 動作環境

| 項目 | 内容 |
| --- | --- |
| Beat Saber | 1.34.2 |
| 依存 MOD | BSIPA ^4.3.2 / HttpSiraStatus ^11.0.0 / SiraUtil ^3.0.0 / HeadDistanceTravelled <1.0.0 |

## インストール

1. Beat Saber を 1.34.2 に合わせる (BSManager などのバージョン管理ツールを推奨)
2. BSIPA と上記の依存 MOD をインストールする
3. [Releases](https://github.com/denpadokei/HttpHDTStatus/releases) から `HttpHDTStatus-2.0.0-bs1.34.2.zip` をダウンロードし、`Plugins` フォルダをゲームフォルダへ上書きコピーする

## 使い方

HttpSiraStatus の WebSocket に接続すると、ステータスの `other` に次のオブジェクトが含まれます (距離が更新されるたびに送信されます)。

```json
{
    "HeadDistanceTravelled": {
        "Position": {
            "x": 0.0,
            "y": 0.0,
            "z": 0.0
        },
        "Rotation": {
            "x": 0.0,
            "y": 0.0,
            "z": 0.0
        },
        "Distance": 0.0
    }
}
```

`Rotation` は HMD のオイラー角です。この MOD 自体に設定項目はありません。

## ビルド

```powershell
git clone https://github.com/denpadokei/HttpHDTStatus.git
cd HttpHDTStatus
dotnet build .\HttpHDTStatus\HttpHDTStatus.csproj -c Release
```

`BeatSaberDir` (または `GameDirectory`) に Beat Saber のインストール先を設定すると、ゲームの参照アセンブリを解決できます。

GitHub Actions の `build-and-release.yml` が push ごとにビルドし、`X.X.X` 形式のタグを push するとリリースを作成します。

## ライセンス

MIT
