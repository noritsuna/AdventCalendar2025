# [Advent Calendar 2025 オープンソース半導体](https://qiita.com/advent-calendar/2025/osssilicon)の7日目の記事

## [RISC-V Day Tokyo 2025 Autumn](https://riscv.or.jp/risc-v-day-tokyo-2025-autumn-public/)で[TinyTapeoutハンズオン](https://www.dreamnews.jp/press/0000335574/)をやってみた報告

約20名の満員御礼って感じでした。  
![RISC-V Dayハンズオン風景](/images/risc-v_day01.jpg)

ロジック系ははっきり言って、コマンド打って、ツールのセットアップをして、ビルドするだけなので、説明していても「これはイマイチ面白くないかも」と思いました。  
やはり、LibreLaneのシーケンス手順でも細かく説明するような内容じゃないと面白みは出なそうというのが今回の知見ですね。  
[ライトニングトーク資料 PPTX版](https://ishi-kai.org/assets/presentation/event/202512/ISHI-KAI_RISC-VDay_ossEDA.pptx)にLibreLaneで使用されているソフト表があるので、これの解説でもすればよかったと反省しております。  

とくに、どうしても、Dockerイメージのダウンロードに時間がかかるのが最悪ですね。ほぼ、30分近く待ちぼうけになるので、この辺りの時間をどうつなぐか？などもっと考えないとハンズオンとしてはつらいという印象です。  
このあたり、最近は、nix-shellへの移行が流行っているので次回はnix-shellベースに変更してみるのも手かもしれません。ただ、こちらはこちらでnix-shellのコンパイルに時間がかかるのので持ち込まれるPCのパワーにかなり左右されそうですが。。。  


ということで、次回があれば、もう少し、つなぎをうまくしたいなぁと思っております。  


* [TinyTapeoutハンズオン資料](https://ishi-kai.org/assets/presentation/2025/ISHIKAI_TinyTapeout_sky130_2025.pdf)
* [ライトニングトーク資料 PPTX版](https://ishi-kai.org/assets/presentation/event/202512/ISHI-KAI_RISC-VDay_ossEDA.pptx)
* [ライトニングトーク資料 PDF版](https://ishi-kai.org/assets/presentation/event/202512/ISHI-KAI_RISC-VDay_ossEDA.pdf)
