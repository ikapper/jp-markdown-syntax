Markdown: Syntax
================

*   [概要](#overview)
    *   [哲学](#philosophy)
    *   [インラインHTML](#html)
    *   [特殊文字の自動エスケープ](#autoescape)
*   [ブロック要素](#block)
    *   [段落と改行](#p)
    *   [ヘッダー](#header)
    *   [ブロッククォート](#blockquote)
    *   [リスト](#list)
    *   [コードブロック](#precode)
    *   [水平方向の罫線](#hr)
*   [インライン要素](#span)
    *   [リンク](#link)
    *   [強調表現](#em)
    *   [コード](#code)
    *   [イメージ](#img)
*   [その他](#misc)
    *   [バックスラッシュエスケープ](#backslash)
    *   [自動リンク生成](#autolink)

* * *

<h2 id="overview">概要</h2>

<h3 id="philosophy">哲学</h3>

Markdownは、実行可能で読みやすく書きやすいように意図されています。

しかし、可読性は何にも増して重要視されるものです。Markdownの文書は、タグや整形命令でマークアップされることなく、そのままの形、プレーンテキストの形で公開可能になるべきです。Markdownの構文は、[Setext][1]や[atx][2]、[Textile][3]、[reStructuredText][4]、[Grutatext][5]、[EtText][6]を含めた、幾つかのテキストをHTMLに変換するフィルタに影響を受けていますが、Markdownの構文のための最も大きな単一の発想の源は、プレーンテキストのEmailのフォーマットです。

[1]: http://docutils.sourceforge.net/mirror/setext.html
[2]: http://www.aaronsw.com/2002/atx/
[3]: http://textism.com/tools/textile/
[4]: http://docutils.sourceforge.net/rst.html
[5]: http://www.triptico.com/software/grutatxt.html
[6]: http://ettext.taint.org/doc/

この目標のために、Markdownの構文は、ほとんどが区切り文字から構成されています。それらの文字は、それらが意味することがわかるように選ばれています。例えば、単語を囲んだアスタリスクは実際に\*強調\*のように見えます。Markdownでは、まあ、そのように表示します。ブロッククォートでさえ、Emailで使ったと思いますが、テキストの引用節のように見えます。


<h3 id="html">インラインHTML</h3>
 
Markdownの構文は、Webを*書く*ための記述形式として使われるという1つの目的のために作成されたものです。

MarkdownはHTMLを置き換えるものでもそれに近づこうとするものでもありません。その構文はとても小さく、HTMLタグのごく一部だけと対応しています。そのアイディアはHTMLタグの挿入を簡単にする構文を作ることではありません。わたしの見解では、HTMLタグは挿入するのはすでに容易です。Markdownのアイディアは散文の読み書き編集を簡単にするものです。HTMLは*公表する*形式ですが、Markdownは*書く*形式です。したがって、Markdownの構文形式は、プレーンテキストで伝えられる問題だけに専念します。

Markdownの構文でカバーできないマークアップについては、単純にHTMLそのものを使用します。そこには、あなたがMarkdownからHTMLに切り替えたことを示すための宣言や境界は必要ありません。すなわち、シンプルにタグを使用します。

`<div>`や`<table>`,`<pre>`,`<p>`などのブロックレベルのHTML要素には制限があります。それらは、空行によって内容を分割しなければならず、ブロックの開始と終了タグはタブやスペースでインデントすべきではありません。MarkdownはHTMLのブロックレベルのタグを囲む余分な（予期しない）`<p>`タグを付加するほどスマートではありません。

例えば、Markdownの記事にテーブルを加えるには、以下のようにします。:

    これは通常の段落です。

    <table>
        <tr>
            <td>Foo</td>
        </tr>
    </table>

    これはまた別の通常の段落です。

Markdownの構文形式はブロックレベルのHTMLタグの内側を処理しないことに注意してください。例えば、HTMLブロックの内側でMarkdownのスタイルである`*強調*`を使うことはできません。

`<span>`や`<cite>`,`<del>`などのインラインレベルのHTMLタグは、リストアイテムやヘッダー、Markdownの段落のどこにでも使用することができます。しようと思えば、Markdownの形式の代わりにHTMLタグを使用することさえできます。例えば、あなたが、Markdownのリンクやイメージの構文の代わりに`<a>`や`<img>`のHTMLタグが使うのが好きであれば、そのままどうぞ。

ブロックレベルのHTMLタグと違い、Markdownの構文はインラインレベルのタグの内側を処理*します*。


<h3 id="autoescape">特殊文字の自動エスケープ</h3>

HTMLでは、特別な扱いが要求される文字が2つあります。すなわち、`<`と`&`です。左山形かっこはタグの開始に使用され、アンパサンドはHTMLの実体を示すために使用されます。それらをそのままの文字として使用したいときは、`&lt;`や`&amp;`のように実体としてエスケープしなければなりません。

実際にアンパサンドはWebライターたちを悩ませています。もし、あなたが'AT&T'と記述したいならば、'`AT&amp;T`'と記述する必要があります。URLの記述でアンパサンドをエスケープする必要さえあります。したがって、以下にリンクしたいときは、:

    http://images.google.com/images?num=30&q=larry+bird

次のようにURLをエンコードする必要があります。:

    http://images.google.com/images?num=30&amp;q=larry+bird

アンカータグの`href`属性をこのようにする必要があります。言うまでもなく、これは忘れがちなものですし、うまくマークアップされたWebサイトでのまさに最も多いHTMLのバリデーションエラーの原因かもしれません。

Markdownでは、あなたがしなければならないエスケープの手間をかけることなく、これらの文字を自然に使用できます。アンパサンドをHTMLの実体の一部として使用すれば、変化しないままになります。そうでなければ、`&amp;`に変換されるでしょう。

ですので、自分の記事の中にコピーライトのシンボルを含めたいときは、:

    &copy;

として、書くことができ、Markdownはそれをそのままにします。しかし、もし、:

    AT&T

と書くと、Markdownは、:

    AT&amp;T

と変換するでしょう。なぜなら、Markdownは[インラインHTML](#html)をサポートしているので、HTMLタグのためにデリミターとして山形かっこを使うと、Markdownはそれらをそのように扱うでしょう。しかし、もし、

    4 < 5

と書くと、Markdownは、

    4 &lt; 5

と、変換します。Markdownのコードのインラインやブロックの内側では、山形かっことアンパサンドは*いつも*自動的にエンコードされます。これによりHTMLコードについて書くためにMarkdownを使うことが簡単になります。（そのままのHTMLとは対照的です。単一の`<`や`&`ごとにエスケープの必要があるため、それはHTML構文を書くにはぞっとする形式です。）


* * *

<h2 id="block">ブロック要素</h2>

<h3 id="p">段落と改行</h3>

1つの段落とは、1つ以上の空行で分けられている1つ以上の連続した文章の行です。（1つの空行とは、スペースやタブ文字の他は何も含まれていない行、つまり余白に見える行のことです。）通常の段落はスペースやタブ文字でインデントすべきではありません。

"1つ以上の連続した文章の行"というルールの含意は、Markdownは"ハードラップした"文章の段落をサポートしているということです。これは、段落中の改行文字すべてを`<br />`に変換する他のほとんどの文章をHTMLにするフォーマッター（"改行文字を変換"オプションを含む）とは、大きく異なります。

あなたがMarkdownで`<br />`タグを挿入したいときは、末尾に2つ以上の空白を空けて改行します。

そう、`<br />`を作成するにはちょっとだけ手間が要ります。しかし、安易な"改行はいつも`<br />`"ルールをMarkdownでは気にしなくて済みます。あなたが強制改行によりフォーマットするとき、MarkdownのEmailスタイル[ブロッククォート][bq]や複数段落の[リストアイテム][l]は最もうまくいきますし、見た目も良いです。

  [bq]: #blockquote
  [l]: #list


<h3 id="header">ヘッダー</h3>

Markdownは、[Setext][1]と[atx][2]の2つのヘッダースタイルをサポートしています。

Setextスタイルのヘッダーは、（ファーストレベルのヘッダーには）イコールサインと（セカンドレベルのヘッダーには）ダッシュを使って"アンダーライン"されます。例えば、:

    This is an H1
    =============

    This is an H2
    -------------

`＝`と`-`のアンダーラインの数は任意です。
 
atxスタイルのヘッダーは、1から6のヘッダーレベルに対応した、1つから6つのハッシュ文字を行頭に使います。例えば、:

    # This is an H1

    ## This is an H2

    ###### This is an H6

任意で、atxスタイルヘッダーは"閉じて"も良いです。これは純粋に見た目のためです。すなわち、あなたがその方が見栄えがいいと思うなら、これを使うことができます。閉じるときのハッシュは、開始時のハッシュの数と一致する必要さえありません。（開始時のハッシュの数が、ヘッダーレベルを決定します。）:

    # This is an H1 #

    ## This is an H2 ##

    ### This is an H3 ######


<h3 id="blockquote">ブロッククォート</h3>

Markdownは、ブロッククォートにはEmailのスタイルである`>`文字を使用します。もしあなたがEmailのテキストにある引用節に馴染みがあれば、あなたはMarkdownでブロッククォートを作る方法を知っています。文章の各行の行頭に`>`を設置すればうまくいきます。:

    > This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
    > consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
    > Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
    > 
    > Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
    > id sem consectetuer libero luctus adipiscing.

Markdownでは、あなたは引用部分にしたい段落の最初の行の行頭だけに`>`を置けばいいので、楽ができます。:

    > これは2段落のブロッククォートです。Lorem ipsum dolor sit amet,
    consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
    Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

    > Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
    id sem consectetuer libero luctus adipiscing.

ブロッククォートは、`>`の階層を追加することで、ネストすること（ブロッククォートの中にブロッククォートを入れること）ができます。

    > これはクォートのファーストレベルです。
    >
    > > これはネストされたブロッククォートです。
    >
    > ファーストレベルに戻ります。
 
ブロッククォートは、ヘッダーやリスト、コードブロックを含めた他のMarkdownの要素を含めることができます。:

    > ## This is a header.
    > 
    > 1.   This is the first list item.
    > 2.   This is the second list item.
    > 
    > Here's some example code:
    > 
    >     return shell_exec("echo $input | $markdown_script");

大方のテキストエディタはEmailスタイルのクォートは簡単なはずです。例えば、BBEditでは選択範囲を指定して、テキストメニューから引用レベルを上げるを選択すればできます。


<h3 id="list">リスト</h3>

Markdownは番号付きリストと番号なしリストをサポートしています。

番号なしリストはリストマーカーとしてアスタリスクとプラス、ハイフンのいずれかを使用します。:

    *   Red
    *   Green
    *   Blue
  
は、以下の2つと等価になります。:

    +   Red
    +   Green
    +   Blue

と、

    -   Red
    -   Green
    -   Blue

番号付きリストは後ろにピリオドを伴った数字を使用します。:

    1.  Bird
    2.  McHale
    3.  Parish
  
リストをマークするのに使用する実際の数字は、Markdownが生成するHTMLの出力には影響を及ぼさないことに注意することが重要です。Markdownが上のリストから生成するHTMLは、以下のようになります。:

    <ol>
    <li>Bird</li>
    <li>McHale</li>
    <li>Parish</li>
    </ol>

それどころかMarkdownでのリストを以下のように書いたり、:

    1.  Bird
    1.  McHale
    1.  Parish

または、:

    3. Bird
    1. McHale
    8. Parish
 
とすると、全く同じHTMLの出力を得られます。ポイントは、もし望むのであれば、順序付けられたMarkdownのリストで順序付けられた数を使うと、ソースでの数字は発行するHTMLでの数字と一致するということです。しかし、面倒なら、その必要はありません。

しかし、適当なリストのナンバリングを使用すると、やはりリストは1からスタートします。今後の幾つかのポイントで、Markdownは任意の数字でスタートする番号付きリストをサポートするかもしれません。

リストマーカーは概ね左マージンで始まりますが、3つまでのスペースでインデントされるかもしれません。リストマーカーには1つか2つのスペースか、1つのタブ文字が続きます。

リストの見た目を良くするために、インデントを下げてアイテムをラップすることができます。:

    *   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
        Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
        viverra nec, fringilla in, laoreet vitae, risus.
    *   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
        Suspendisse id sem consectetuer libero luctus adipiscing.

面倒であればする必要はありません。:

    *   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
    Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
    viverra nec, fringilla in, laoreet vitae, risus.
    *   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
    Suspendisse id sem consectetuer libero luctus adipiscing.

リストアイテムが空行で分けられているならば、Markdownは`<p>`タグでアイテムをラップしてHTMLに出力します。例えば、この入力は、:

    *   Bird
    *   Magic

次のようになります。:

    <ul>
    <li>Bird</li>
    <li>Magic</li>
    </ul>

しかし、これは:

    *   Bird

    *   Magic

次のようになります。:

    <ul>
    <li><p>Bird</p></li>
    <li><p>Magic</p></li>
    </ul>

リストアイテムが複数の段落から成ることができます。リストアイテムの中で、それぞれに続く段落は、4つのスペースか、1つのタブ文字でインデントされなければいけません。:

    1.  これは2つの段落のリストアイテムです。Lorem ipsum dolor
        sit amet, consectetuer adipiscing elit. Aliquam hendrerit
        mi posuere lectus.

        Vestibulum enim wisi, viverra nec, fringilla in, laoreet
        vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
        sit amet velit.

    2.  Suspendisse id sem consectetuer libero luctus adipiscing.
  
次の段落の行ごとにインデントすれば、見た目は良くなりますが、ここでまた、Markdownにより、怠けることができます。:

    *   これは2つの段落のリストアイテムです。

        これは2番目の段落です。この2番目の段落中では、
    あなたは、最初の行だけインデントする必要
    があります。
    Lorem ipsum dolor
    sit amet, consectetuer adipiscing elit.

    *   同じリストの他のアイテム

リストアイテム中でブロッククォートを入れるためには、ブロッククォートの`>`区切り文字はインデントする必要があります。:

    *   ブロッククォート付きリストアイテム:

        > これは、リストアイテムの中の
        > ブロッククォートです。

リストアイテム中でコードブロックを入れるためには、コードブロックは*2倍*、すなわち8つのスペースか、2つのタブ文字でインデントする必要があります。:

    *   コードブロック付きリストアイテム:

            <code goes here>

次のように記述して、偶然番号付きリストを生成してしまう可能性があることに注意する必要があります。:

    1986. What a great season.

言い換えれば、行頭の1つの*数字-ピリオド-スペース*の流れのことです。この回避策として、ピリオドをバックスラッシュでエスケープできます。:

    1986\. What a great season.


<h3 id="precode">コードブロック</h3>

整形済みのコードブロックはプログラムやマークアップのソースコードを書くために使われます。通常の段落で整形するよりも、正確にコードブロックの行は解釈されます。Markdownは`<pre>`と`<code>`タグの両方でコードブロックをラップします。

Markdownでコードブロックを生成するために、単純に少なくとも4つのスペースか、1つのタブ文字でブロックの各行をインデントしてください。例えば、次の入力を与えると、:

    これは通常の段落です:

        これはコードブロックです。

Markdownは次を生成します。:

    <p>これは通常の段落です:</p>

    <pre><code>これはコードブロックです。
    </code></pre>

インデントの1レベルである、4つのスペースか1つのタブ文字は、コードブロックの各行から除去されます。例えば、以下は、:

    Here is an example of AppleScript:

        tell application "Foo"
            beep
        end tell

次のようになります。:

    <p>Here is an example of AppleScript:</p>

    <pre><code>tell application "Foo"
        beep
    end tell
    </code></pre>

1つのコードブロックは、インデントされていない行（あるいは記事の終わり）まで続きます。

コードブロックの内側では、アンパサンド(`&`)と山形かっこ(`<`と`>`)は自動的にHTMLの実体に変換されます。これにより、ペーストしたりインデントするだけのMarkdownを使ってHTMLのサンプルコードを含めるのがとても簡単になり、Markdownは、アンパサンドと山形かっこのエンコーディングの厄介ごとを引き受けてくれます。例えば、次の:

        <div class="footer">
            &copy; 2004 Foo Corporation
        </div>

は、次のようになります。:

    <pre><code>&lt;div class="footer"&gt;
        &amp;copy; 2004 Foo Corporation
    &lt;/div&gt;
    </code></pre>

標準のMarkdownの構文はコードブロックの内側では処理されません。例えば、アスタリスクはコードブロック内では文字どおりのアスタリスクになります。これは、Markdownの構文を書くためにMarkdown自身を使用することが簡単であることも意味しています。


<h3 id="hr">水平方向の罫線</h3>

3つ以上のハイフンやアスタリスク、アンダースコアを一列に置くことによって、水平罫線タグ`<hr />`を生成することができます。したいのであれば、ハイフンやアスタリスクの間にスペースを使うことができます。次の各行は水平罫線を生成します。:

    * * *

    ***

    *****

    - - -

    ---------------------------------------


* * *

<h2 id="span">インライン要素</h2>

<h3 id="link">リンク</h3>

Markdownは、*インライン*と*リファレンス*の2つのリンクのスタイルをサポートしています。

どちらのスタイルでも、リンクテキストは、[角かっこ]により区切られます。

インラインリンクを生成するためには、リンクテキストの閉じ角かっこの直後に通常の丸かっこを使います。丸かっこの内側には、 クォートで囲った*任意の*リンクのタイトルと一緒に、リンクさせたいURLを設置してください。例えば、:

    This is [an example](http://example.com/ "Title") inline link.

    [This link](http://example.net/) has no title attribute.
  
は、以下を生成します。:

    <p>This is <a href="http://example.com/" title="Title">
    an example</a> inline link.</p>

    <p><a href="http://example.net/">This link</a> has no
    title attribute.</p>

同じサーバーのローカルリソースを参照したければ、相対パスを用いることができます。:

    See my [About](/about/) page for details.

リファレンススタイルのリンクは2つ目の角かっこのセットを使用し、その内側には、リンクを識別するためのラベルを設置します。:

    This is [an example][id] reference-style link.

任意で2つの角かっこの間にスペースを使うことができます。:

    This is [an example] [id] reference-style link.

それから、文書のどこかに、次のようにリンクラベルを定義すると、リンクが生成されます。:

    [id]: http://example.com/ "Optional Title Here"

すなわち、:

* （任意の3つまでのスペースを使って左からインデントされた）リンクの識別子を含んでいる角かっこに、
* 後ろにコロンが続き、
* さらに1つ以上のスペースか、タブ文字が続き、
* さらにリンク先のURLが続き、
* 最後に、任意の、ダブルかシングルクォートか丸かっこで囲まれたリンクのtitle属性が続きます。

次のリンクの定義は等価になります。:

    [foo]: http://example.com/  "Optional Title Here"
    [foo]: http://example.com/  'Optional Title Here'
    [foo]: http://example.com/  (Optional Title Here)

**注意:** Markdown.plのバージョン1.0.1では、シングルクォートがリンクタイトルの識別に使われるのを妨げてしまう既知のバグがあります。

次のように、リンクURLは任意で、山形かっこで囲うこともできます。:

    [id]: <http://example.com/>  "Optional Title Here"

次の行に、パディングのために追加のスペースやタブ文字を使ってタイトル属性を置くこともできます。それにより、長めのURLの時の見た目をより良くできます。:

    [id]: http://example.com/longish/path/to/resource/here
        "Optional Title Here"

リンク定義は、Markdownの処理中にリンクを生成するためだけに使われ、HTMLの出力では文書から取り除かれます。

リンク定義名は、文字と数字、句読点を含みますが、大文字小文字を*区別しません*。例えば、次の2つのリンク定義は、:

    [link text][a]
    [link text][A]

等価です。

*暗黙的なリンク名*のショートカットにより、リンク名を省くことができ、このケースでは、リンクテキスト自身はリンク名としても使われます。単に空にした角かっこを使用します。例えば、"Google"という単語をgoogle.comのウェブサイトとリンクするためには、単純に次のように記述します。:

    [Google][]

そして、リンクを定義します。:

    [Google]: http://google.com/

リンク名はスペースを含むことができるので、このリンクはリンクテキスト内の複数ワードにまたがって有効になります。:

    Visit [Daring Fireball][] for more information.

そして、リンクも定義します。:

    [Daring Fireball]: http://daringfireball.net/

リンク定義はMarkdownの文書内のどこにでも書くことができます。私はよく、それぞれの使った段落の直後にそれらを書きますが、したければ、文書の最後にすべて書いて、脚注の一種のようにできます。

以下に実際のリファレンスのリンクの例を示します。:

    I get 10 times more traffic from [Google] [1] than from
    [Yahoo] [2] or [MSN] [3].

    [1]: http://google.com/        "Google"
    [2]: http://search.yahoo.com/  "Yahoo Search"
    [3]: http://search.msn.com/    "MSN Search"

暗黙的なリンク名のショートカットも使用できるので、代わりに以下のようにもかけます。:

    I get 10 times more traffic from [Google][] than from
    [Yahoo][] or [MSN][].

    [google]: http://google.com/        "Google"
    [yahoo]:  http://search.yahoo.com/  "Yahoo Search"
    [msn]:    http://search.msn.com/    "MSN Search"

上の2つの例はともに次のHTMLを出力します。:

    <p>I get 10 times more traffic from <a href="http://google.com/"
    title="Google">Google</a> than from
    <a href="http://search.yahoo.com/" title="Yahoo Search">Yahoo</a>
    or <a href="http://search.msn.com/" title="MSN Search">MSN</a>.</p>

比較のため、ここでは、同じ節をMarkdownのインラインリンクのスタイルで書いてみます。:

    I get 10 times more traffic from [Google](http://google.com/ "Google")
    than from [Yahoo](http://search.yahoo.com/ "Yahoo Search") or
    [MSN](http://search.msn.com/ "MSN Search").

リファレンススタイルのリンクのポイントは書きやすくする事ではありません。そのポイントは、リファレンススタイルのリンクによって、文書がはるかに読みやすくなるということです。上の例を比較すると、リファレンススタイルの場合は節の長さは81文字でしかありません。一方で、インラインスタイルでは、176文字です。そのままのHTMLで書くと、234文字になります。HTMLでは、テキストより多くのマークアップが存在しています。

Markdownのリファレンススタイルのリンクを使うと、ソースの文書はなおさら、ブラウザでレンダリングするときの最終的な出力に似てきます。マークアップに関連したメタデータを段落の外に移動させられることにより、話の流れを遮ることなくリンクを追加することができます。


<h3 id="em">強調表現</h3>

Markdownは、アスタリスク(`*`)やアンダースコア(`_`)を強調表現の指標として扱います。1つの`*`や`_`でラップされたテキストは、`<em>`タグとしてラップされ、2つの`*`や`_`でラップされたものは、`<strong>`タグでラップされます。例えば、次の入力は、:

    *single asterisks*

    _single underscores_

    **double asterisks**

    __double underscores__

次を生成します。:

    <em>single asterisks</em>

    <em>single underscores</em>

    <strong>double asterisks</strong>

    <strong>double underscores</strong>

あなたの好きなスタイルを使用することができます。その唯一の制限は、強調部分の開始と終了は同じ文字を使用しなければならないことです。

強調は単語の中でも使用できます。:

    un*frigging*believable

しかし、スペースで`*`や`_`を囲むならば、それは文字通りのアスタリスクやアンダースコアとして扱われます。

他の方法で強調の区切り文字として使用する位置で、文字通りのアスタリスクやアンダースコアを生成するためには、バックスラッシュでそれをエスケープできます。:

    \*このテキストはアスタリスクで囲まれます\*


<h3 id="code">コード</h3>

インラインのコードを示すためには、バックティッククォート（`` ` ``）でラップします。整形済みのコードブロックと異なり、インラインのコードは通常の段落中でコードを示します。例えば、次は:

    Use the `printf()` function.
  
以下を生成します。:

    <p>Use the <code>printf()</code> function.</p>

インラインのコードの内側に文字通りのバックティックを含めるために、開始と終了の区切り文字として複数のバックティックを使用できます。:

    ``There is a literal backtick (`) here.``

上は以下を生成します。:

    <p><code>There is a literal backtick (`) here.</code></p>

インラインのコードを囲むバックティックの区切り文字は、開いた後に1つ、閉じる前に1つのスペースを含めることができます。これにより、インラインのコードの開始時と終了直前に文字通りのバックティック文字を置くことができます。:

    A single backtick in a code span: `` ` ``

    A backtick-delimited string in a code span: `` `foo` ``
  
は、以下を生成します。:

    <p>A single backtick in a code span: <code>`</code></p>

    <p>A backtick-delimited string in a code span: <code>`foo`</code></p>

インラインのコードでは、アンパサンドと山形かっこは自動的にHTMLの実体にエンコードされます。それにより、HTMLタグなどを含めやすくなります。Markdownは、以下を、:

    Please don't use any `<blink>` tags.

次のように変換します。:

    <p>Please don't use any <code>&lt;blink&gt;</code> tags.</p>

このように書くことができ、:

    `&#8212;` is the decimal-encoded equivalent of `&mdash;`.

は、以下を生成します。:

    <p><code>&amp;#8212;</code> is the decimal-encoded
    equivalent of <code>&amp;mdash;</code>.</p>


<h3 id="img">イメージ</h3>

広く知られているように、プレーンテキストの文書の形式にイメージを配置するための"自然な"構文を工夫するのは、結構難しいです。

Markdownは、リンクの構文と似たイメージの構文を使用します。つまり、*インライン*と*リファレンス*の2つのスタイルです。

インラインのイメージ構文は次のようになります。:

    ![Alt text](/path/to/img.jpg)

    ![Alt text](/path/to/img.jpg "Optional title")

すなわち、:

* 1つのエクスクラメーションマーク（`!`）に、
* イメージの代わりとなる`alt`属性のテキストを含んだ、山形かっこが後ろに続き、
* さらに、イメージのURLかパスを含んだ、丸かっこが続きます。（任意で、ダブルかシングルクォートで囲んだ`title`属性を挿入できます。）

リファレンススタイルのイメージ構文は次のようになります。:

    ![Alt text][id]

idは定義されたイメージのリファレンスの名前になります。イメージのリファレンスは、リンクのリファレンスと全く同じ構文で定義されます。: 

    [id]: url/to/image  "Optional title attribute"

現時点で、Markdownには、イメージの大きさを指定する構文はありません。指定したいときは、単に通常の`<img>`タグを使うことができます。


* * *

<h2 id="misc">その他</h2>

<h3 id="autolink">自動リンク生成</h3>

Markdownは、URLやEmailアドレスのリンクを"自動"で生成するためのショートカットスタイルをサポートしています。それは単純にURLやEmailアドレスを山形かっこで囲むものです。これが意味することは、実際のURLやEmailアドレスのテキストを示したり、クリック可能なリンクにしたいならば、次のように施せばいいということです。:

    <http://example.com/>

Markdownは以下のように変換します。:

    <a href="http://example.com/">http://example.com/</a>

自動リンクは、Emailアドレスにも同様に動作します。ただし、Markdownが、アドレスを収集するスパムボットから分かりにくくするのを支援するために、ランダム化された10進法と16進法の実体エンコードを少し実行します。例えば、Markdownは以下を、:

    <address@example.com>

次のようなものに変換します。:

    <a href="&#x6D;&#x61;i&#x6C;&#x74;&#x6F;:&#x61;&#x64;&#x64;&#x72;&#x65;
    &#115;&#115;&#64;&#101;&#120;&#x61;&#109;&#x70;&#x6C;e&#x2E;&#99;&#111;
    &#109;">&#x61;&#x64;&#x64;&#x72;&#x65;&#115;&#115;&#64;&#101;&#120;&#x61;
    &#109;&#x70;&#x6C;e&#x2E;&#99;&#111;&#109;</a>

これは、ブラウザでは"address@example.com"へのクリック可能なリンクとして、表現されます。

（この種の実体エンコードのトリックは実際に、アドレス収集ボットのほとんどではなくとも、多くのものを騙すことができるでしょう。しかし、それら全てがはっきりと騙せるとは限りません。何もしないよりは良いということですが、この方法で公開されるアドレスは、おそらく、最終的にはスパムを受け取り始めるでしょう。）


<h3 id="backslash">バックスラッシュエスケープ</h3>

Markdownでは、その構文形式のための特殊な意味以外のそのまま文字通りの文字を生成するために、バックスラッシュエスケープが使用できます。例えば、（`<em>`タグの代わりに）文字通りのアスタリスクで単語を囲みたいならば、このように、アスタリスクの前にバックスラッシュを使用できます。:

    \*literal asterisks\*

Markdownは、次のような文字でのエスケープを提供しています。:

    \   backslash           バックスラッシュ
    `   backtick            バックティック
    *   asterisk            アスタリスク
    _   underscore          アンダースコア
    {}  curly braces        波かっこ
    []  square brackets     角かっこ
    ()  parentheses         丸かっこ
    #   hash mark           ハッシュ
    +   plus sign           プラス
    -   minus sign (hyphen) マイナス（ハイフン）
    .   dot                 ドット
    !   exclamation mark    エクスクラメーションマーク
