# Japanese Tokenizer for SpamAssassin

## Overview

This is a patch for Japanese Tokenizer for SpamAssassin.
When applying this patch, the Bayes filter of SpamAssassin can tokenize Japanese mail messages and learn Japanese tokens properly.
As a result, the accuracy of the Bayes filter in Japanese mail improves.

### Feature

- Tokenizer plugin which adds tokenizer function as pre-processing of Bayes filter.
- Tokenizer::SimpleJA plugin as Japanese implementation of Tokenizer plugin.
    - Plugin that tokenize Japanese messages by scripts (Han, Hiragana, Katakana, and the others)
- Tokenizer::MeCab plugin as Japanese implementation of Tokenizer plugin.
    - Plugin that tokenize Japanese messages by MeCab morphological analyzer
- Improvement of Japanese processing in Bayes filter
- Improvement of detection processing of Japanese character encoding

Note that these features can be used when `normalize_charset` option is enabled.

## Overview (for Japanese)

これは SpamAssassin 用日本語トークナイザーのパッチです。
SpamAssassinのベイズフィルターにおいて、日本語の文章の分かち書きを行い、適切に日本語のトークンを学習できるようになります。この結果として、日本語メールのベイズフィルターの判定精度が向上します。

### 機能

- ベイズフィルターの前処理としてトークナイザー機能を追加する Tokenizer プラグインの追加
- Tokenizerプラグインの日本語対応の実装として、 Tokenizer::SimpleJA プラグインを追加
    - 文字種（漢字、ひらがな、カタカナ、それ以外）により分かち書きを行うプラグイン
- Tokenizerプラグインの日本語対応の実装として、 Tokenizer::MeCab プラグインを追加
    - 形態素解析器MeCabにより分かち書きを行うプラグイン
- ベイズフィルターにおける日本語処理の改善
- 日本語の文字エンコーディングの検出処理の改善

なお、これらの機能は `normalize_charset` 機能（UTF-8エンコーディングに変換して評価する機能）が有効なときに利用できます。

## LICENSE

- [Apache License, Version 2.0](LICENSE)

## AUTHOR

- Takashi Takizawa
