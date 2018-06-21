> 本記事はReact Native at Airbnbのpart3となります。数えきれない程の技術的なメリットとデメリットに加え、私達はエンジニアリング組織にとってReact Nativeが何を意味しているかという事を学びました。React Nativeを適用するという事は新しいライブラリや設計パターンを既存のプラットフォームに導入する事よりもはるかに複雑です。React Nativeの導入は沢山の組織的なチャレンジを私達にもたらしました。殆どのケースで最終的に解決されたり避ける事のできる技術的なチャレンジとは異なり組織的なチャレンジはより認識、改善していく事が難しい問題です。幸いな事に私達のモバイル開発文化は健全ですが、React Nativeの導入に辺り意識すべき沢山のポイントが存在します。

### React Native に対する様々な反応

私達の経験では、React Nativeに対するエンジニアの反応は実に様々でした。iOS/Android/Webを統一する銀の弾丸だと褒め称える者もいれば、React Nativeの利用をチーム内で全く認めないような者までいました。同じ状況はReact Nativeの利用を開始してからも起こったのです。幾つかのチームは素晴らしい体験を得た一方で導入を後悔しNativeに戻っていったチームもいました。

## 根本原因の帰属

React Nativeで開発をしていて、避けることのできないバグや改善、パフォーマンスの問題に遭遇しました。しかしながら、沢山の流動的なポイントが存在しました。

- React Native自体の開発は活発です
- 私達は機能開発とインフラストラクチャの整備を同時に進めていました
- 殆どのエンジニアにとってReact Nativeを学ぶ事は比較的新しい事でした
- 私達のdev/production環境でのデバッグに関するドキュメントやガイダンスは一貫性に欠き、紛らわしいものでした

結果として、問題の根本的な原因を特定する事が困難な事態にしばしば遭遇しました。どのチームが問題の原因なのかはたまたReact Native固有の問題なのかが明確でないケースがしばしばありました。

### React NativeはNative

よくある思い違いはReact NativeがあればNativeコードを一切書かなくても良いという思い込みです。しかしながら、現時点ではそれは幻想といってもいいです。React NativeのNativeの部分は依然としてしばしば私達の前に姿を現します。例えば、Textは各プラットフォームによって若干異なる表示の仕方になります。キーボードも異なる挙動をし、AndroidではActivityは画面回転時に再構築されます。React Nativeを用いて高品質な体験を提供するには両OSの世界への注意深い配慮が必要です。3プラットフォームのノウハウをバランスよく取り入れないといけないという問題は一貫性のある高品質な体験の提供を難しくします。

### プラットフォームを横断したデバッグ

殆どのエンジニアはせいぜい1つか2つのプラットフォームにしか精通していません。Android、iOS、Reactの全部について詳しい人に出会えるのはごく稀です。React Native上での殆どの開発がReactやJavaScriptによって成されるとしても、Nativeのビルドやデバッグの知識を求められる事は存在します。その状況ではエンジニアは時として自身の専門外の状況でデバッグをしなければなりません。この状況はエンジニアが問題を解決する為にどこから手を付けていいか自信がない時にさらにひどくなります。

### 採用

私達はReact Nativeに対して投資をしてきましたが、私達のモバイルチームと野望はそれと並行して加速していきました。しかしながら、コミュニティの噂を通して多くの人はAirbnbとReact Nativeを関連付けて考え、一部の人は私達のアプリが100%React Nativeであると信じていました。それは真実とは程遠いですが、多くのiOS/Androidエンジニアは結果としてAirbnbに応募する事を躊躇う事になりました。もしあなたがその一部だとしたら、私達は積極採用中ですよ！

### ハイブリッドアプリは難しい

100% Nativeか、100% React Nativeかという世界は比較的単純です。しかしながら、一度コードを混ぜてしまうと沢山の新しい問題が噴出します。どうやってチームを分割しようか？どうやってチーム同士は協業するのか？どうやって状態をアプリ間で共有する？どうやってテストする？どうやってエンジニアは3つのプラットフォームを跨いでデバッグする？どうやって新機能をReactかNativeで開発するか決める？どうやって組織を跨いでエンジニアを採用/配属する？これらの看過できない問題はあなたがハイブリッド開発の道を行くときには必ず生じますよ。

### 3つの開発環境

