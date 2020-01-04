# 18日目: GameplayTag のネットワークでのやりとり

> [UE4 GameplayTag Advent Calendar 2019 18日目](https://qiita.com/advent-calendar/2019/ue4-gameplaytag)  
>#UE4Study #UE4.23 #UnrealEngine #GameplayTag

# そもそも、GameplayTag 型変数はレプリケートできるのか？

* 変数の型によって、レプリケート(ネットワーク通信によるサーバ-クライアント間複製)できない型がある。
* レプリケートできる。すなわち、`FGameplayTag::NetSerialize()` が実装されている。
* GameplayTagContainer もレプリケートできる。
* つまり、サーバークライアント間の情報伝達媒体として、GameplayTag を使うことができる。

# レプリケート時のサイズは？

* 16日目に見たように、GameplayTag の実体は FName である。
* FName の実体は、uint32 が2つだった。FName のレプリケートはどうなっている？
    * エンジンコード読み込めてないこともあり、さらっと読める感じではなかった。無念。
    * ~~FName Advent Calendar やるべきか~~
    * [NetGUIDを作って、最初だけNetGUIDと文字列そのものを送ってる？](https://twitter.com/mkaech/status/1149712274589753344)
* GameplayTag


## 次回予告

* 19日目: GameplayTag 使用箇所の検索性

---

> [UE4 GameplayTag Advent Calendar 2019(Qiita)](https://qiita.com/advent-calendar/2019/ue4-gameplaytag)  
> [inks.blue > UE4 GameplayTag Advent Calendar 2019](./Index.md)  
> [inks.blue](../../)

(C) 2019 inks.blue
