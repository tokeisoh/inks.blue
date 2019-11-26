# Draft

1. GameplayTagとは？
    * ゲーム内の要素、状態などを文字列のタグ(ラベル)として表現するためのデータ型。
    * このAdventCalendarでは、ある程度使い方を絞って情報をまとめる。
    * どんな場面で使われるか、何ができるか、グラフィカルに説明する。

    * enumと似た特徴を持つ。enumとの違いは別記事にてまとめる。
        * エディタ上では文字で表示されるため、状態や意図が分かりやすい。
        * エディタ上で選択するだけなので、スペルミスなどが起きない。
        * 内部ではFName(ハッシュ)で扱われるためコピーや比較などが高速。
    * enumにない主な特徴
        * タグ値は階層を表現することができる。
        * すべてのタグ値がGameplayTag型の値として扱われる。
        * C++、Blueprintで、共通してGameplayTag型(C++ではFGameplayTag型と呼ばれる)の値をやりとりできる。バインド不要。
        * タグ値の1セットを1つのDataTableに定義することができ、1プロジェクトで複数のDataTableを利用することが可能。
0. GameplayTagを、DataTableで追加する
    * DataTableを使ったやり方に絞る
    * Blueprint上で使うための作業
    * DataTable複数登録する
0. ActorTag, ComponentTagとの違い
    * 文字列は自由に設定できる、定義がいらない。スペルミスする可能性あり。
    * FName型
    * ただのプロパティ
0. enum、bitflagとの違い
    * enumは異なるenum型をコンパイルエラーにできるが、GameplayTagはすべてのタグがGameplay型になるため、コンパイルエラーにできない。
    * 入力ミスが起こる前提で使用する。
0. GameplayTagとGameplayTagを比較する
0. GameplayTagContainerに含まれるGameplayTagを調べる
0. GameplayTagContainerとGameplayTagContainerを比較する
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
0. IGameplayTagAssetInterfaceとEQSのGameplayTagsテスト
0. GameplayTag CSV/JSON エクスポート
0. GameplayTag CSV インポート、Reimport
0. GameplayTag DataTable 複数登録 こんなとき、どうなる？
0. タグ値重複定義していたらどうなる？
0. タグ値、データテーブル間で重複したらどうなる？
0. GameplayTag 中間階層タグ未定義 右 DevCommentが、先頭の子タグになる。
0. GameplayTag 使用していたタグを変更or削除してしまったらどうなる？
0. 検索性
0. リファクタによるタグ名変更を安全に行うには
    * 定義の一斉置換、使用箇所の一斉置換
    * DevCommentに[Obsolete] とあるタグをリスト化。アセット中に使われるタグを全探索し、Warningを出す。
0. 不正なタグ名、定義にないタグ名使用箇所を検出するには
0. GameplayTagでゲーム内要素全てを仕様定義してみる。

<!-- 0. GameplayTagをプロジェクト設定ファイルで直接使ってみる
0. できないこと
        * ×タグ値同士を「演算」したい
        * C++上で定義する。C++以外で使用できないようにする。
-->