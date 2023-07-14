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
    │   ├── embeddings
    │   └── Lora
    ├── outputs
    ├── .dockerignore
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

2. Dockerコンテナのログにて`Running on local URL: ~`が表示されたことを確認後，ブラウザから`localhost:7860`にアクセスし，`Settings -> Stable Diffusion -> SD VAE`の項目で使用するVAEを変更します．その後，`Apply settings`を押して設定を反映します．<br>
もし`localhost:7860`にアクセスできない場合は，Dockerコンテナが正常に動作しているか，または他のアプリケーションが`7860`ポートを使用していないか確認してください．

3. stable-diffusion-webuiの基本的な使い方については，様々な方がWeb記事などで掲載されていますので，それを参考にしてください．


# Abyss Orange Mix3 の使い方
- prompt
    - negative prompt は，できるだけシンプルが良いです．<br>
        `(worst quality, low quality:1.4)`
    - リアルな顔を避ける<br>
        `(realistic, lip, nose, tooth, rouge, lipstick, eyeshadow:1.0), (abs, muscular, rib:1.0)`
    - ボケを避ける<br>
        `(depth of field, bokeh, blurry:1.4)`
    - モザイクを除去する<br>
        `(censored, mosaic censoring, bar censor, convenient censoring, pointless censoring:1.0)`
    - 赤ら顔を除去する<br>
        `(blush, embarrassed, nose blush, light blush, full-face blush:1.4)`
    - NSFWを除去する<br>
        `(trembling, motion lines, motion blur, emphasis lines:1.2)`
    - 🔰アニメ美少女のための基本的なnegative prompt
        - v1<br>
            `nsfw, (worst quality, low quality:1.4), (realistic, lip, nose, tooth, rouge, lipstick, eyeshadow:1.0), (dusty sunbeams:1.0), (abs, muscular, rib:1.0), (depth of field, bokeh, blurry:1.4),(motion lines, motion blur:1.4), (greyscale, monochrome:1.0), text, title, logo, signature`
        - v2<br>
            `nsfw, (worst quality, low quality:1.4), (lip, nose, tooth, rouge, lipstick, eyeshadow:1.4), (blush:1.2), (jpeg artifacts:1.4), (depth of field, bokeh, blurry, film grain, chromatic aberration, lens flare:1.0), (1boy, abs, muscular, rib:1.0), greyscale, monochrome, dusty sunbeams, trembling, motion lines, motion blur, emphasis lines, text, title, logo, signature`
- Sampler : お好みで選んでください
- Steps :
    - DPM++ SDE Karras: Test: 12～ ,illustration: 20～
    - DPM++ 2M Karras: Test: 20～ ,illustration: 28～
- Clipskip : 1 or 2
- CFG : 8 (6～12)
- Upscaler :
    - 詳細なイラスト :<br>
        - Latent (nearest-exact)
        - Denoising strength : 0.5 (0.5~0.6)
    - シンプルなアップスケール :<br>
        - Swin IR, ESRGAN, Remacri など…
        - Denoising strength : 低く設定することも可能です (0.35~0.6)
