# インストール手順

以下は，Dockerを用いたstable-diffusion-webuiの環境構築の手順についてです．

## ファイル配置
1. 以下のようなファイル構成を持つディレクトリを作成します．この際に`models`ディレクトリとそのサブディレクトリ，そして`outputs`ディレクトリを作成します．
    ```
    .
    ├── docker-compose
    │   ├── .env
    │   └── docker-compose.yml
    ├── Dockerfile
    │   ├── Dockerfile
    │   ├── download_model.py
    │   └── requirements.txt
    ├── models
    │   ├── checkpoint
    │   └── Lora
    ├── outputs
    ├── .gitignore
    └── README.md
    ```
2. `models/checkpoint`ディレクトリに使用するモデルを配置します．

## Dockerイメージのビルド

1. コマンドプロンプト（またはターミナル）でディレクトリ内の`docker-compose`ディレクトリに移動します．移動するためには，以下のようなコマンドを使用します．
    ```
    cd docker-compose
    ```

2. Dockerイメージを作成するため，以下のコマンドを実行します．
    ```
    docker-compose build
    ```
    実行結果として，必要なDockerイメージがビルドされます．

## 起動と設定
1. Dockerコンテナを起動するため，以下のコマンドを実行します．
    ```
    docker-compose up -d
    ```
    実行結果として，stable-diffusionのDockerコンテナがバックグラウンドで実行されます．<br>
    以下のコマンドを実行することで，稼働中のコンテナのログがリアルタイムで表示されます．これにより，アプリケーションの動作状況やエラーの発生を確認することができます．
    ```
    docker-compose logs -f
    ```

2. Dockerコンテナのログにて`Running on local URL: ~`が表示されたことを確認後，ブラウザから[http://localhost:7860/](http://localhost:7860/)にアクセスしてください．もし[http://localhost:7860/](http://localhost:7860/)にアクセスできない場合は，Dockerコンテナが正常に動作しているか，または他のアプリケーションが`7860`ポートを使用していないか確認してください．

3. `txt2img`タブを選択し，`Prompt`・`Negative prompt`・`Sampling method`などに適切なプロンプトや数値を設定し，`Generate`ボタンを押してください．イラストの生成が開始されます．適切なプロンプトや数値については，以下の`Ebara Pony の使い方`を参照してください．

4. その他のstable-diffusion-webuiの使い方については，様々な方がWeb記事などで掲載されていますので，それを参考にしてください．


# Ebara Pony の使い方
可愛い系の画像に特化したPony系モデル
- prompt
    - ポジティブ<br>
        `score_9, score_8_up, score_7_up` `source_anime`
    - ネガティブ<br>
        空でも良いが，Ponyのデフォルトネガティブを使うこともできる<br>
        `score_6_up, score_5_up, score_4_up, source_furry, source_pony, source_cartoon, realistic, 3d, monochrome, blurry, watermark`
- Sampling method : Euler A
- Steps : 30
- CFG Scale : 7 ~ 10
- Upscaler :
    - Hires
        - Denoise : 0.4
        - Steps : 15
        - Upscaler : 4x-AnimeSharp
