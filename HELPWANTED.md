# 「求人募集中」

angrは巨大なプロジェクトで，保守するのは大変です．
コミュニティに貢献し，願わくばフィードバックを得たいという思いから，私たちはここに，遠大なTODOリストを掲載します．
幅広い難易度の，すべてのスキルレベルに応じた課題が（きっと）あるはずです．


## ドキュメンテーション：API

私たちはつねにドキュメンテーションに遅れを取っています．
私たちは現状のドキュメントに何が欠けている把握するため，githubでissueをトラッキングしています：

1. [angr](https://github.com/angr/angr/issues/145)
2. [simuvex](https://github.com/angr/simuvex/issues/28)
3. [claripy](https://github.com/angr/claripy/issues/17)
4. [cle](https://github.com/angr/cle/issues/29)
5. [pyvex](https://github.com/angr/pyvex/issues/34)


## ドキュメンテーション：gitbook

本書にはいくらか核心部分の抜けがあります．
具体的には，下記の要素に改善の余地があります：

1. あちこちに残されたTODOを完遂する．
2. 実例のページを理にかなったやり方で整理する．いまのところ実例のほとんどは極めて冗長で，大部分をシンプルな表にまとめられれば，ページ数をいくらか削減できるかもしれない．


## ドキュメンテーション・開発：angr学習コース

angr初学者に向けた「コース」なるものの開発は，必ずや有益な取り組みとなることでしょう．
これは，[こちら](https://github.com/angr/angr-doc/pull/74)の方向性に沿って実現されつつありますが，さらなる拡張が見込まれます．

回を重ねるごとに難易度が上昇し，段階的にangrの機能を学べるようなハンズオンが理想です．


## 開発：angr-management

angrのGUIである[angr-management](https://github.com/angr/angr-management)には*多大な*伸びしろがあります．
angrの機能を適切に可視化する手法はきっと有用です！


## 開発：アーキテクチャサポートの追加

新しいアーキテクチャに対応すれば，angrはより有用なものとなるでしょう．それには，下記の作業を伴います：

1. アーキテクチャの情報を[archinfo](https://github.com/angr/archinfo)に追加する．
2. IR変換処理を`angr.Block`に追加する．
3. IRパーサを`simuvex`に追加する（おそらくは`simuvex.SimRun`のさらなるサブクラスとして）．
4. SimProcedures対応のために（システムコールを含む）呼び出し規約を`simuvex.SimCC`に追加する．
5. 初期化処理対応のために`angr.SimOS`を追加・改変する．
6. バイナリをロードするCLEバックエンドを作成する．バイナリがELFフォーマットであれば，CLE ELFバックエンドを拡張すればよい．

手順2および3は，アーキテクチャのネイティブコードからVEXへの変換器を書いて済ませることもできます．PyVEX構造体を出力するだけなら，Pythonで事足ります．


### 新しいアーキテクチャ・IRのアイデア

- PIC, AVR, その他組み込みアーキテクチャ
- SPARC（libVEXのSPARCサポートを[準備中](https://bitbucket.org/iraisr/valgrind-solaris)です）
- LLVM IR（に対応できれば，angrをバイナリ解析プラットフォームからプログラム解析プラットフォームへと拡張し，さまざまな機能を追加できるようになります！）


## 開発：環境サポート

私たちは，オペレーティングシステム（すなわち，そのシステムコールによる影響）とライブラリ関数の環境をモデル化するため，「機能の概要」というコンセプトを採用しています．
この拡張は，angrのユーティリティを発展させる大きな助けとなるでしょう．
機能の概要については[こちら](https://github.com/angr/simuvex/tree/master/simuvex/procedures)を参照のこと．

機能の概要の具体的なサブセットはシステムコールを単位としています．
SimProduresのライブラリ関数（これがなくともangrは実際の関数を実行可能です）もさることながら，私たちは未実装のシステムコールを回避する策を少ししか持ち合わせていません．
システムコールの実装次第で，angrの扱えるバイナリの幅が広がります！
