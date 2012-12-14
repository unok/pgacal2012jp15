.. coding:sjis

==========================================================
複数のバージョンをインストールし, 自由自在に操ろう
==========================================================

:Author: sakamotomsh
:Date: 2012-12-15

.. sectnum::

はじめに
----------

本記事は `PostgreSQL Advent Calender 2012`_ の12/15 用の記事です。
私のgithub上のレポジトリ `pgacal2012jp15`_ を使い,
github:pagesの機能でホスティングしています。

.. _`PostgreSQL Advent Calender 2012`: http://atnd.org/events/34176
.. _`pgacal2012jp15`: https://github.com/sakamotomsh/pgacal2012jp15

目標
---------

- 一つのサーバに,
- 複数のバージョンのPostgreSQLをインストールし,
- 自由自在に切り替えて使う方法を紹介/提案します。

イントロダクション
--------------------

私は某システム会社でPostgreSQLの問い合わせ業務をしています。
問い合わせ業務ではスピードが命です。
問い合わせを受け付けてから環境構築をし, 問題解析をして, 回答をつくり....
そんなことをやっていると時間がいくらあっても足りません。

そんな中, 私や同僚の多くは環境構築の自動化などのテクニックを持っています。  
今日はそのうちの一つとして, 私が使っている **「一つのサーバに複数のPostgreSQL
をインストールし, 自由自在に環境を切り替える方法」** を紹介します。

応用例として **「同期レプリケーションクラスタがとてもに簡単にできること」** 
をデモンストレーションします。

*注記*: 本記事と非常に似た目的のソフトウェアとして pgvm_ があります。 皆さん考えることは一緒ですね..

.. _pgvm: https://github.com/guedes/pgvm


技術的な要素
----------------

- ソースコードの入手
    PostgreSQLは `gitでソースコード管理`_ されています。 そして各バージョンは明解な
    命名規約に基づいたタグ名が付与されています。  そのため, cloneしたローカルの
    gitレポジトリから **「システマティックに」** 任意のバージョンのソースコードを入手できます。

- コンパイル/インストール
    configure時にprefixオプションでインストール先を付与すると, 
    一つのサーバにいくらでもPostgreSQLをインストールすることができます。
    その際に--enable-debugなど解析に役立つオプションをつけることができます。

- 環境の分離/切り替え
    PostgreSQLはインストールしただけでは使えません。
    同居するPostgreSQLどうしの使用するポート番号がかぶらないようにしたり
    適切なPATH設定をして目的のバージョンのpg_ctlを呼び出したり,
    initdbするデータベース領域を確保したりする必要があります。

    一般的な言い方をすると **「環境の切り替え」** が必要となります。
    pythonのvirtualenvでいうactivate, node.jsのnvmにおけるuseに相当する機能です。 
    PostgreSQLの場合, **「基本的に環境変数を設定するだけ」** で環境を分離できます。

    - PATH環境変数: 操作対象のバージョンのpg_ctl/psqlを見つけられるように設定
    - PGDATA環境変数: バージョンごとに違うデータ領域を設定
    - PGPORT環境変数: 同一サーバで動作させた際にポート番号の重複をしないように設
      定(本来はpostgresql.confのportで設定すべきですが, pg_ctlだけでなく
      psqlなどのクライアントアプリケーションが暗黙的に接続するポート番号を
      設定できるというメリットのため環境変数で設定します)

    これらの環境変数をセットしてbashを `exec`_ してあげるプログラムを作るとよさそうです。
    ついでにPS1環境変数をいじってあげて, 現在どのバージョンを使っているかをわかりやすく表示
    するのもよいでしょう。

こうした経緯で, 私が作成したのが二つのプログラム `pginstall`_ と `pgbash`_ です。
前者はインストールを簡略化し, 後者は環境切替を簡略化します。

以下実装を記載しますが, 技術的な部分は以上でカバーしたので,
この先は興味のある方のみ読み進めてください。
また, 自分なりのツールを自作しても面白いと思います。
ぜひチャレンジしてみてください。

.. _`gitでソースコード管理`: http://git.postgresql.org/gitweb/?p=postgresql.git;a=summary
.. _`exec`: http://linuxjm.sourceforge.jp/html/LDP_man-pages/man3/exec.3.html

