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
    │   ├── embeddings
    │   └── Lora
    ├── outputs
    ├── .gitignore
    └── README.md
    ```

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

3. `txt2img`タブを選択し，`Prompt`・`Negative prompt`・`Sampling method`などに適切なプロンプトや数値を設定し，`Generate`ボタンを押してください．イラストの生成が開始されます．適切なプロンプトや数値については，以下の`Animagine XL の使い方`を参照してください．

4. その他のstable-diffusion-webuiの使い方については，様々な方がWeb記事などで掲載されていますので，それを参考にしてください．


# Animagine XL の使い方
- **prompt**
    - **Tag**<br>
        最適な結果を得るためには、構造化されたプロンプトテンプレートに従うことをお勧めします<br>
        `1girl/1boy, character name, from which series, by which artists, everything else in any order.`
    - **Quality tags**<br>
        ```
        masterpiece	        > 95%
        best quality	    > 85% & ≤ 95%
        great quality	    > 75% & ≤ 85%
        good quality	    > 50% & ≤ 75%
        normal quality	    > 25% & ≤ 50%
        low quality	        > 10% & ≤ 25%
        worst quality	    ≤ 10%
        ```
    - **Rating tags**<br>
        ```
        safe	            General
        sensitive	        Sensitive
        nsfw	            Questionable
        explicit, nsfw	    Explicit
        ```
    - **Year tags**<br>
        ```
        newest	    2021 to 2024
        recent	    2018 to 2020
        mid	        2015 to 2017
        early	    2011 to 2014
        oldest	    2005 to 2010
        ```
    - **Aesthetic tags**<br>
        ```
        very aesthetic	   > 0.71
        aesthetic	       > 0.45 & < 0.71
        displeasing	       > 0.27 & < 0.45
        very displeasing   ≤ 0.27
        ```
- **Recommended Settings**
    - **Negative prompts**<br>
        ```
        nsfw, lowres, (bad), text, error, fewer, extra, missing, worst quality, jpeg artifacts, low quality, watermark, unfinished, displeasing, oldest, early, chromatic aberration, signature, extra digits, artistic error, username, scan, [abstract]
        ```
    - **Positive prompts**<br>
        ```
        masterpiece, best quality, very aesthetic, absurdres
        ```
    - **Sampling method** : Euler a
    - **Steps** : 30以下
    - **CFG Scale** : 5 ~ 7
