# unbound_adblokinglists

AdBlocking-Lists for Unbound.  

# Description

Unbound用の日本向け(+α)の広告ブロックリストです。  
Unboundでは、設定ファイルにて以下のような記述をするとNXDOMAINを返答するため、DNSによる広告ブロックを実現できます。

    local-zone: "googleadservices.com." static

そこで、`/etc/hosts`用として提供されている広告ブロックリストをUnbound用に変換しました。
元の広告ブロックリストを以下に示すと共に、配信者に敬意を表します。

- https://adaway.org/hosts.txt
- https://github.com/multiverse2011/adawaylist-jp
- https://sites.google.com/site/hosts2ch/ja
- https://logroid.github.io/blogger/file/hosts.txt
- https://warui.intaa.net/adhosts/hosts_lb.txt
- http://winhelp2002.mvps.org/hosts.txt

# Usage

[blocking](./blocking/)以下に広告ブロックリストがあるので、これを`include`してください。  
設定内容は[unbound.conf.example](./unbound.conf.example)を参考にしてください。

# How to make AdBlocking-List for Unbound

vimでの操作を記述します。  
まず、`127.0.0.1 localhost`等の関係ない行を削除してください。次に、コメント行と空行を削除します。

    :g/#/d
    :v/./d

次に、`127.0.0.1 `や`0.0.0.0 `を`local-zone: "`に置換します。この説明では`127.0.0.1 `とします。

    :%s/127.0.0.1 /local-zone: \"/g

次に全行の末尾に`." static`を追記します。

    gg
    Ctrl-V
    Shift-G
    $
    Shift-A
    ." static
    Esc

以上です。
[blocking](./blocking/)以下にある広告ブロックリストはこの方法で作成しました。

また、[280blocker.net](https://280blocker.net/download/)の
[広告ドメインリスト](https://280blocker.net/files/280blocker_domain.txt)も
ほぼ同様の方法で使用できます。
`Adawayや、hosts形式に使えるファイルは現在ありません。（上記ファイルを変換して使用しても広告のすり抜けが大量に発生します。）`
との記述がありますが、使ってみるとそれなりに使えているので、私は有り難く使わせていただいています。
ライセンスの関係で改変物を公開できないので、以下に作成方法を記します。

まず、配布されているファイルは改行コード等が変なので、直接ダウンロードして使うのではなく
ブラウザなどで開いてエディタにコピー&ペーストして使うことをお勧めします。

あとは同様に改変すればいいのですが、このリストは`/etc/hosts`用ではないので
`127.0.0.1 `等の記述がないため、置換する工程を全行の先頭に追加する工程に変更してください。
操作は以下の通りです。

    gg
    Ctrl-V
    Shift-G
    Shift-I
    local-zone: "
    Esc

以上です。
