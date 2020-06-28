実は株より安全資産!？レバレッジETFを統計的に検証してみた

絶対投資するな！？レバレッジ・インデックスETFをpythonで考察してみた結果...

# 超短い結論
レバレッジ・インデックスETFは超割のいい宝くじ。適切に運用しよう。全ぶっ放するのはNG

# はじめに
僕が投資先を選定する上でレバレッジ・インデックスETF（以後レバレッジETF）に出会い。この記事はレバレッジETFが危険と言われるのはどうしても信じられなかったので自分で検証した記事です。

僕は俗にあるレバレッジETFの特性は勘違いによって生まれていると思います。そこで、この記事を通してレバレッジETFの強みと弱みを”統計的”な側面から客観的に見ていただきたいという思いを込めて書いています。ぜひ、この機会にレバレッジETFの世界を一緒に眺めて見ませんか？きっと面白く思えるはずです。ただし、

*あくまで投資は自己判断で。*

申し訳ありませんが、僕は皆様のお金に責任は持てませんのでご注意ください。信じるも信じないも皆様次第です。

では、サッソク見て行きましょう！！！

# 背景
昨今の暴落もあり投資が注目を集めてる気がします。しかし、個別株はかなり知識がないと厳しそうです。非証券マンなエンジニアにはそれはきつい。
そこで、何か、簡単に投資できて利回りが良いもの追い求めた結果たどり着いたのが「レバレッジETF」です。
レバレッジETFとは、何か参考となる株価に対してレバレッジ、つまり倍率をかけた株価になるように動く証券です。例えば、日経225の2倍レバレッジETFは日経225の株価の2倍の株価に連動して動きます。

要は、100万円日経225に投資する代わりに2倍レバレッジETFに投資すれば200万円日経225に投資したのと同じような効果を得られるということです。ただし、借金して100万円を200万円にしてるわけじゃないので、仮に日経225が0円になってもレバレッジETFに投資した100万円が0円になるだけで、借金をこさえる心配はありません。

ここだけ聞くと青天井が2倍で下が同じに見えるので最高の証券にも見えるのですが、そんな甘い話じゃないんですね。レバレッジETFには様々な人が様々な立場で話しています。

以下に立場別にいくつかリンクをご紹介します。


