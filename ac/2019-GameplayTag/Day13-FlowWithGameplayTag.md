# 13日目: GameplayTag 情報を使って、処理を行う

> [UE4 GameplayTag Advent Calendar 2019 13日目](https://qiita.com/advent-calendar/2019/ue4-gameplaytag)  
>#UE4Study #UE4.23 #UnrealEngine #GameplayTag

# Switch (GameplayTag)

* Switch on Gameplay Tag ノードと、Switch on Gameplay Tag Container ノードがある。
* いずれも、"Exact Match" な条件のところにのみ、処理が流れる。
* Switch on Gameplay Tag Container では、Container に含まれるタグすべてが一致する条件のところに処理が流れる。  
つまり、"Has All (Exact Match == true)" で分岐する。
![Day13_SwitchOnGameplayTag](./Images/Day13_SwitchOnGameplayTag.png)

# 特定のタグ条件を満たす Actor を見つける

* [2日目](./Day02-VsActorOrComponentTags.md) に紹介したような、Get All～ 系のノードは、GameplayTagQuery を使うものだけが用意されている:  
![Day13_GetAllActorsOfClassMatchingTagQuery](./Images/Day13_GetAllActorsOfClassMatchingTagQuery.png)
* この Get All Actors Of Class Matching Tag Query を使って調べられるのは、GameplayTagAssetInterface を実装している Actor のみ。

# GameplayTagAssetInterface

* エンジンにデフォルトで用意されているインタフェース。以下の関数がある。  
![Day13_GameplayTagAssetInterface](./Images/Day13_GameplayTagAssetInterface.png)
* 特殊なことをしないのであれば、Actor に GameplayTagContainer を持たせて、


# Actor が保持する GameplayTag 情報を取得する

* 



## 次回予告

* [14日目: GameplayTag と文字列を相互に変換する](./Day14-ConvertFromOrToString.md)

---

> [UE4 GameplayTag Advent Calendar 2019(Qiita)](https://qiita.com/advent-calendar/2019/ue4-gameplaytag)  
> [inks.blue > UE4 GameplayTag Advent Calendar 2019](./Index.md)  
> [inks.blue](../../)

(C) 2019 inks.blue
