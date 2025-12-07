# [Advent Calendar 2025 オープンソース半導体](https://qiita.com/advent-calendar/2025/osssilicon)の3日目の記事

## [Wafer.Sapce GF180 Run 1 への投稿完了！！！](https://ishi-kai.org/waferspace/shuttle/gf180/2025/12/01/shuttle_ISHI-KAI_Multiple_Projects_WaferSapce-GF180-1_submitted.html)の続報
「[Wafer.Sapce GF180 Run 1 への投稿完了！！！](https://ishi-kai.org/waferspace/shuttle/gf180/2025/12/01/shuttle_ISHI-KAI_Multiple_Projects_WaferSapce-GF180-1_submitted.html)」で報告したWafer.Sapce GF180 Run 1ですが、投稿後にPDKがアップデートしたため対応を行いました。  
DRCにCUPとアンテナルールが追加され、もろに引っかかったので、3000を超えるエラーが出ました。これを一つずつ、手直ししたので3日ほど要しましたが、無事に全部Fixできました。  
やはり、第一回目ということもあり、ドタバタしていますね！これはこれでこのようなサービスの立ち上げを生で見られて良い経験となっております。  
[2025年12月イベント「東海理化シャトルのオープンPDK解説会」](https://github.com/noritsuna/AdventCalendar2025/blob/main/OSSSilicon_Day_08.md)で開設予定の東海理化シャトルのオープンPDKも来年は本格立ち上げとのことなので、このような光景が見られるかもしれません。  
***このあたりをサポートしてくれる人を募集中とのことです！***  


### DRC内容
少なくともアンテナルールのDRCは当初はWafer.Space側としては「ファブに対して無視して作ってくれ。」と交渉していたらしいですが「だめ！」って言われて対応することになったようです。  
実際に、アンテナルールに関しては「理論的には起きるけど、可能性は低い」ってものなので「壊れても文句言わないからエラーは無視して作ってくれ」というと対応してくれることが多いDRCの一つです。  

- CUP
    - Padに対して接続されているメタル線が細すぎる場合に出力される
        - 本質的には大きなメタルに対して、接続されているメタルの幅の比が大きくなりすぎる場合に出るエラー。エッチング時などに大きいものに対してい小さすぎる場合影響がでかくなるためである（通常よりも侵食が進む）。
    - 対策
        - 図のように鏡餅のように段々と細くなるようにメタルを作る
        - ![配線例](/images/WS_CUP_01.png)
- アンテナルール
    - Gateに接続されているメタル線が長すぎる場合に出力される
        - 本質的には大きな面積を持つメタルが接続される場合に出るエラー。面積が大きいメタル＝保持される電荷量も大きいということであり、大電流によりGateの酸化膜の絶縁破壊が起きる可能性があるためである。
    - 対策
        - メタル線を分割する＝M1 -> M2 -> M3 というような感じでM1など一層だけ使わずに複数層を使って線を引く
            - ![配線例](/images/WS_ANT_01.png)
        - メタル線にサージ対策（TVS）としてのダイオードを付加する
            - 今回はこれは行わなかった。理由は「ダイオードが無視される」という現象が出ていたため。この原因は「PDK 1.4.1」で修正されているが「PDK 1.3.1」で修正を行なっていたため、気が付かずにこの対策を諦めたためである。
            - ![配線例](/images/WS_ANT_02.png)


### PDKアップデート履歴
- 2025/12/04
    - PDK 1.3.1
        - Implement CUP.2 and CUP.3 rules.
        - Modify the pad library to conform to CUP.2 and CUP.3.
        - Flatten the guard ring and merge the marker polygons.
        - Correct ANTENNAGATEPLUSDIFF in the techlef for thick oxide devices. (thanks @egor!)
    - Project template 1.2.2
        - Update the PDK to 1.3.1.
        - Enable KLayout antenna checks by default.
        - Add a script to generate standalone padrings for analog designs.
- 2025/12/05
    - PDK 1.4.1
        - Fix the connectivity setup in KLayout DRC.
        - Check for both P/N-type diodes in the KLayout antenna script. (thanks @tnt!)
    - Project template 1.2.3
- 2025/12/07
    - PDK 1.4.4
        - Skip certain checks in the KLayout antenna script if corresponding layers are empty. Correctly check the top metal layer. (thanks @Egor Lukyanchenko!)
        - Don't consider dummy metal in the KLayout antenna script (already handled by the DRC rules).
        - Actually check for both P/N-type diodes in the KLayout antenna script. (thanks again @tnt!)
    - Project template 1.2.5