- 否定
    -  [マネーの手帳　レバレッジ型ETFの投資で知っておくべき特徴やリスクをまとめました](https://www.crowdport.jp/money-notebook/833/#:~:text=%E3%83%AC%E3%83%90%E3%83%AC%E3%83%83%E3%82%B8%E5%9E%8BETF%E3%81%A8%E3%81%AF%E3%80%81%E6%9D%B1%E8%A8%BC1%E9%83%A8%E3%81%AB%E4%B8%8A%E5%A0%B4,%E3%81%99%E3%82%8B%E4%B8%8A%E5%A0%B4%E6%8A%95%E8%B3%87%E4%BF%A1%E8%A8%97%E3%81%A7%E3%81%99%E3%80%82)
    - [高橋ダン様 【騙されるな】買ってはいけない金融商品？](https://www.youtube.com/watch?v=ecxP6wCQrQg)
    - [両学長　第40回 お手軽に莫大な利益を得る方法。レバレッジETFはアリか？【お金の勉強 株式投資編】](https://youtu.be/oRei15CZG14)
- 肯定
    - [rokohouse様 超低リスクで2億円を手にするレバレッジETFによる超長期投資法とは？](http://www.rokohouse.net/archives/2312)


>### リンク先記事補足
>否定派はyoutubeの動画が2件になってしまいました。普通のWEB記事にも多かった印象があるんですが、探そうと思うと見つからないもんです。もう1つのサイトもじゃっかん否定的ですが中立的です。どれも指数からの乖離などを説明する典型的な説明をなさっていると思います。
> 一応言っておくと、両学長さんもダン高橋さんも非常に知己に富んだ情報を発信してくれる方々です。発信者としては両名ともにおすすめできる方です。お二方の動画を上げたのは僕が見て記憶に新しかっただけです。
> 肯定派に上げたrokohouseさんの記事もどれも良記事です。ぼくと同じで統計的な性質に重きを置くエンジニアの方のようです。実は今書いている記事を書くまで存じ上げなかったのですが、周辺調査をする最中に発見し大体読ませていただきました。正直、rokohouseさんの記事読んでいれば、このQiitaの記事はそこまで差はないと思います。一応差分を作ったつもりではありますが。

僕はレバレッジETFについては肯定派よりだと思います。なぜなら、否定派の説明は数学的に考えて理屈に合わないと思うからです。では、その理屈と僕の納得が行かない理由を見ていきます。

## 否定派の理由
### レバレッジETFは日々の株価の動きにレバレッジをかけているので指数から乖離する
レバレッジの投資商品はいくつもあり、有名所だとFXが上げられると思いますが、レバレッジETFはFXと大きくことなるのが*前日比*に対してレバレッジをかけていることです。
この仕組の直感的でない(?)ところが原因で、例えば

> 10年でS&P500の株価が100%増加した => レバレッジ3倍S&PETFは300%増加した

は成り立ちません。「おいおい日経225の2倍で動くとかさっき自分で説明してたじゃん」と思った方。鋭いです。しかし、「あれは嘘だ」。ただ、同時に近似的には正解なんです。厳密には違うというだけ。

細かいことを言えば、レバレッジETFの増加分は元となる株価の倍数よりも小さかったり大きかったりするのです。
もう一度になりますが、それは、レバレッジETFの価格は元となる株価の1日よりも長い時間に対する価格変動に単純に倍数をかけただけの動きを保証しないからです。

しかし、本当に問題になるほど乖離するのでしょうか？

では株価変動の様子を実例で見ていきましょう。

例えば、2012/4/2-2020/4/2の動きで、SP500[^1]”先物”[^2]は1.81倍に、対してSP500の3倍レバレッジETFであるSPXLは3.47倍です。単純な計算であれば 1+0.81*3 = 3.43倍なので、少し単純計算よりも儲けが多いです。 しかし、まぁ誤差の範囲内でしょう。

[^1]: SP500はアメリカの株式の代表的な株価指数です。最近はこれを買っておけって意見がほとんどですね。
[^2]: あえて”先物”と書きましたが、SPXLは先物の3倍の値動きを目指すものなので先物を指標に使いました。ただ、先物も現物もめちゃくちゃ値動きが異なるということはないので先物でも現物でも大した差はないです。現物は例示の機関で1.74倍になってました。

このように確かにレバレッジETFは日々の価格に対して”しか”倍率をかけていませんが、それってあまり問題ではないんですね。

Qiitaらしく数学的な話をするならこれは高校でならう近似式のお話そのもです。 $r_i << 1$である$r_i$について次の近似式が成り立ちます。

```math
\prod_{i=1}^{N} (1+r_i) \simeq 1 + \sum_{i=1}^{N} r_i
```

この式が示すのは、「1%上昇、1.5%上昇、0.5%下降した価格はおおよそ2%(=1+1.5-0.5)上昇になるよ」という至って直感的な話です。

つまり、価格変動が1よりも十分に小さいといえる範囲（数％）ならばその変動率を足し算した変化率が全体の変化率とほぼ言えるのです。SP500などの指数は暴落時などを除けば1%以内の動きで収まります。となれば、この近似式が成り立つので長期で見てもそこまで乖離することはないのですね。

まとめると、日々の価格変動にしか倍率をかけていないからと行って全体の指数がハチャメチャになるかというとそんなことはなくないということです。近似的には全体でも倍率をかけた株価になってくれます。

### レンジ相場に弱い

レンジ相場とは上げて戻して上げて戻してとジグザグして全体としては上昇も下降もしない相場のことを言います。

仮にレバレッジETFが元とする指数が「-5%, +5%, -5%, +5%」と動くときは3倍のレバレッジETFは「-15%, +15%, -15%, +15%」となります。両方の最終的な株価の変動率を計算してみると

```math
origin:          0.95 \times 1.05 \times 0.95 \times 1.05 = 0.995
3倍レバレッジETF: 0.85 \times 1.15 \times 0.85 \times 1.15 = 0.956 
```

とこのように、レンジ相場にも関わらずレバレッジETFの方がより下落幅が大きくなるので、多くの場合、この減少を「レバレッジETFの原価効果」といい、「レバレッジETFはレンジ相場に弱い」と言われています。

たしかに3倍レバレッジETFの方が下がりが大きいし、それは3倍どころではありません。

ここでも数式のモデルを使って見ましょう。レンジ相場を$r$と$-r$の変化率の繰り返しと定義し、$2N$日後の株価を考えるものとします。このとき$r^3 << 1$で無視できるものとします。すると、以下の近似式が成り立つのです。

```math
2N日後の価格の比 = (1+r)^N (1-r)^N = 1 - Nr^2
```

さきほどの例で言えば\$r = 5%\$なので　\$2 \times 0.05^2 = 0.005\$と下落幅ピタリですね。では、レバレッジETFはどうかというと、この変動率\$r\$に倍率Lをかけるだけなので

```math
2N日後のレバレッジETFの価格の比 = (1+Lr)^N (1-Lr)^N = 1 - N(Lr)^2
```

単純ですね。ただし、$L$の2乗で効いてくるのがポイントです。先程の例で言うなら、$2 \times (3 \times 0.05)^2 = 0.045$です。下落幅は3倍じゃなくて、9倍だったんですね！。

というように、レンジ相場での下落幅は倍率の2乗で効くことがわかりました。恐ろしいですねー。

ただし、思いおこしてほしいのが、$r^2$ってそもそも小さくないか？ということです。
今回は5%の例を上げましたが、日々の動きが5%の指数って結構荒れてます。普通は1％くらいです。
つまり$r^2$自体が結構無視できる程度の変化率なのかなと思います。1万分の1ですからね。

ただし、暴落時のV時回復は別です。今回のコロナ暴落もそうですが、値動きが激しいレンジは$r^2$の効果がでるでしょう。実際、今回のコロナ暴落で米国株はほぼ元の価格に2020/6/27現在で戻っていますが、レバレッジETFはその限りではありません(SP500は2月のピークから-10%程度、対して、3倍レバレッジETFのSPXLは-47%)。この点は注意が必要です。ただ、3月からここまで120日程度あるので、$Nr^2 = 0.1$となり、$9* Nr^2 = 0.9$のはずですが、そこまでの下落ではないので、モデルが単純過ぎた結果なのかモデルほどの酷さはないようです。そもそも、毎日同じ変動率なのは変ですからね。そういうところから来る誤差だと思います。

この項でお伝えしたかったのは、一般に言うレバレッジETFの原価効果は何もレバレッジETFにのみに存在する効果ではなく、レバレッジによって増強される程度は高々$(Lr)^2$であるということです。$r$が小さければほとんど問題になりません。

## 肯定できる理由
### 期待値を上げる効果が期待できる
そもそもSP500などに投資する目的って多くが「長期投資すれば”必ず”儲かる」からなんです。このあとちゃんと検証もしますが、たしかにSP500は長期間持つことでほとんど損失することなく利益を得ることができます。

ここで少し話を変えてみましょう。

例えば、ここにお金を入れると必ず2倍に増えてお金がでる装置があったとします。この装置は3回だけ使えるとしましょう。そんな装置があったら、どうします？

僕ならこうします。まず銀行に行ってこの装置の説明をします。そこからありとあらゆる自分の資産を担保に極限までお金を借りて、そのお金を装置に入れます。出てきたお金はもう一度通します。また、もう一度通します。こうすることで例えば、1億円借りられれば大体7億円利益が得られます。やべー。今手元にあるお金が100万円しかなければ、利益は700万円ですから、その差は圧倒的です。

つまりです。必ず儲かる仕組みがあるなら借金をしてでもやるべきなんです。

話を戻します。

SP500に投資するときは「長期投資すれば”必ず”儲かる」から投資するのでした。ここでいう長期投資はよく言うのは20年くらい。この長期投資ができる回数って大体の人にとって3回くらいですかね。

そうです。本質的には先程の装置の例えとそこまで変わりません。お金を入れてからでるまで20年かかるだけです。（そこが1番の問題ですが）

なので、借金をしてでも投資する、レバレッジETFにはそういう意味で合理性があるといえると思います。

ただ、ここまでは定性的な話でした。数式でも見ていきましょう。

#### 数式で検証してみる

ある証券Aの20年後に得られる価格変動率を確率変数$R$とします。　では、そのAの$L$倍のレバレッジETFについてその平均値と分散を考えて見ましょう。しかし、これは簡単ですね。

```math
レバレッジETFの平均値 = L \times E[R]
レバレッジETFの分散 = L^2 \times VAR[R]
```

つまり、レバレッジETFは得られる期待値を$L$倍して分散は$L^2$します。例えば、必ず儲かるマシンの話なら$VAR[R]$はそもそも0なので、期待値を上げる効果だけが作用してお得だった訳です。

しかし、実際の長期投資はそういうわけではありません。期待値を上回る利益の方向にも逆に下回る方向にも分散があります。問題になるのは、もちろん下回る方向の分散です。上回ってくれる分には何も文句がありませんからね。

しかし、こればっかりは何もフォローの仕様がありません。調べてわかったことでもありますが、きちんと損する可能性が生まれてしまうくらいには下方向の分散を大きくしています。SP500に投資している分には必ず儲かるのに、その*レバレッジETFでは、無価値化する場合が出始める程度には危険度が増します*。

無価値化するというのは想像異常に危険で、半値程度ならそのあと倍以上に上がってくれれば這い上がれるのですが、本当に0になってしまうと何をかけても0なので救いようがないわけです。実はこれを救う方法もあるのですが、あとに書きますね。

危険度の話ばかりフォーカスしましたが、利益の面で強調したいのは*期待値や中央値という尺度では明らかにレバレッジを効かせた方が良い利益をもたらす*こともわかりました。しっかり式通りの性質があるのですね。

しかも、無価値化すると怖いことを書きましたが、その確率は1%とかそこらです。十分すぎるくらい大きいと個人的には思いますが、繰り返しますが、期待値や中央値はきちんと良くなってます。

実際のところ、否定派の理由として使うなら「無価値化する確率が少なからずあること」ここを十分に指摘するべきだと僕は思います。自分が100個の独立な世界線を生きれる量子的な存在ならいいですけど、そんなんじゃないですからねｗ。1%の確率でも分だら死ぬならやりたくないわけです。

# 検証

さぁ、なが～いプロローグでしたが、やっと本題の検証です。以上の事前検証からわかるのはレバレッジETFのリスクとメリットを定量的に測ること。これを歴史的なデータから定量的にやることだと考えました。

考察するにあたりある程度前提をご紹介します。

## 対象
- [S&P500](https://finance.yahoo.com/quote/%5EGSPC/history?p=%5EGSPC)
- [NASDAQ100](https://finance.yahoo.com/quote/%5EIXIC/history?p=%5EIXIC)

個人的に好きな指数です。おそらく多くの人が知っていて投資したいindexだと思います。S&P500に関しては92年分のデータが手に入ったのでかなり良い統計量が与えられそうです。(大恐慌時の株価も検証に入ります)データのソースはリンクとして貼っておきました。

また、レバレッジETFとして各々の指数の3倍レバレッジETFを想定します。これは実際に存在するSPXLとTQQQに相当します。しかし、SPXLとTQQQはリーマンショック以降に誕生した証券でそれ以前の価格を参照することができず、リーマンショック以降は明らかな株高だったのでレバレッジETFに有利な方向に統計的に偏ります。

そこで、本記事の検証ではSPXLやTQQQのデータはあえて用いずにSP500とNASDAQ100の指数のみから3倍レバレッジETFをシミュレートすることでその代わりをさせることとします。

このとき、シミュレーションの方法はそれぞれの指数の終値前日比に対して3倍を掛けて得られた3倍前日比から累積積を取ることで計算しました。

## もしリーマンショック以前にレバレッジETFがあったら

検証の前に株価がどう推移したのかをレバレッジETFと元の指数を並べて見てみましょう。

|  SP500  |  NASDAQ100 |
| :-: | :-: |
|  ![sp500の価格変動](images/sp500_price_moving.png) |  ![nasdaq100の価格変動](images/nasdaq100_price_moving.png)   |

どちらのデータも始まりの日を価格１として計算し、株価を対数にした片対数グラフにしました。

まず意外だったのは、レバレッジETFは前日比を３倍するという仕組み上元とする指数の前日比が-33%を超えると-100%の下落となり無価値化してしまうとおもったのですが、今回の検証の範囲ではそういう日は一度もなかったようです。

とはいえ、SP500の大恐慌時の暴落はひどかったようで、一時は1/1000にまで価格が下落しています。ほぼ無価値化してますね。
ただ、その後はSP500のレバレッジETFはリーマンショックなどの暴落の影響を受けて1/10の価格になるなどを経験しつつも大方順調に価格を伸ばています。

NASDAQ100の方は大恐慌のときの株価がなかったため、主に.comバブルの影響が強い印象です。.comバブルとリーマンショックを合わせれば価格が1/500程度に下がっています。

このように、レバレッジETFは暴落時に価格をほぼ無価値にしてしまう危険性がつきものだということがわかりました。つまり、暴落手前まで伸ばしてきた資産を暴落でほぼ0にしてしまうのです。これじゃ、いくら利回りが良くてもいつかは破綻します。

しかし、同時に無価値化したあとも元の指数と並びかつ超えることができる程に暴落後の伸びも著しいものがあります。
つまり、やはり利回り自体はいいけれどいつかは紙くずになる。それがレバレッジETFです。

## 今買ったETFはn年後どうなってる？

nには1,2,4,5,10,20,30を使いました。
検証方法はまずランダムに投資開始日を決定して、そこからちょうどn年後の価格の価格を見て何倍になったかを1万回サンプリングすることによって検証しました。
この検証によって、今日買った証券がn年後、何倍になっているかを予想することができます。

その結果は次の表のようになりました。

### sp500
|         |期待値|  1%  |  5%  | 10%  | 15%  | 20%  | 25%  | 50% | 75% | 80% | 85%  | 90%  | 95%  | 99%  |
|---------|-----:|-----:|-----:|-----:|-----:|-----:|-----:|----:|----:|----:|-----:|-----:|-----:|-----:|
|1y_sp500 | 1.072|0.5849|0.7462|0.8328|0.8799|0.9213|0.9586|1.087|1.191|1.219| 1.250| 1.291| 1.350| 1.489|
|2y_sp500 | 1.150|0.4101|0.6738|0.7929|0.8831|0.9565|1.0127|1.156|1.310|1.362| 1.415| 1.472| 1.582| 1.838|
|3y_sp500 | 1.225|0.3050|0.6790|0.7682|0.8807|0.9646|1.0354|1.234|1.415|1.464| 1.534| 1.633| 1.821| 2.050|
|4y_sp500 | 1.304|0.3324|0.6235|0.7918|0.8912|0.9616|1.0292|1.318|1.543|1.594| 1.668| 1.771| 2.008| 2.439|
|5y_sp500 | 1.401|0.3801|0.6972|0.8354|0.8964|0.9765|1.0589|1.388|1.679|1.753| 1.868| 1.976| 2.208| 2.867|
|10y_sp500| 1.969|0.4895|0.6915|0.9483|1.0658|1.1714|1.2791|1.860|2.623|2.735| 2.889| 3.126| 3.543| 4.034|
|20y_sp500| 4.136|0.6182|1.5686|1.8270|1.9676|2.1490|2.3559|3.528|5.475|5.761| 6.115| 6.849| 9.589|11.460|
|30y_sp500| 7.600|1.6423|3.4498|4.2480|4.7292|5.0750|5.3154|7.032|9.334|9.988|11.063|12.217|13.868|15.636|

### sp500レバレッジETF
|            |期待値|   1%   |  5%   |  10%  |  15%  |  20%  |  25%  | 50%  |  75%  |  80%  |  85%  |  90%  |  95%  |  99%  |
|------------|-----:|-------:|------:|------:|------:|------:|------:|-----:|------:|------:|------:|------:|------:|------:|
|1y_sp500_x3 | 1.233|0.109745|0.29547| 0.4835| 0.5885| 0.6925| 0.7974| 1.208|  1.573|  1.686|  1.815|  1.985|  2.313|  2.992|
|2y_sp500_x3 | 1.490|0.019428|0.16976| 0.3372| 0.5008| 0.6574| 0.8062| 1.320|  1.971|  2.181|  2.474|  2.800|  3.397|  4.661|
|3y_sp500_x3 | 1.796|0.008216|0.15377| 0.2486| 0.4107| 0.6126| 0.8502| 1.556|  2.327|  2.559|  2.949|  3.470|  4.759|  7.039|
|4y_sp500_x3 | 2.216|0.004204|0.09563| 0.2553| 0.4015| 0.5883| 0.7896| 1.790|  2.821|  3.113|  3.629|  4.577|  6.549| 10.452|
|5y_sp500_x3 | 2.762|0.004370|0.07741| 0.2670| 0.3708| 0.5266| 0.7436| 1.993|  3.641|  4.128|  4.801|  6.036|  8.597| 15.772|
|10y_sp500_x3| 6.647|0.002661|0.04547| 0.2320| 0.4333| 0.6099| 0.8442| 3.577|  8.547| 10.323| 13.187| 17.218| 27.053| 40.076|
|20y_sp500_x3|41.201|0.002241|0.27435| 1.3274| 1.9549| 2.4473| 2.8453| 8.373| 44.691| 61.330| 77.435|113.823|220.332|317.413|
|30y_sp500_x3|85.558|0.025679|0.59219|13.5687|17.4862|21.0602|23.4252|43.245|111.102|143.500|183.405|229.073|302.146|477.023|

### nasdaq100
|             |期待値|  1%  |  5%  |  10%  |  15%  |  20%  |  25%  | 50%  | 75%  | 80%  | 85%  | 90%  | 95%  | 99%  |
|-------------|-----:|-----:|-----:|------:|------:|------:|------:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|
|1y_nasdaq100 | 1.116|0.5274|0.7103| 0.8109| 0.8726| 0.9543| 0.9994| 1.132| 1.236| 1.268| 1.316| 1.371| 1.473| 1.726|
|2y_nasdaq100 | 1.238|0.4142|0.6206| 0.7965| 0.9441| 1.0019| 1.0676| 1.245| 1.452| 1.486| 1.528| 1.594| 1.708| 2.232|
|3y_nasdaq100 | 1.368|0.3618|0.5946| 0.8083| 0.9110| 1.0520| 1.1399| 1.385| 1.606| 1.660| 1.721| 1.814| 2.070| 2.537|
|4y_nasdaq100 | 1.520|0.4986|0.6299| 0.7571| 0.9321| 1.0557| 1.1338| 1.559| 1.818| 1.894| 1.996| 2.109| 2.411| 3.333|
|5y_nasdaq100 | 1.697|0.5252|0.7388| 0.8116| 0.9715| 1.0910| 1.1792| 1.711| 2.077| 2.165| 2.278| 2.407| 2.719| 3.966|
|10y_nasdaq100| 2.850|0.5138|1.0136| 1.4516| 1.6600| 1.8210| 1.9444| 2.553| 3.398| 3.677| 3.956| 4.346| 5.310|10.051|
|20y_nasdaq100| 7.070|1.8617|2.9467| 3.3482| 3.6162| 3.9314| 4.1309| 5.403| 9.306|11.125|12.131|13.066|15.008|20.372|
|30y_nasdaq100|17.384|8.2901|9.8052|10.4582|11.5588|12.3461|13.1357|15.916|21.244|22.271|23.048|24.596|27.442|39.013|

### nasdaq100レバレッジETF
|                |期待値 |   1%   |   5%   |  10%  |  15%  |  20%  |  25%  | 50%  |  75%  |  80%  |  85%  |  90%  |  95%   |  99%   |
|----------------|------:|-------:|-------:|------:|------:|------:|------:|-----:|------:|------:|------:|------:|-------:|-------:|
|1y_nasdaq100_x3 |  1.427|0.070984| 0.26381| 0.4577| 0.5738| 0.7895| 0.9245| 1.369|  1.766|  1.888|  2.078|  2.313|   2.796|   4.529|
|2y_nasdaq100_x3 |  1.896|0.027423| 0.13385| 0.3775| 0.6520| 0.8326| 0.9927| 1.656|  2.634|  2.882|  3.145|  3.409|   4.054|   6.293|
|3y_nasdaq100_x3 |  2.542|0.013903| 0.12862| 0.2515| 0.4159| 0.7231| 0.9719| 2.165|  3.430|  3.820|  4.336|  4.965|   6.178|   9.088|
|4y_nasdaq100_x3 |  3.539|0.026296| 0.13224| 0.2568| 0.3581| 0.5152| 0.8400| 3.004|  4.589|  5.270|  6.181|  7.621|   9.725|  16.355|
|5y_nasdaq100_x3 |  5.108|0.027536| 0.07451| 0.3078| 0.4036| 0.5225| 0.7347| 3.709|  6.706|  7.706|  9.042| 10.634|  14.098|  30.401|
|10y_nasdaq100_x3| 21.348|0.008965| 0.08759| 0.3585| 0.5901| 0.9416| 1.4631| 6.377| 20.045| 25.588| 34.684| 48.138|  64.706| 308.601|
|20y_nasdaq100_x3|190.055|0.174684| 0.64021| 0.8633| 1.2858| 1.5467| 1.8932|10.645|246.497|400.073|560.955|691.165| 860.859|1675.155|
|30y_nasdaq100_x3|434.339|7.297600|11.31917|14.0263|17.9216|22.2937|27.3989|56.430|281.821|327.326|382.029|517.423|2746.792|7719.617|

それぞれ数字はn年後に何倍の価格になったかを表しており、行は期待値と分位点を表しています。例えば、行 50$の列　10_nasdaq100_x3の値はNASDAQ100の3倍レバレッジETFの株価が10年後に取りうる価格の中央値を表しています。

まず、このデータからわかるのは株価の指数は半値になることすらほとんどないということです。SP500のデータを見てみると下位1%の値で0.58倍です。半値になることを恐れなければ、かなり底堅く利益を狙えることが伺えます。

一方で、レバレッジETFは、どのn年後をみても無価値化するリスクを抱えていることがわかります。例外的にnasdaq100の30年後だけ下位1%でも7倍になっていますが、NASDAQ100のデータが50年ほどしかなく、30年のスパンを見れば.comバブル直前での買いをせずにからだと考えられます。よって、レバレッジETFのデメリットはやはり下振れリスクの大幅増にあると言えます。

ただし、利益の面でも注目が必要です。元の指数とレバレッジETFの1年後の中央値を比較すれば、SP500では8.7%と20.8%で2.5倍程度、NASDAQ100では13.2%と36.9%で、レバレッジETFの方が利益も大きいことは明らかです。

もっとも夢のある見方をすれば、NISAの投資期間である5年を見ると、NASDAQ100のレバレッジETFは上位10%で10倍に価格を伸ばしています。NASDAQ100自体の上位10%が2倍であることを踏まえると3倍どころでない利益だとわかります。
NISAの投資枠は年間120万円ですから、120万円投資したとすると、1200万円を得ることができたという訳です。すごすぎ

また、それぞれの証券について期待値を見ても同様にレバレッジETFが3倍よりも良い成果をあげていることがわかります。しかし、期待値については上振れの外れ値の影響を強く受ける性質があるので注意が必要です。


### 箱ひげ図
次にこれらのデータを箱ひげ図で見てみましょう。

|レバレッジ/指数| SP500 | NASDAQ100 |
| :-: | :-: | :-: |
|レバレッジなし| ![sp500](images/hakohige_sp500.png) |  ![nasdaq100](images/hakohige_nasdaq100.png)|
|レバレッジあり| ![sp500_x3](images/hakohige_sp500_x3.png)| ![nasdaq100_x3](images/hakohige_nasdaq100_x3.png)|

これを見ると、レバレッジなしの指数はきれいに時間が経つごとに利益が伸びる性質があるのがわかります。美しさすら感じます。
面白いの最小値の動きで、年月を大きくすると最初は小さくなりますが、ある年を超えると大きくなります。下振れリスクが小さい証拠です。
ただ、これ見て気づいたのですが、どこかで20年以上SP500を持っていれば損した年はなかったっていうのを聞いた記憶があったんですが、損する日はどこかにはあるみたいですね。5%よりは低い確率みたいですが。おそらく大恐慌あたりでしょうね。

## 過去に５年間積立投資していたら統計的にどうだった？

積立投資を想定することには統計的には意味があまりないと思うのですが、実際に投資すると思ったら、普通は積立だと思うのでデータとしては同様にこちらも載せておきます。積立は色々ありますが、日割りでドルコスト平均法の積立した場合を想定しています。

ただし、僕もROKOHOUSE様同様に固まった現金のある方は積立よりも一括投資をおすすめします。理由は次の記事が参考になります[ドルコスト平均法という残念な宗教](http://www.rokohouse.net/archives/2605)

表記は[前項](#今買ったETFはn年後どうなってる？)と同じです。

### sp500
|         |期待値|  1%  |  5%  | 10%  | 15%  | 20%  | 25%  | 50% | 75% | 80% | 85% | 90% | 95% | 99% |
|---------|-----:|-----:|-----:|-----:|-----:|-----:|-----:|----:|----:|----:|----:|----:|----:|----:|
|1y_sp500 | 1.034|0.7213|0.8566|0.9077|0.9347|0.9558|0.9761|1.045|1.097|1.111|1.128|1.150|1.183|1.250|
|2y_sp500 | 1.073|0.6341|0.7992|0.8837|0.9250|0.9638|0.9944|1.091|1.166|1.187|1.211|1.246|1.306|1.399|
|3y_sp500 | 1.110|0.5393|0.7751|0.8863|0.9355|0.9792|1.0125|1.131|1.216|1.236|1.268|1.319|1.413|1.516|
|4y_sp500 | 1.154|0.5084|0.7929|0.9078|0.9542|0.9996|1.0355|1.166|1.267|1.303|1.344|1.410|1.540|1.648|
|5y_sp500 | 1.197|0.6736|0.8169|0.9071|0.9614|1.0100|1.0539|1.198|1.316|1.357|1.411|1.508|1.640|1.821|
|10y_sp500| 1.447|0.7470|0.9340|1.0143|1.0679|1.1152|1.1554|1.419|1.678|1.731|1.812|1.933|2.199|2.510|
|20y_sp500| 2.256|1.0953|1.2015|1.2840|1.3638|1.4708|1.5858|2.157|2.798|2.912|2.997|3.179|3.951|4.969|
|30y_sp500| 3.540|1.6855|1.8777|2.0454|2.2146|2.5034|2.7015|3.285|4.205|4.392|4.594|4.845|6.513|8.066|

### sp500レバレッジETF
|            |期待値|  1%  |  5%  | 10%  | 15%  | 20%  | 25%  | 50%  | 75%  | 80%  | 85%  | 90%  |  95%  |  99%  |
|------------|-----:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|------:|------:|
|1y_sp500_x3 | 1.111|0.3523|0.5830|0.7141|0.7859|0.8453|0.9049| 1.122| 1.301| 1.349| 1.406| 1.492|  1.616|  1.890|
|2y_sp500_x3 | 1.244|0.2178|0.4683|0.6308|0.7266|0.8126|0.9043| 1.243| 1.534| 1.618| 1.721| 1.871|  2.120|  2.538|
|3y_sp500_x3 | 1.370|0.1837|0.4057|0.6030|0.7250|0.8154|0.9170| 1.348| 1.697| 1.808| 1.947| 2.156|  2.606|  3.360|
|4y_sp500_x3 | 1.548|0.1592|0.4133|0.5932|0.7140|0.8622|0.9866| 1.437| 1.894| 2.063| 2.274| 2.595|  3.364|  4.361|
|5y_sp500_x3 | 1.734|0.2154|0.4175|0.5823|0.7314|0.8968|1.0418| 1.522| 2.083| 2.275| 2.557| 3.183|  4.118|  5.722|
|10y_sp500_x3| 3.105|0.2350|0.3864|0.6508|0.8761|1.0048|1.1453| 2.432| 3.673| 4.249| 5.157| 6.422|  9.674| 14.715|
|20y_sp500_x3|11.829|0.6800|0.8909|1.0567|1.2385|1.5748|1.9222| 6.178|16.136|19.593|23.274|27.939| 41.816| 79.587|
|30y_sp500_x3|33.328|2.9051|4.1168|4.9064|5.4754|6.0304|6.6525|15.205|42.602|47.148|60.573|74.734|121.520|219.718|

### nasdaq100
|             |期待値|  1%  |  5%  | 10%  | 15%  | 20%  | 25%  | 50% | 75% | 80% | 85% | 90% | 95%  | 99%  |
|-------------|-----:|-----:|-----:|-----:|-----:|-----:|-----:|----:|----:|----:|----:|----:|-----:|-----:|
|1y_nasdaq100 | 1.055|0.7077|0.8137|0.8923|0.9358|0.9672|0.9882|1.066|1.125|1.141|1.162|1.198| 1.243| 1.388|
|2y_nasdaq100 | 1.117|0.6254|0.7383|0.8541|0.9434|0.9953|1.0313|1.130|1.224|1.245|1.271|1.312| 1.382| 1.595|
|3y_nasdaq100 | 1.180|0.5854|0.7130|0.8685|0.9887|1.0466|1.0858|1.192|1.316|1.341|1.363|1.404| 1.487| 1.768|
|4y_nasdaq100 | 1.257|0.6093|0.7723|0.9017|1.0266|1.0804|1.1234|1.256|1.405|1.433|1.461|1.524| 1.685| 2.091|
|5y_nasdaq100 | 1.340|0.6238|0.8268|0.9652|1.0302|1.1057|1.1558|1.333|1.501|1.534|1.573|1.658| 1.838| 2.477|
|10y_nasdaq100| 1.823|0.7614|1.0609|1.1463|1.2061|1.2644|1.3661|1.761|2.067|2.139|2.286|2.466| 3.003| 4.285|
|20y_nasdaq100| 3.170|1.3688|1.6798|1.8028|1.9104|2.1114|2.2061|2.774|3.717|3.924|4.270|4.936| 6.256| 9.064|
|30y_nasdaq100| 5.753|2.7137|3.3677|3.6086|3.7774|3.9042|4.0986|4.847|5.787|6.004|6.597|8.284|13.892|19.241|

### nasdaq100レバレッジETF
|                |期待値 |  1%  |  5%  | 10%  | 15%  | 20%  | 25%  | 50%  | 75%  | 80%  | 85%  |  90%  |  95%   |  99%   |
|----------------|------:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|------:|-------:|-------:|
|1y_nasdaq100_x3 |  1.197|0.3179|0.5289|0.6874|0.7847|0.8749|0.9410| 1.183| 1.404| 1.473| 1.559|  1.709|   1.886|   2.550|
|2y_nasdaq100_x3 |  1.438|0.2239|0.3920|0.6013|0.8254|0.9414|1.0546| 1.388| 1.774| 1.862| 1.982|  2.139|   2.411|   3.690|
|3y_nasdaq100_x3 |  1.719|0.1853|0.3150|0.6382|0.8998|1.0572|1.2116| 1.578| 2.210| 2.367| 2.492|  2.724|   3.077|   4.320|
|4y_nasdaq100_x3 |  2.101|0.1650|0.3010|0.7009|0.9869|1.1630|1.2720| 1.849| 2.667| 2.868| 3.092|  3.495|   4.347|   6.841|
|5y_nasdaq100_x3 |  2.521|0.1630|0.3584|0.7663|0.9791|1.1618|1.3676| 2.148| 3.168| 3.381| 3.736|  4.395|   5.832|   8.368|
|10y_nasdaq100_x3|  7.227|0.2054|0.4687|0.7034|0.8557|1.0787|1.3414| 4.229| 7.990| 9.072|11.034| 14.231|  23.094|  52.777|
|20y_nasdaq100_x3| 36.423|0.3499|0.6734|0.9322|1.2093|2.0550|2.5179| 5.876|45.566|60.827|71.801| 92.401| 152.204| 361.352|
|30y_nasdaq100_x3|209.080|1.4975|2.4697|2.9681|3.3808|3.8410|5.0386|11.469|30.962|36.079|49.351|132.403|1602.172|4506.264|

### 箱ひげ図
|レバレッジ/指数| SP500 | NASDAQ100 |
| :-: | :-: | :-: |
|レバレッジなし| ![sp500](images/tumitate_hakohige_sp500.png) |  ![nasdaq100](images/tumitate_hakohige_nasdaq100.png)|
|レバレッジあり| ![sp500_x3](images/tumitate_hakohige_sp500_x3.png)| ![nasdaq100_x3](images/tumitate_hakohige_nasdaq100_x3.png)|

リスク小さくなるからと思いがちですが、実際のところドルコスト平均法で投資すると利回りが減るのは明らかですが、リスクはそこまで小さくなりません。
当たり前ですが、最後方の投資は結局買ってすぐ売る想定になってしまい、そもそも投資期間が十分に保てていないので利益も損益も出ていないが原因ですね。
投資は基本長い方が有利なので、投資期間にばらつきがでるドルコスト平均法は弱くなるわけです。
ただし、実際問題一生分の投資資金を今この瞬間に投資することは不可能なので、通常は積立投資せざるを得ないです。

なので、この結果からは証券の性質というよりもより実践的な利回りの想定ができます。
例えば、NISAや積立NISAを行った場合の想定収益です。
NISAはあと3年間だけ使える制度なので、3年間の利回りを見ると収益を想定できます。
積立NISAなら20年間の利回りで想定できます。ただし、レバレッジETFは使うことができません。
他にもレバレッジETFは使えませんが積立NISAの20年の投資期間の利回りなどが計算できるでしょう。

#### 残り3年のNISAで積立したとき
|               |期待値|  1%  |  5%  | 10%  | 15%  | 20%  | 25%  | 50% | 75% | 80% | 85% | 90% | 95% | 99% |
|---------------|-----:|-----:|-----:|-----:|-----:|-----:|-----:|----:|----:|----:|----:|----:|----:|----:|
|3y_sp500       | 1.110|0.5393|0.7751|0.8863|0.9355|0.9792|1.0125|1.131|1.216|1.236|1.268|1.319|1.413|1.516|
|3y_sp500_x3    | 1.370|0.1837|0.4057|0.6030|0.7250|0.8154|0.9170|1.348|1.697|1.808|1.947|2.156|2.606|3.360|
|3y_nasdaq100   | 1.180|0.5854|0.7130|0.8685|0.9887|1.0466|1.0858|1.192|1.316|1.341|1.363|1.404|1.487|1.768|
|3y_nasdaq100_x3| 1.719|0.1853|0.3150|0.6382|0.8998|1.0572|1.2116|1.578|2.210|2.367|2.492|2.724|3.077|4.320|

やっぱり積立ちゃうと利益は狙いにくくなりますね。その割にレバレッジETFは1割り程度に減る確率はあるのでまだ怖いです。

#### 積立NISAで20年積立したとき
|             |期待値| 1%  | 5%  | 10% | 15% | 20% | 25% | 50% | 75% | 80% | 85% | 90% | 95% | 99% |
|-------------|-----:|----:|----:|----:|----:|----:|----:|----:|----:|----:|----:|----:|----:|----:|
|20y_sp500    | 2.256|1.095|1.201|1.284|1.364|1.471|1.586|2.157|2.798|2.912|2.997|3.179|3.951|4.969|
|20y_nasdaq100| 3.170|1.369|1.680|1.803|1.910|2.111|2.206|2.774|3.717|3.924|4.270|4.936|6.256|9.064|

ここまで底堅いと、政府が20年の積立NISAを推奨したい気持ちがわかりますね。

# 考察
## レバレッジETFの危険性は無価値化にある
無価値化はSP500やNASDAQ100に投資しているならばおよそ想像する必要のない危険性です。
先にも述べた通り、無価値化すると、追加投資なしにはその資金が取り返せません。
その危険性がレバレッジETFにはあります。

本記事の検証では、92年間の歴史上では無価値化が起こらなかったことがわかりましたが、1000万円が1万円になるとか数十万円になる危険性はことがわかりました。

今回は証券のなかでは比較的安定している指数であるSP500とNASDAQ100のレバレッジETFの結果だけを見ましたが、より動きの激しい指数や株のレバレッジETFはその危険性が高まるのは言うまでもありません。

一例をあげれば、原油の指数のレバレッジETN（ほぼETFと同義）が無価値化したことがつい最近ありました。[Bloombergの記事](https://www.bloomberg.co.jp/news/articles/2020-04-22/Q9764VDWLU6T01)

SP500やNASDAQ100のレバレッジETFがいつこうなるかとは誰も予想できません。レバレッジETFに投資する際は明日にも無価値化する危険性が常にあるということだけは抑える必要があるかと思います。

## レバレッジETFは買うな？
「無価値化する危険性があるからレバレッジETFを買うな」というわけではありません。
心づもりを持つ必要があるのと、それを知った上で正しい運用をすべきです。
では具体的にどんな運用かと言うと、すべての投資資産をレバレッジETFで持たなければよいのです。

まず、検証してきた通りレバレッジETFの利回りは確実に元の指数よりも高いです。この良い性質を自分のポートフォリオに生かさない手はないと僕は考えます。

ここで50%の確率で10倍、50%の確率で0倍のお金を返却するスロットがあったとしましょう。
すぐわかるように、このマシンの期待値は5倍なので、回せば回すほど得しそうです。
こんなうまい話は実際にはないでしょう。
では、掛け金をすべてこのマシンに投下し、得られた利益もすべてこのマシンにかけることを繰り返しましょう。
そうすれば利益を最大化できるはずです…。

しかし、これをやってみると、どこかで必ず資産がなくなります。
無限回の試行を行えば必ず0倍の場合を経験するはずだからです。

この例はかなりシンプルな例ですが、レバレッジETFの危険性を理解するのに有効です。
おわかりの通り、このマシンはレバレッジETFの比喩です。1試行が1年間の運用とでも考えると良いと思います。
しかし、ここで終わりではありません。
では、このマシンに投下する資金はかならず現状の資金の1割だとした場合はどうでしょうか？
これなら、仮に0倍で帰って来ても1割の損失で済ませることができます。

では、実験しましょう。
スロットを20回試行するとして、毎度資金の1割だけをスロットに投下します。スロットから得られた利益は資金に追加することとします。この一連の試行を1万回試し、資金の最終的な利回りを見てましょう。
その結果はつぎの図のようになります。

![スロットマシーンの結果](images/slotmachine_simple.png)

結果、下位1%の利回りが5倍、元本割れリスク0.02%、利回り中央値818倍、利回り期待値214倍となりました。

どうでしょうか？リスクをほぼなくし、利益はしっかりあるのがわかると思います。

実際にはこんな上手いスロットマシーンあるわけないのですし、そもそも、期待値5倍なので$5^20=9 \times 10^12$が狙えるはずなんてことを考えると利益もしょぼく見えます。
しかし、全資金を常にかける方法に比べて遥かに安全かつ利回りを得ることができるのですから、よしとするべきです。

この資産を保全するやり方は投資の世界では古くから行われるアセットアロケーションとか資産配分と言われる行為そのものです。

投資的に言うなら「スロットマシーン1割、現金9割の資産配分を行い、毎試行ごとにリバランスした」となります。

資産配分とかリバランスとか、それっぽいこと言ってますが、要はさっきの投資法そのものです。

つまり、リスクの高い投資手法にすべてを投資するのではなく、分散して投資しようというある意味当たり前な話なのです。

## 資産配分は逆レバレッジ？

この資産配分の話を見るとこれは逆レバレッジではないかと考える方がいらっしゃると思います。
つまり、10投資できたものを5で抑えるのなら0.5倍の倍率を証券に掛けたと考えることができるからです。
この捉え方は何も誤りはありません。全くのそのとおりです。

なら、3倍レバレッジETFを0.5の倍率掛けたり、ましては1/3の倍率を掛けては、せっかくのレバレッジETFの意味がないじゃないか。

そう思いますよね。

次の項ではそんな疑問を解決しつつ、衝撃の事実を明らかにします。

# 衝撃の事実　実はインデックスよりも安全だったレバレッジETF



# まとめ
## レバレッジETFは博打的な投資
インデックスに投資するメリットとしてほぼほぼ無価値化することはありえないことが上げられます。
しかし、見てきた通りレバレッジETFはその可能性が普通にあります。約2割…。

## でもやっぱり利益も多い
しかし、最初にも述べた通り統計的には期待値が正ならレバレッジを効かせるのは期待値を上乗せする意味で理屈上はいいことのはずです。（一時の下がりを気にしない仏の心があれば）
実際今回の検証でも利回りの期待値は参考にしたインデックスに比べ圧倒的です。
NISA枠でも数千万円の利回り狙えるってやばい。

## バブル疑惑
検証内容からは外れますが、アメリカのインデックスはバブルの傾向があるのは明らかな傾向だと思います。
最近の「とりあえずSP500に投資」の流れは仮想通貨にもあった「BTCよく知らないけど買う」に近い流れを感じます。
一つ注意したいのは、*今回の検証もこのバブル傾向に強く影響された検証*です。
ただ、バブルとは言いましたが、本当にバブルかは弾けてみないとわからないのがバブルです。
最近の金融緩和の流れは明らかに歴史上異常なことです。
そのなかで証券の価格が下がるのも確かに難しいかもしれないです。

# 要するに

今回扱った米国インデックスのレバレッジETFは安定して期待値

# 最後に：投資は自己判断で！

長文お読みくださり、ありがとうございました！

# おまけ: 復元抽出で未来をシミュレートする