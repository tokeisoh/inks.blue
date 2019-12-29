# 17日目: FGameplayTagContainer の中身はどうなってるの？

> [UE4 GameplayTag Advent Calendar 2019 17日目](https://qiita.com/advent-calendar/2019/ue4-gameplaytag)  
>#UE4Study #UE4.23 #UnrealEngine #GameplayTag

# GameplayTagContainer はどう定義されているのか？

* GameplayTagContainer は、C++ 上で定義されている。
    * GameplayTagContainer (Blueprint) ← FGameplayTagContainer (C++)
* ["F" ということは、その他扱い？](https://docs.unrealengine.com/ja/Programming/Introduction/index.html#クラス名のプレフィックス)
* C++ 側での実体はどうなっているのか？メンバ構成はどうなっているのか？
* FGameplayTagContainer も下記のソースコードに定義されている:  
`Engine/Source/Runtime/GameplayTags/Classes/GameplayTagContainer.h` 

# FGameplayTagContainer の実体

* 複数の FGameplayTag を保持するコレクション、struct (C++) / USTRUCT (Blueprint) な型。copyable.
* メンバ変数は以下の通り:
    * `TArray<FGameplayTag> GameplayTags`
    * `TArray<FGameplayTag> ParentTags`
* というわけで、あまり Array 的には使えない GameplayTagContainer だが、中身は TArray なのであった。
* ParentTags は、各タグの親＆先祖タグをキャッシュしている TArray.

# FGameplayTagContainer の C++ only な機能 (目についたもの)

* `static const FGameplayTagContainer EmptyContainer`  
空のコンテナを表す定数。
* `FGameplayTagContainer GetGameplayTagParents() const`  
今の FGameplayTagContainer に含まれるタグ「と」、  
その親タグすべてを含む FGameplayTagContainer を取得する。
* `bool AddLeafTag(const FGameplayTag& TagToAdd)`    
`TagToAdd` を追加し、その親タグや先祖タグがあれば取り除く。  
`TagToAdd` の子孫タグがすでに存在するなら、追加しない。
* `FGameplayTag GetByIndex(int32 Index) const`  
 配列の Index を指定してタグを取得する。

# 備考

* いくつか動作を検証しておきたいものがあったけど、未検証。
* のちのち試したら追記します。

# UGameplayTagManager まで追いたいけど今回はパス

* 機会があれば、記事追加します。

## 次回予告

* 18日目: GameplayTag のネットワークでのやりとり

---

> [UE4 GameplayTag Advent Calendar 2019(Qiita)](https://qiita.com/advent-calendar/2019/ue4-gameplaytag)  
> [inks.blue > UE4 GameplayTag Advent Calendar 2019](./Index.md)  
> [inks.blue](../../)

(C) 2019 inks.blue
