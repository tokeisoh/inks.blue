# 18日目: GameplayTag のネットワークでのやりとり

> [UE4 GameplayTag Advent Calendar 2019 18日目](https://qiita.com/advent-calendar/2019/ue4-gameplaytag)  
>#UE4Study #UE4.23 #UnrealEngine #GameplayTag

# そもそも、GameplayTag 型変数はレプリケートできるのか？

* UE4では、変数の型によって、レプリケート(ネットワーク通信によるサーバ-クライアント間複製)できる型とできない型がある。
* GameplayTag はレプリケートできる。すなわち、`FGameplayTag::NetSerialize()` が実装されている。
* GameplayTagContainer もレプリケートできる。
* つまり、サーバークライアント間の情報伝達媒体として、GameplayTag を使うことができる。

# レプリケート時のサイズは？

* 16日目に見たように、GameplayTag の実体は FName である。
* FName の実体は、uint32 が2つだった。FName のレプリケートはどうなっている？
    * [NetGUIDを作って、最初だけNetGUIDと文字列そのものを送ってる？](https://twitter.com/mkaech/status/1149712274589753344)
    * ってあるけど、特定の固有名以外は、毎回文字列送ってるような… `UPackageMap::StaticSerializeName()`
    * キャプチャして調べたい
* で、肝心の GameplayTag はどうなっているか？ → 2パターンのいずれかが送られている。
    * タグをFNameで送信。
    * タグを数値化 (uint32 x1) して送信。ただし、頻繁に使われるタグを、より低コストに送信するための仕組みがある。
    * `SerializeTagNetIndexPacked()` コメント部分を参照。

## 次回予告

* 19日目: GameplayTag 使用箇所の検索性

---

> [UE4 GameplayTag Advent Calendar 2019(Qiita)](https://qiita.com/advent-calendar/2019/ue4-gameplaytag)  
> [inks.blue > UE4 GameplayTag Advent Calendar 2019](./Index.md)  
> [inks.blue](../../)

(C) 2019 inks.blue
