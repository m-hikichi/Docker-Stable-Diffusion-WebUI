# インストール手順

以下は，Dockerを用いたstable-diffusionのインストール手順です．

## クローンとビルド
1. `AUTOMATIC1111/stable-diffusion-webui`リポジトリをクローンするために，コマンドプロンプト（またはターミナル）を開き，リポジトリルートにて以下のコマンドを実行します．
    ```
    git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git -b 1.1.1
    ```
    実行結果として，stable-diffusionの1.1.1バージョンがローカル環境にクローンされます．

2. コマンドプロンプト（またはターミナル）でディレクトリ内の`docker-compose`ディレクトリに移動します．移動するためには，以下のようなコマンドを使用します．
    ```
    cd docker-compose
    ```

3. Dockerイメージを作成するため，以下のコマンドを実行します．
    ```
    docker-compose build
    ```
    実行結果として，必要なDockerイメージがビルドされます．

## ファイル配置
4. 必要なモデルファイルを`stable-diffusion-webui/models/Stable-diffusion`ディレクトリに配置します．モデルファイルは様々な種類が存在し，その取得元も様々です．用途や好みに合わせて適切なモデルを選択してください．一例として，2023年5月時点では以下のサイトからダウンロードすることができます．（URLは変わる可能性があるため，必ず最新の情報を確認してください）
    - [cetus-mix](https://civitai.com/models/6755/cetus-mix)
    - [OrangeMixs](https://huggingface.co/WarriorMama777/OrangeMixs)

5. VAEモデルを`stable-diffusion-webui/models/VAE`ディレクトリに配置します．VAEもまた様々な種類が存在し，その取得元は多岐にわたります．用途や好みに合わせて適切なVAEモデルを選択してください．一例として，2023年5月時点でのVAEモデルのダウンロードURLは以下の通りです．（URLは変わる可能性があるため，必ず最新の情報を確認してください）
    - [vae-ft-mse-840000-ema-pruned](https://huggingface.co/stabilityai/sd-vae-ft-mse-original/tree/main)

## 起動と設定
6. Dockerコンテナを起動するため，以下のコマンドを実行します．
    ```
    docker-compose up -d
    ```
    実行結果として，stable-diffusionのDockerコンテナがバックグラウンドで実行されます．<br>
    以下のコマンドを実行することで，稼働中のコンテナのログがリアルタイムで表示されます．これにより，アプリケーションの動作状況やエラーの発生を確認することができます．
    ```
    docker-compose logs -f
    ```

7. Dockerコンテナのログにて`Startup time: `が表示されたことを確認後，ブラウザから`localhost:7860`にアクセスし，`setting -> stable diffusion -> SD VAE`の項目で使用するVAEを変更します．その後，`Apply settings`を押して設定を反映します．
