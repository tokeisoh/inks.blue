# タグを CSV で管理する

> [UE4 GameplayTag Advent Calendar 2019 5日目](https://qiita.com/advent-calendar/2019/ue4-gameplaytag)  
>#UE4Study #UE4.23 #UnrealEngine #GameplayTag

## タグの DataTable を CSV で管理する

* DataTable は、CSV からインポートすることができる。
* 当然、タグの DataTable も、CSV からインポートできる。
* みんなだいすき Excel で都度編集し、再インポートできる。
* しかし、そこにはちょっとした落とし穴がいくつか。

## DataTable から CSV にエクスポートする

* ざっと DataTable で作ってたけど、そろそろ Excel で管理したくなってきたなー。
* そうだ、タグが増えて訳分からなくなる前に、コメントつけておこう。 **日本語で。**  
![AddDevCommentIntoDataTable](./Images/Day05_AddDevCommentIntoDataTable.png)
* よし、じゃあ CSV にエクスポートしてみよう。
* コンテンツブラウザで DataTable を右クリック、Export as CSV で、CSV ファイルに保存。  
![ExportAsCSV](./Images/Day05_ExportAsCSV.png)

## Excel で CSV 開きたいだけなのに

* では早速、Excel で開いてみよう。どん。  
![ExportedCSV_AsIs](./Images/Day05_ExportedCSV_AsIs.png)
* えっ…ただのカンマ区切り文字列？CSV になってない？どういうこと？
* VSCodeで開いてみるか…。  
![ExportedCSV_VSCode_UTF16LE](./Images/Day05_ExportedCSV_VSCode_UTF16LE.png)
* UTF-16LE…これがあかんのかな？とりあえず、Shift_JIS あたりにしてみよう。  
![ExportedCSV_ShiftJIS](./Images/Day05_ExportedCSV_ShiftJIS.png)
* おお、ちゃんと区切られた！よし、じゃあUE4でインポートしてみよう！

## UE4 で CSV インポートしたいだけなのに

* DataTable の Asset メニューから、Reimport なんちゃらをクリック。  
![Reimport](./Images/Day05_Reimport.gif)  
* どん。  
![FailedToReimport](./Images/Day05_FailedToReimport.png)
* Oh...
* インポートする CSV ファイルを Excel で開きっぱなしだとこうなる。
    * __→ UE4.24 から、Excel で開きっぱなしの CSV もエラーなくインポートできるようになりました！__
* というわけで、Excel をいったん閉じて、気を取り直してもう一回！  
![ImportedCSV_ShiftJIS](./Images/Day05_ImportedCSV_ShiftJIS.png)
* Oh...

## UTF-8 BOM にすれば OK.

* UTF-8 BOM なしにすると、インポートは OK だが、Excel がこうなる。かなしい。  
![ExportedCSV_UTF8](./Images/Day05_ExportedCSV_UTF8.png)
* UTF-8 BOM ありにしましょう。  
![ExportedCSV_UTF8BOM](./Images/Day05_ExportedCSV_UTF8BOM.png)  
![ImportedCSV_UTF8BOM](./Images/Day05_ImportedCSV_UTF8BOM.png)
* めでたしめでたし。

## 次回予告

* [06日目: タグを JSON で管理する](./Day06-ManageDataTableWithJSON.md)

---

> [UE4 GameplayTag Advent Calendar 2019(Qiita)](https://qiita.com/advent-calendar/2019/ue4-gameplaytag)  
> [inks.blue > UE4 GameplayTag Advent Calendar 2019](./Index.md)  
> [inks.blue](../../)

(C) 2019 inks.blue