強いReact Nativeエンジニアになる為には、React Native、Android、iOSの環境に関して精通してキャッチアップしなければなりません。Airbnbと同じサイズの組織であればそれぞれのプラットフォームの環境のセットアップ、学習コストやキャッチアップにはかなりの時間がかかります。数週間の休暇から戻ってくると何時間も全ての情報のキャッチアップに費やす事になります。

### NativeとReact Nativeのバランス

問題に対する最適な答えがNativeとReact Nativeの両方に跨っている、というケースは数多く存在します。例えば私達のNavigationライブラリはActivityとViewControllerを主に利用しておりコードはほとんどNativeです。殆どの場合で、コードがNativeで書かれるかReact Nativeで書かれるべきかというのは自明ではなく当然の事として、エンジニアは自分が慣れ親しんだプラットフォームでコードを書き、そのコードは理想的とは言えないケースがしばしば起こります。

### クロスプラットフォームのテスト

エンジニアはまず1つのプラットフォーム上で開発を進めがちです。勿論もう一方のプラットフォームでの動作を保証し、テストをしなければならずそれは殆どの場合React Nativeの力でなんとかなるのですが、然しながらそれらの検証が不十分なままQAやプロダクション環境で問題を起こしてしまった事もしばしばありました。

### チーム分割

NativeとReact Nativeで開発を進めているチームはしばしば技術とコミュニケーション両方の問題にぶつかります。NativeとReact Nativeのコードを分割してしまえば、コードの断片化が発生します。ロジック、モデル、状態の共通化はよりチャレンジングになりエンジニアは全体のflowを一貫して受け持つ事になり、彼らの得意分野の力を出せなくなります。私達はこれらの問題は最初は起こるがWebチームとの共同により徐々にましになっていくだろうと期待していました。が、実際には幾つかのチームがコードや知識のシェアをWeb-Mobile間で始めただけで殆どのチームは潜在的な利益に気づかないままでした。

### (開発者にとっての) イテレーションのスピード

私達のゴールの1つは開発のスピードを高速化する事でした。殆どの場合、React Nativeの機能は各プラットフォームに担当をアサインする代わりに一人のエンジニアによって書かれます。React Nativeエンジニアの観点から見れば、AndroidかiOSどちらかにかかる時間より50%以上の時間がかかれば、全体で数時間の短縮になったとしても開発者にとってはそれは実に長く感じられます。

### 公式リソースとドキュメント

iOS/Androidは10年の歴史と何百万の開発者を抱えており大量の学習教材、OSS、オンラインの情報が存在します。私達はCodePathや沢山の情報をNativeエンジニアの育成の為に利用してきました。React Nativeはクロスプラットフォーム開発の一角を占めるようになりましたが、それでもAndroidやiOSのコミュニティよりは小さいです。殆どのインフラストラクチャを自前で開発しないといけなかったという事実は私達がReac tNativeの教育や育成に投資をしすぎたという事を意味しています。

# その他の記事
- [Part 1](https://medium.com/airbnb-engineering/react-native-at-airbnb-f95aa460be1c)（[日本語訳](https://github.com/react-native-jp/react-native-at-airbnb-jp-translation/blob/master/1-alt-react-native-at-airbnb.md)）: React Native at Airbnb
- [Part 2](https://medium.com/airbnb-engineering/react-native-at-airbnb-the-technology-dafd0b43838)（[日本語訳](https://github.com/react-native-jp/react-native-at-airbnb-jp-translation/blob/master/2-react-native-at-airbnb-the-technology.md)）: The Technology
- [Part 3](https://medium.com/airbnb-engineering/building-a-cross-platform-mobile-team-3e1837b40a88)（[日本語訳](https://github.com/react-native-jp/react-native-at-airbnb-jp-translation/blob/master/3-building-a-cross-platform-mobile-team.md)）: Building a Cross-Platform Mobile Team(本記事)
- [Part 4](https://medium.com/airbnb-engineering/sunsetting-react-native-1868ba28e30a)（[日本語訳](https://github.com/react-native-jp/react-native-at-airbnb-jp-translation/blob/master/4-sunsetting-react-native.md)）: Making a Decision on React Native
- [Part 5](https://medium.com/airbnb-engineering/whats-next-for-mobile-at-airbnb-5e71618576ab)（[日本語訳](https://github.com/react-native-jp/react-native-at-airbnb-jp-translation/blob/master/5-what%E2%80%99s-next-for-mobile-at-airbnb.md)）: What’s Next for Mobile
