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
    │   └── requirements.txt
    ├── models
    │   ├── control-net
    │   ├── embeddings
    │   ├── Lora
    │   ├── stable-diffusion (ここに.safetensors拡張子のモデルを配置してください)
    │   └── vae (ここに.safetensors拡張子のVAEを配置してください)
    ├── outputs
    ├── .dockerignore
    ├── .gitignore
    └── README.md
    ```

2. 使用したいモデルファイルを`models/stable-diffusion`ディレクトリに配置します．モデルファイルは様々な種類があり，どれを使うかはあなたのプロジェクトや好みによります．例として，2023年5月時点では以下のサイトからダウンロードすることができます．（URLは変わる可能性があるため，必ず最新の情報を確認してください）
    - [cetus-mix](https://civitai.com/models/6755/cetus-mix)
    - [OrangeMixs](https://huggingface.co/WarriorMama777/OrangeMixs)

3. VAEモデルを`models/vae`ディレクトリに配置します．VAEも様々な種類があり，どれを使うかはあなたのプロジェクトや好みによります．例として，2023年5月時点では以下のサイトからVAEモデルをダウンロードできます．（URLは変わる可能性があるため，必ず最新の情報を確認してください）
    - [vae-ft-mse-840000-ema-pruned](https://huggingface.co/stabilityai/sd-vae-ft-mse-original/tree/main)

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

2. Dockerコンテナのログにて`Model loaded in ~: `が表示されたことを確認後，ブラウザから`localhost:7860`にアクセスし，`Settings -> Stable Diffusion -> SD VAE`の項目で使用するVAEを変更します．その後，`Apply settings`を押して設定を反映します．<br>
もし`localhost:7860`にアクセスできない場合は，Dockerコンテナが正常に動作しているか，または他のアプリケーションが`7860`ポートを使用していないか確認してください．

3. stable-diffusion-webuiの基本的な使い方については，様々な方がWeb記事などで掲載されていますので，それを参考にしてください．