pginstall: インストール簡略化スクリプト 
-------------------------------------------------

スクリプトの全体は `pginstall`_ に記載しました。 
pythonで作った100行ちょっとのスクリプトです。 
/usr/bin などPATHが通っている場所に配置すると
本当に簡単にPostgreSQLをインストールできます。使い方はこうです

.. code:: bash

    $ pginstall 8.4.12

.. _`pginstall`: https://github.com/sakamotomsh/pgacal2012jp15/blob/master/pginstall
.. _`pgbash`: https://github.com/sakamotomsh/pgacal2012jp15/blob/master/pgbash

中で動くコマンドの動作を少し見てみましょう。

.. code:: bash

    #ソースコードの抽出
    cd /home/pgacal2012jp15/.pgbash/repo
    mkdir /home/pgacal2012jp15/.pgbash/src/pgsql-8.4.12
    git archive REL8_4_12 | tar -x -C /home/pgacal2012jp15/.pgbash/src/pgsql-8.4.12
    
    #コンパイルとインストール
    cd /home/pgacal2012jp15/.pgbash/src/pgsql-8.4.12
    ./configure --prefix=/home/pgacal2012jp15/.pgbash/bin/pgsql-8.4.12 --enable-debug
    make; make install
    cd contrib; make ; make install

つまりgit archiveコマンドでインストール対象のバージョンのソースコードを抜き出し
て, configureする際にprefixを指定してインストールするだけの簡単な作業です。

いくつか補足です。PostgreSQLのレポジトリとして $HOME/.pgbash/repo を使います。
なければgit cloneするよう指示されます。ソースコード, インストールバイナリなど
全てのデータは $HOME/.pgbash 配下に置かれます。

このように一台のマシンに複数のPostgreSQLをインストールするのはとても簡単です。
システマティックにPostgreSQLをインストールできるようになると,
「ちょっと別バージョンで動かしてみるか」と思えるようになります。
**このような心理状態になるのが一番の効能です**.みなさんもぜひ試してみて下さい。


pgbash: 環境切替シェル
-------------------------

スクリプトの全体は `pgbash`_ に記載しました。 
環境切り替えに関しては, 実現するべき機能が複数あります。

- 機能A: どのバージョンが使えるか一覧化する/どのバージョンが起動しているかを表示する
- 機能B: 環境を切り替える(bashをexecする)

機能Aは以下のようにつかいます::

    $ pgbash -l
    [ ] pgsql-8.4.10
    [*] pgsql-8.4.12 (port=18412,port=28412)
    [ ] pgsql-8.4.5
    [ ] pgsql-9.0.2
    [*] pgsql-9.0.7 (port=19007)
    [ ] pgsql-9.1.5
    [ ] pgsql-9.2.0
    [ ] pgsql-9.2.1


この環境では, 結構いろいろなバージョンがインストールされていることがわかります。
ここで[\*]は現在そのバージョンのサーバが起動中であることをあらわします。
Ver8.4.12のインスタンスが2つ, Ver9.0.7のインスタンスが1つあがっているようです。
実はこの表示をするのが大変でした. lsofコマンドでPostgreSQLのドメインソケット一覧と
それを保持しているPIDの対応を基点に, psコマンドでpostmasterのプログラムパスから
どのバージョンがどのポートで動作しているのかを推定しています。

機能Bは, 先ほど述べたように, 環境変数を設定してbashを立ち上げるだけの
プログラムです。 

Ver9.2.1を立ち上げてみます::

    $ pgbash pgsql-9.2.1 
    (pgsql-9.2.1-1)[pgacal2012jp15@~]$ pg_ctl start
    server starting
    (pgsql-9.2.1-1)[pgacal2012jp15@~]$ pgbash -l
    [ ] pgsql-8.4.10
    [*] pgsql-8.4.12 (port=18412,port=28412)
    [ ] pgsql-8.4.5
    [ ] pgsql-9.0.2
    [*] pgsql-9.0.7 (port=19007)
    [ ] pgsql-9.1.5
    [ ] pgsql-9.2.0
    [*] pgsql-9.2.1 (port=19201) ★ここが起動した

