# 19日目: ネットワーク通信での GameplayTagContainer

> [UE4 GameplayTag Advent Calendar 2019 19日目](https://qiita.com/advent-calendar/2019/ue4-gameplaytag)  
>#UE4Study #UE4.23 #UnrealEngine #GameplayTag

# そもそも、GameplayTagContainer 型変数はレプリケートできるのか？

* UE4では、変数の型によって、レプリケート(ネットワーク通信によるサーバ-クライアント間複製)できる型とできない型がある。
* GameplayTagContainer もレプリケートできる。すなわち、`FGameplayTagContainer::NetSerialize()` が実装されている。
* つまり、サーバークライアント間の情報伝達媒体として、GameplayTagContainer を使うことができる。

# レプリケート時のサイズは？

* [18日目](./Day18-ReplicateGameplayTag.md) 同様に、Container に含まれるタグが送信される。
* 高速に送信する設定も同様。
* [プロジェクト設定] - [GameplayTags] - [NumBitsForContainerSize] を指定することで、「『コンテナに含まれるタグ数』を表現するビット数」を設定できる。


## 次回予告

* 20日目: GameplayTag 使用箇所の検索性

---

> [UE4 GameplayTag Advent Calendar 2019(Qiita)](https://qiita.com/advent-calendar/2019/ue4-gameplaytag)  
> [inks.blue > UE4 GameplayTag Advent Calendar 2019](./Index.md)  
> [inks.blue](../../)

(C) 2019 inks.blue
