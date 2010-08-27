# ap_dark8

<a href="http://www.flickr.com/photos/36836508@N02/4931578715/" title="ap_dark8 by apribase, on Flickr"><img src="http://farm5.static.flickr.com/4100/4931578715_bce275f211.jpg" width="500" height="313" alt="ap_dark8" /></a>

ap_dark8 は 8色しか色を扱えない Mac Terminal.app のために作成した色設定です。
<a href="http://visor.binaryage.com/">Visor</a> がないと生きていけないので作成しました。

## 目的

「Visor + tmux + vim で ssh 先でも快適にプログラミング」をコンセプトに。

代替案として iTerm や urxvt で Visor のような振る舞いをする設定や、sshfs + MacVim (フルカラー) でテキスト編集するなどの方法を模索しましたが、どこかで妥協する必要はあり、「そもそも256色使えたとしてほんとうに使うのか？」と冷静になった後、8色でそれなりに満足できる設定を作ろうと思ったのが経緯です。

Terminal.app の色変更には <a href="http://niw.at/articles/2007/11/02/TerminalColoreopard/ja" title="TerminalColoreopard">TerminalColoreopard</a> を使用しています。

ターミナルそのものの描画能力、TERMINFO の情報、tmux や screen 等のマルチプレクサの描画能力、いろいろな環境から接続される ssh サーバのための分岐設定。
ターミナル生活は悩ましいですね。

## Terminal.app に色設定を追加する

<a href="http://www.flickr.com/photos/36836508@N02/4931578877/" title="Mac Terminal 設定 by apribase, on Flickr"><img src="http://farm5.static.flickr.com/4116/4931578877_7c08b95da1.jpg" width="500" height="380" alt="Mac Terminal 設定" /></a>

<a href="http://github.com/apribase/ap_dark8/blob/master/Visor_AP_Dark8.terminal" title="Visor_AP_Dark8.terminal">Visor_AP_Dark8.terminal</a> は Mac Terminal.app の設定をエクスポートしたファイルです。
<a href="http://github.com/apribase/ap_dark8/blob/master/Visor_AP_Dark8.terminal">Visor_AP_Dark8.terminal</a> をダブルクリックすると Visor_AP_Dark8 が Terminal.app の設定に追加されます。

<a href="http://visor.binaryage.com/">Visor</a> を使用する場合、読み込み設定は自動的に Visor が選択されるため、Visor_AP_Dark8 の名前を Visor に置き換えてください。

## .vim/color に色設定を追加する

<a href="http://www.flickr.com/photos/36836508@N02/4931710837/" title="ap_black8.vim by apribase, on Flickr"><img src="http://farm5.static.flickr.com/4074/4931710837_fd427cb57d.jpg" width="500" height="310" alt="ap_black8.vim" /></a>

<a href="http://github.com/apribase/ap_dark8/blob/master/ap_dark8.vim" title="ap_dark8.vim">ap_dark8.vim</a> は vim 向けの色設定ファイルです。
通常の vim 色設定ファイルと同じように $HOME/.vim/color/ap_dark8.vim に置くことで使用できます。

<a href="http://blog.infinitered.com/entries/show/8" title="ir_black">ir_black.vim</a> をベースに、明るすぎる色を抑えるために <a href="http://d.hatena.ne.jp/y_yanbe/20070904/1188911217">inkpot16.vim</a> の色を参考にしました。
BOLD 指定がいくつか残っていますが、BOLD は使っていません。
また、色はすべて dark から始まる基本8色のみを使っているため、bright color は使用していません。

## (余談) 256色描画可能なターミナルについて

<a href="http://www.flickr.com/photos/36836508@N02/4931623821/" title="iTerm 256colors2.pl by apribase, on Flickr"><img src="http://farm5.static.flickr.com/4137/4931623821_774d413a08.jpg" width="500" height="266" alt="iTerm 256colors2.pl" /></a>

Mac では iTerm や urxvt (256色パッチ適用) で256色描画が可能です。
しかし Visor は Terminal.app にしか適用できませんし、urxvt では日本語入力環境を X に用意する必要があります。

Linux では gnome-terminal, konsole, urxvt (256色パッチ適用) で256色描画が可能です。
Visor のようなドロップダウンターミナルとして Guake や Yakuake が存在しますが、色の設定が行いにくいです。

<a href="http://www.flickr.com/photos/36836508@N02/4932216282/" title="Visor (Terminal.app) 256colors2.pl by apribase, on Flickr"><img src="http://farm5.static.flickr.com/4077/4932216282_ef61f9fb3c.jpg" width="500" height="263" alt="Visor (Terminal.app) 256colors2.pl" /></a>

Terminal.app は8色 (ボールドテキストに対して明るめの色を設定した場合16色) しか扱うことができません。
Visor も Terminal.app を使用するため同様です。

## (余談) terminfo について

<a href="http://www.flickr.com/photos/36836508@N02/4932276836/" title="tput colors by apribase, on Flickr"><img src="http://farm5.static.flickr.com/4134/4932276836_e2934df156.jpg" width="378" height="233" alt="tput colors" /></a>

terminfo はターミナルの能力に関する情報です。
tput colors コマンドで確認することができます。
256色描画が可能なターミナル (たとえば gnome-terminal) であっても、最初は8を返す設定 (TERM=xterm) になっている場合が多いです。
描画自体は terminfo に関係なく可能であるため、256color.pl で確認することができます。
しかし、vim などのアプリケーションに「256色描画が可能である」という情報を伝えるために terminfo が使用されます。

ssh 接続した場合、ssh 先に terminfo が存在しないこともあります。
たとえば Debian サーバの場合、ncurses-base パッケージによく使われる terminfo が、その他は ncurses-term パッケージに含まれていますが、最小インストールでこれらがインストールされていないこともあります。
普段 Linux を使っていたが Solaris にログインしたらターミナルの挙動がおかしくなったといったときも、まずは terminfo を確認してみましょう。