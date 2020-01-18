# 18日目: ネットワーク通信での GameplayTag

> [UE4 GameplayTag Advent Calendar 2019 18日目](https://qiita.com/advent-calendar/2019/ue4-gameplaytag)  
>#UE4Study #UE4.23 #UnrealEngine #GameplayTag

# そもそも、GameplayTag 型変数はレプリケートできるのか？

* UE4では、変数の型によって、レプリケート(ネットワーク通信によるサーバ-クライアント間複製)できる型とできない型がある。
* GameplayTag はレプリケートできる。すなわち、`FGameplayTag::NetSerialize()` が実装されている。
* つまり、サーバークライアント間の情報伝達媒体として、GameplayTag を使うことができる。

# レプリケート時のサイズは？

* [16日目](./Day16-FGameplayTag.md)に見たように、GameplayTag の実体は FName である。
* FName の実体は、uint32 が2つだった。FName のレプリケートはどうなっている？
    * [NetGUIDを作って、最初だけNetGUIDと文字列そのものを送ってる？](https://twitter.com/mkaech/status/1149712274589753344)
    * ってあるけど、エンジンで予約してる固有名以外は、毎回文字列送ってるような…  
    `CoreNet.cpp: UPackageMap::StaticSerializeName()` あたり。
* で、肝心の GameplayTag はどうなっているか？
* なにも設定しなければ、GameplayTag 値は、FName として文字列で送信されるぽい。
    * CoreNet.cpp の 329行目、同じタグを複数回送っても、毎回通る。ので、毎度文字列を送ってるっぽい。
* [プロジェクト設定] - [GameplayTags] - [Fast Replication] にチェックを入れると、文字列の代わりに、数値 (uint32 x1) が送信される。
    * 要は辞書のキーだけを送っていることになるので、送信元と送信先の GameplayTag 辞書が同一であることが前提と思われる。
    * さらに、頻繁に送信するタグを、より低コストに送信するための仕組みがあるらしい。

# より高速にレプリケートするには？

* `GameplayTagContainer.cpp: SerializeTagNetIndexPacked()` コメント部分より。
    * 「頻繁に送信するタグ」を [プロジェクト設定] - [GameplayTags] - [Commonly Replicated Tags] にセットする。
    * 「頻繁に送信するタグ」を表現するためのビット数を [Net Index First Bit Segment] に指定する。
* これらは、コンソールコマンド `GameplayTags.PrintReport` or `GameplayTags.PrintReportOnShutdown 1` でプロファイルすると、それぞれオススメの値を出力してくれる。
* 実際通信してるところキャプチャしてみたいけど、時間がないのでまたの機会に…。

## 次回予告

* 19日目: ネットワーク通信での GameplayTagContainer

---

> [UE4 GameplayTag Advent Calendar 2019(Qiita)](https://qiita.com/advent-calendar/2019/ue4-gameplaytag)  
> [inks.blue > UE4 GameplayTag Advent Calendar 2019](./Index.md)  
> [inks.blue](../../)

(C) 2019 inks.blue
