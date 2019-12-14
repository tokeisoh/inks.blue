# Draft

* 重く考えすぎない。さらっと書く。さらっとまとめる。ブランチ上でpublishしながら、整理していく。Qiitaにリンク貼らなきゃバレないし。

[GameplayTagを知ってみる]
1. GameplayTag: ざっくり見てみる
    * ゲーム内の要素、状態などをタグ(ラベル)として表現するためのデータ型。
    * アセット化されたenumのようなやつ。階層を表現できるのが嬉しい。
    * 記念すべき初日は、ひとまず雰囲気をざっと掴める程度のスクショを並べてみる。
    * ss: 使いたいGameplayTagたちのDataTableを用意する
    * ss: プロジェクト設定で登録する
    * ss: 変数いくつか並んでる、関数の引数
    * ss: GameplayTagContainer Queryしてる 選択しようとしてる
    * メリット、デメリット、それなりにある。
    * 残り24記事。主に自分が公私プロジェクトでGameplayTagを使うために、まとめておきたいことをひたすら書いていく。
    * 前提
        * 自分が公私プロジェクトでGameplayTagを使うため、という観点で情報をまとめる。
        * エディタ英語。ゴメンね！
        * プロジェクトのどの職種の人も使うもの。可能な範囲で平易な言葉を使う。
        * Blueprintメイン、C++については必要なところで触れる。
1. タグと言えば: ActorTag, ComponentTagとの違い
    * 紛らわしいやつは、先に排除しておきたい。
    * Actor, Componentのプロパティに、必ずいる
    * 文字列は自由に設定できる、定義がいらない。スペルミスする可能性あり。
    * FName型？
    * ただのプロパティ
1. じゃあ、enumとはどう違うの？どう使い分けよう？
    * タグ値は階層を表現することができる。
    * すべてのタグ値がGameplayTag型の値として扱われる。
    * C++、Blueprintで、共通してGameplayTag型(C++ではFGameplayTag型と呼ばれる)の値をやりとりできる。バインド不要。
    * タグ値の1セットを1つのDataTableに定義することができ、1プロジェクトで複数のDataTableを利用することが可能。
    * 入力ミスが起こる前提で使用する。
    * enumは異なるenum型をコンパイルエラーにできるが、GameplayTagはすべてのタグがGameplay型になるため、コンパイルエラーにできない。
    * ×タグ値同士を「演算」したい
    * ×C++以外で使用できないようにする。
1. 使用するタグを登録する
    * プロジェクトで使うタグを定義する
    * DataTable複数登録する
    * CSVやJSONからインポートもできるよ
1. タグ登録、うっかりこうするとどうなるの？
    * GameplayTag 中間階層タグ未定義 右 DevCommentが、先頭の子タグになる。
    * タグ、データテーブル間で重複したらどうなる？
1. タグをCSVで管理する？
    * インポート、Reimport、エクセル問題、文字コード問題
1. タグをJSONで管理する？
    * インポート、Reimport
    * ツールから吐き出す系

[GameplayTagを使ってみる]
1. GameplayTagとGameplayTagを比較する
1. GameplayTagContainerに含まれるGameplayTagを調べる
1. GameplayTagContainerとGameplayTagContainerを比較する
1. GameplayTagか、GameplayTagContainerか、GameplayTagの配列か
    * GameplayTagContainerには、「このカテゴリのタグが含まれる」ことは分かっても、「そのタグの具体的な値」は知ることができない？
    * 条件にマッチするタグがいくつあるか、把握できない？→まあそういうのを作ればいいんだけど、エンジンにないものを仕組みとして使うのは、それなりにリスキー。きっちりモジュールを作る覚悟で。
//0. MatchesTag 階層 含有 階層化における留意点
1. ObjectやActorにGameplayTag情報を保持させる
    * 1変数として
    * GameplayTagContainerとして
    * 配列の値として
    * ハッシュのキーとして
1. イベントや関数でGameplayTag値を流す
1. C++との受け渡し

[GameplayTagを運用してみる]
1. GameplayTag値と文字列を相互に変換する
    * GameplayTagを文字列から: C++ static FGameplayTag::RequestGameplayTag() をラップする。
1. FGameplayTagの中身はどうなってるの？
    * 変数上のサイズ FGameplayTag シリアライズされたらどうなるの
    * ネットワーク通信時のサイズ、扱い
1. AssetUserTagでアセットにGameplayTag情報を付加してみる
    * GameplayTagAssetInterface
1. GameplayTag使用箇所の検索性
1. GameplayTag 使用していたタグを変更or削除してしまったらどうなる？
1. リファクタによるタグ名変更を安全に行うには
    * 定義の一斉置換、使用箇所の一斉置換
    * DevCommentに[Obsolete] とあるタグをリスト化。アセット中に使われるタグを全探索し、Warningを出す。
1. 不正なタグ名、定義にないタグ名使用箇所を検出するには

[GameplayTagで遊んでみる]
1. GameplayTagで参照カウンタを作ってみる
    * ゲームや演出でのイベント排他処理
1. GameplayTagで参照カウンタを作ってみる C++版
1. GameplayTagでゲーム内要素全てを仕様定義してみる。


<!--
1. GameplayTagをプロジェクト設定ファイルで直接使ってみる
1. IGameplayTagAssetInterfaceとEQSのGameplayTagsテスト
-->