このように新たにbashが立ち上がり, pg_ctl などをバージョンを意識せずに打つことが
できます。実際に正しくパスが設定されているか？等を確認してみましょう::

    (pgsql-9.2.1-1)[pgacal2012jp15@~]$ psql -c "select version()"
                                                       version
    --------------------------------------------------------------------------------------------------------------
     PostgreSQL 9.2.1 on x86_64-unknown-linux-gnu, compiled by gcc (GCC) 4.4.6 20120305 (Red Hat 4.4.6-4), 64-bit
    (1 row)
    
    (pgsql-9.2.1-1)[pgacal2012jp15@~]$ which psql
    ~/.pgbash/bin/pgsql-9.2.1/bin/psql
    (pgsql-9.2.1-1)[pgacal2012jp15@~]$ echo $PGDATA $PGPORT
    /home/pgacal2012jp15/.pgbash/data/pgsql-9.2.1-1 19201

このように、バージョンを切り替えてPostgreSQLを思うがままに扱えます。


ミッション: 同期レプリケーションクラスタを構築せよ
----------------------------------------------------------

最近リリースされたPostgreSQLの 9.2.2 を新規にインストールして,
同期レプリケーションをクラスタを組んでみましょう。 
といっても, 以下をこぴぺするだけです。
一杯のコーヒーを飲む時間もなく, クラスタが構築できました

.. code:: bash
    
    TARGET_VERSION=9.2.2
    ENV_ID=pgsql-$TARGET_VERSION

    #Install ##################################################################
    yes | pginstall $TARGET_VERSION

    #Setup Master##############################################################
    pgbash $ENV_ID 1
    rm -rf $PGDATA
    initdb --no-locale -U postgres
    cat << EOF >> $PGDATA/postgresql.conf
    wal_level = hot_standby
    max_wal_senders = 3
    hot_standby = on
    EOF
    cat << EOF >> $PGDATA/pg_hba.conf
    host replication postgres 0.0.0.0/0 trust
    host replication postgres ::1/0 trust
    EOF
    pg_ctl -w start
    pgbench -i
    exit
    
    #Setup Standby############################################################
    pgbash $ENV_ID 2
    pg_basebackup -x -c fast -D $PGDATA -h localhost -p `expr $PGPORT - 10000`
    cat << EOF >> $PGDATA/recovery.conf
    standby_mode = 'on'
    primary_conninfo = 'host=localhost port=`expr $PGPORT - 10000` user=postgres application_name=sby01'
    EOF
    pg_ctl -w start
    exit

    #Start Replication #######################################################
    pgbash $ENV_ID 1
    echo "synchronous_standby_names = '*'" >> $PGDATA/postgresql.conf
    pg_ctl -w restart
    exit

確かめてみます::

    $ pgbash -l
    [ ] pgsql-8.4.10
    [*] pgsql-8.4.12 (port=18412,port=28412)
    [ ] pgsql-8.4.5
    [ ] pgsql-9.0.2
    [*] pgsql-9.0.7 (port=19007)
    [ ] pgsql-9.1.5
    [ ] pgsql-9.2.0
    [*] pgsql-9.2.1 (port=19201)
    [*] pgsql-9.2.2 (port=19202,port=29202)
    
    $ pgbash pgsql-9.2.2
    (pgsql-9.2.2-1)[pgacal2012jp15@~]$ psql -xc "select * from pg_stat_replication"
    -[ RECORD 1 ]----+------------------------------
    pid              | 28019
    usesysid         | 10
    usename          | postgres
    application_name | sby01
    client_addr      | ::1
    client_hostname  |
    client_port      | 43608
    backend_start    | 2012-12-12 00:08:13.220873+09
    state            | streaming
    sent_location    | 0/4000080
    write_location   | 0/4000080
    flush_location   | 0/4000080
    replay_location  | 0/4000080
    sync_priority    | 1
    sync_state       | sync

最後に
----------
ルーチンを定型化/自動化することでこころにゆとりが生まれます。
生まれたゆとりで, 真の意味で生産性が求められることに心を使いましょう。

明日12/16はyohgakiさんです.


.. vim: tw=80 :
