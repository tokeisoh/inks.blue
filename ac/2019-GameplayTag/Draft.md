# Draft

0. GameplayTagとは？
    * ゲーム内の要素、状態などを文字列タグとして表現するためのデータ型。
    * エディタ上では文字で表示されるため、意図が分かりやすい。
    * エディタUI上で特定のタグ値を扱う場合、文字列入力ではなく選択するだけなので、スペルミスなどが起きない。
    * 文字列と異なり、内部では数値で扱われるため、コピーや比較などが高速。
    * タグ値のセットは、DataTableで定義することができ、1プロジェクトで複数のDataTableを利用することが可能。
    * C++、Blueprintで、共通してGameplayTag型(C++ではFGameplayTag型と呼ばれる)の値をやりとりできる。
    * enumと異なり、すべてのタグ値がGameplayTag型として扱われる。
    * タグ値は階層化することができる。
0. できないこと
        * ×タグ値同士を「演算」したい
0. まずは使ってみる
    * DataTable
0. GameplayTag DataTable 複数登録 タグ値重複していたら？
0. ActorTag, ComponentTagとの違い
0. enum、bitflagとの違い
    * enumは異なるenum型をコンパイルエラーにできるが、GameplayTagはすべてのタグがGameplay型になるため、コンパイルエラーにできない。
0. Match, Has, Query 比較方法
0. MatchesTag 階層 含有 階層化における留意点
0. AActorにGameplayTagを保持させる
    * 1変数として
    * GameplayTagContainerとして
    * 配列のキーとして
    * 配列の値として
0. イベントや関数でGameplayTag値を流す
0. C++との受け渡し
0. GameplayTagContainer と `TArray<GameplayTag>`
0. GameplayTagか、GameplayTagContainerか
    * GameplayTagContainerには、「このカテゴリのタグが含まれる」ことは分かっても、「そのタグの具体的な値」は知ることができない？
    * 条件にマッチするタグがいくつあるか、把握できない？
0. GameplayTag値を文字列に変換する
0. GameplayTag値を文字列から取得する
0. GameplayTagで参照カウンタを作ってみる ゲームや演出でのイベント排他処理
0. GameplayTagで参照カウンタを作ってみる C++版
0. 変数上のサイズ FGameplayTag
    * ネットワーク通信時のサイズ、扱い
0. GameplayTagAssetInterface, AssetUserTagでアセットに情報付加し、使用するには
0. GameplayTag CSV/JSON エクスポート
0. GameplayTag CSV インポート、Reimport
0. 検索性
0. リファクタによるタグ名変更を安全に行うには
0. 不正なタグ名、定義にないタグ名使用箇所を検出するには
0. GameplayTagでゲーム内要素全てを仕様定義してみる。

<!-- 0. GameplayTagをプロジェクト設定ファイルで直接使ってみる -->