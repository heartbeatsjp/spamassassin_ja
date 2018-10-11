# Installation

## Installation

### 準備

次のソフトウェアを事前にインストールしてください。
なお、2,3,4に関してはTokenizer::MeCabプラグインを使う場合に必要です。
5,6,7は必須ではないですが、それぞれ日本語と中国語の検出制度が向上します。

1. 文字エンコーディング検出器Encode::Detect
    - 配布元: https://metacpan.org/pod/Encode::Detect
2. 形態素解析エンジンMeCab
    - 必要とするバージョン: 0.996以降
    - 配布元: https://taku910.github.io/mecab/
    - インストール時の注意事項:
        - ./configureのオプションで"--with-charset=utf8"を付ける必要がある。
3. MeCabの辞書mecab-ipadic
    - 必要とするバージョン: 2.7.0-20070801以降
    - 配布元: https://taku910.github.io/mecab/
    - インストール時の注意事項:
        - ./configureのオプションで"--with-charset=utf8"を付ける必要がある。
4. MeCabのPerlバインディングmecab-perl
    - 必要とするバージョン: 0.996以降
    - 配布元: https://taku910.github.io/mecab/
5. JIS X 0213対応 日本語エンコーディングモジュール Encode::JIS2K
    - 配布元: https://metacpan.org/pod/Encode::JIS2K
6. 中国語拡張エンコーディングモジュール Encode::HanExtra
    - 配布元: https://metacpan.org/pod/Encode::HanExtra
7. Microsoft Windows互換日本語エンコーディングモジュールEncode::EUCJPMS
    - 配布元: https://metacpan.org/pod/Encode::EUCJPMS

### ダウンロード

次のサイトからパッチをダウンロードできます。

https://github.com/heartbeatsjp/spamassassin_ja/patches/

以下のファイルをダウンロードできます。

- spamassassin-3.4.x-japanese-tokenizer.patch (a patch file for Japanese Tokenizer)
- tokenizer.pre (a configuration file for Japanese Tokenizer)

### インストール

SpamAssassinのtar ballを展開後、このパッチを当ててください。

```
cd Mail-SpamAssassin-3.4.x
patch -p1 < spamassassin-3.4.x-japanese-tokenizer.patch
```

後は、通常のSpamAssassinのインストールと同じです。

## 設定

1. 設定ファイル `lcoal.cf` に次の行を記述します。

    ```
    normalize_charset 1
    ```
2. `tokenizer.pre` を `local.cf` と同じディレクトリにコピーします。
3. （MeCabプラグインを使う場合）`tokenizer.pre` を編集し、SimpleJAプラグインの行をコメントアウトし、MeCabプラグインの行頭の `#` を削除して有効にします。

    ```
    # Tokenizer::SimpleJA
    #
    #loadplugin Mail::SpamAssassin::Plugin::Tokenizer::SimpleJA
    
    # Tokenizer::MeCab
    #
    loadplugin Mail::SpamAssassin::Plugin::Tokenizer::MeCab
    ```
4. `spamassassin --lint` を実行して、ワーニングが出ていないかを確認します。

    ```
    spamassassin --lint
    ```
5. 以上で設定が完了しましたので、spamd等のデーモンを利用している人はデーモンを再起動してください。

