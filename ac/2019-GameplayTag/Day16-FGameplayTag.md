# 16日目: FGameplayTag の中身はどうなってるの？

> [UE4 GameplayTag Advent Calendar 2019 16日目](https://qiita.com/advent-calendar/2019/ue4-gameplaytag)  
>#UE4Study #UE4.23 #UnrealEngine #GameplayTag

# GameplayTag はどう定義されているのか？

* GameplayTag は、C++ 上で定義されている。
    * GameplayTag (Blueprint) ← FGameplayTag (C++)
* ["F" ということは、その他扱い？](https://docs.unrealengine.com/ja/Programming/Introduction/index.html#クラス名のプレフィックス)
* C++ 側での実体はどうなっているのか？メンバ構成はどうなっているのか？
* FGameplayTag は下記のソースコードに定義されている:  
`Engine/Source/Runtime/GameplayTags/Classes/GameplayTagContainer.h` 

# FGameplayTag の実体

* 1つの GameplayTag を表す、struct (C++) / USTRUCT (Blueprint) な型。copyable.
* 概念としての1つの GameplayTag は、 UGameplayTagsManager に登録されている。
* メンバ変数は以下の通り:
    * `FName TagName`
* つまり、実体は FName 1つだけ。
* FName のメンバ変数はというと:
    * `FNameEntryId ComparisonIndex` (中身は uint32 only)
    * `uint32 Number`
* というわけで、uint32 x2 が FGameplayTag 1つのサイズ。

# FGameplayTag の C++ only な機能 (目についたもの)

* static定数: 空タグを表す定数。  
`static const FGameplayTag EmptyTag`
* static関数: Name 型から GameplayTag へ変換する関数。[14日目を参照。](./Day14-ConvertFromOrToString.md)  
`static FGameplayTag RequestGameplayTag(FName TagName, 略)`
* static関数: GameplayTag として Valid な文字列か。  
`static bool IsValidGameplayTagString(const FString& TagString, 略)`
* instance関数: もう1つの GameplayTag が何階層まで一致しているか。  
`int32 MatchesTagDepth(const FGameplayTag& TagToCheck) const`
* instance関数: 直接の親階層を表す GameplayTag を取得する。  
`FGameplayTag RequestDirectParent() const`
* この GameplayTag と、その親＆先祖タグを含むコンテナ「への参照」を取得する。
`const FGameplayTagContainer& GetSingleTagContainer() const`
* この GameplayTag の、親＆先祖タグを含むコンテナ「のコピー」を取得する。
`FGameplayTagContainer GetGameplayTagParents() const`

# 備考

* いくつか動作を検証しておきたいものがあったけど、未検証。
* のちのち試したら追記します。

## 次回予告

* [17日目: FGameplayTagContainer の中身はどうなってるの？](./Day17-FGameplayTagContainer.md)

---

> [UE4 GameplayTag Advent Calendar 2019(Qiita)](https://qiita.com/advent-calendar/2019/ue4-gameplaytag)  
> [inks.blue > UE4 GameplayTag Advent Calendar 2019](./Index.md)  
> [inks.blue](../../)

(C) 2019 inks.blue
