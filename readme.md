## Zebra Gomoku

#### A ridiculously small JavaScript gomoku AI implementation, as a jQuery plugin

<br>

<img src="https://raw.githubusercontent.com/stefangabos/Zebra_Gomoku/master/screenshot.png" width="420" align="right" alt="Zebra Gomoku">

**Gomoku** is an abstract strategy board game also known as **Gobang** or **Five in a Row**, and it is traditionally played with Go pieces (black and white stones) on a go board with 15x15 cells; because once placed, pieces are not moved or removed from the board, gomoku may also be played as a paper and pencil game. The game is known in several countries under different names.

This is probably one of the shortest implementation of the game, weighing 1768 bytes of JavaScript (not counting jQuery, that is). A **much** shorter version exists at http://js1k.com/2010-first/demo/795 (by Keon Ahn) weighing just 1017 bytes *but* it doesn't has the possibility of changing the board's size, the player who starts the game, nor firing a callback function when the game ends. On the other hand it doesn't require jQuery, which makes it even more cooler *but* my version beats it fair and square, so I'll settle for that.

This started out as a weekend project but turned out to be something that took away 2 or 3 hours a day for two weeks, time spent playing countless games with other AIs (like those by [Steffen Gerlach](http://steffengerlach.de/gomoku/index.html) and [Anton Mudrenok](http://codepen.io/mudrenok/pen/gpMXgg)) in order to adjust the game formula, fixing bugs, optimizing and commenting the code. In the process I found out that there is a [championship for Gomoku AIs](http://gomocup.org/), that the best ever AI is [Yixin](http://www.aiexp.info/pages/yixin.html), and that there's a paper called [Go-Moku and Threat-Space Search](https://chalmersgomoku.googlecode.com/files/allis1994.pdf) where the authors "solved" the game.

While this AI performs decently, given the amount of code used to write it, it doesn't do that well when matched against an AI which implements more complex algorithms and which check A LOT of moves in advance - like the one by [Yao Yujian](http://yjyao.com/2012/06/gomoku-in-html5.html) (which my AI manages to defeat if it is the one starting the game).

You can choose the board's size, the player who makes the first move, and a callback function to be fired when somebody wins the game.

*Currently this implementation does not handle the situation where there are no more moves left. Nothing will happen in that case. That's because I couldn't find a way to handle that without writing more code :)*

###### Below is the minified code

*Note that I've used Jed Schmidt's [Byte saving techniques](https://github.com/jed/140bytes/wiki/Byte-saving-techniques) to make the code a bit shorter*

<textarea>(function(f){f.gomoku=function(A,B){var C={board_size:15,ai_first:null,endgame:null},l=this,e=[],b,u,v=!1,x=function(b,g){e[b]=g;f(u[b]).addClass("p"+Math.abs(g-l.s.ai_first))};(function(){l.s=f.extend({},C,B);l.board=A;b=l.s.board_size;var y=f('&lt;table id="zebraGomoku"&gt;').on("click","td",function(){if(!v||e[u.index(this)])return!1;x(u.index(this),2);var a,q,p,c,r,d,m,n,g,f,t,h,k,w;v=!1;for(a=b*b;a--;)if(1!=e[a]){e[a]||void 0!==h||(h=[a,0,0]);k=[0,0];for(q=4;q--;){w=[0,0];for(p=e[a]?1:5;p--;){m=e[a]||void 0;n=[];for(c=7;c--;)if(r=-5+p+c,!((0===q&&!1!==(d=a+b*r)&&a%b==d%b||1==q&&!1!==(d=a+r)&&~~(d/b)==~~(a/b)||2==q&&!1!==(d=a-b*r+r)&&(d>a&&d%b<a%b||d<a&&d%b>a%b||d==a)||3==q&&!1!==(d=a+b*r+r)&&(d<a&&d%b<a%b||d>a&&d%b>a%b)||d==a)&&0<=d&&d<b*b)||e[d]!=m&&(e[a]||e[d]&&void 0!==m)&&c&&6!=c)if(c&&6!=c)break;else n.push(void 0);else n.push(d),c&&c^6&&void 0===m&&e[d]&&(m=e[d]);if(7==n.length&&void 0!==m){r=e[a]?!0:!1;e[a]=m;t=g=f=0;for(c=5;c--;)e[n[c+1]]==m&&g++;for(c=n.indexOf(a)-1;0<=c;c--)if(e[n[c]]==m)f++;else{0===e[n[c]]&&t++;break}for(c=n.indexOf(a);c<n.length;c++)if(e[n[c]]==m)f++;else{0===e[n[c]]&&t++;break}c=[[0,1],[2,3],[4,12],[10,64],[256,256]][f>=g?Math.min(f,5)-1:g-1][f>=g?t?t-1:0:0];r?256<=c&&(c=1024):e[a]=0;c>w[m-1]&&(w[m-1]=c)}}for(p=2;p--;)k[p]+=w[p]}q=k[0]+k[1];p=h[1]+h[2];(k[0]||k[1])&&(q>p||q==p&&k[0]>=h[1]&&k[0]^h[1]&&k[1]^h[2])&&(!e[a]||1024<=k[1])&&(h=[a,k[0],k[1]])}1024>h[2]&&x(h[0],1);(256<=h[1]||1024<=h[2])&&"function"==typeof l.s.endgame?l.s.endgame.apply(null,[1024>h[2]]):v=!0}),g,z;for(g=0;g<b*b;g++)e[g]=0,g%b||(z=f("&lt;tr&gt;").appendTo(y)),f("&lt;td&gt;").appendTo(z);y.appendTo(l.board);u=f("td",l.board);l.s.ai_first||null===l.s.ai_first&&Math.random()+.5|0?(l.s.ai_first=1,x(~~(b/2)*(1+b),1)):l.s.ai_first=2;v=!0})()}})(jQuery);</textarea>

<br>
Go ahead, [try it yourself](http://stefangabos.github.io/Zebra_Gomoku/)
<br><br>

###### Embedding

This should get you started:

```javascript
<!doctype html>
<html>
<head>
	<meta charset="utf-8">
	<title></title>
   	<link rel="stylesheet" href="path/to/zebragomoku.css">
    <style type="text/css">
    #game {
        width: 800px;
        height: 800px;
        margin: 50px auto;
    }
    </style>
</head>
<body>
    <div id="game"></div>
    <script src="path/to/jquery-1.11.3.js"></script>
    <script src="path/to/zebragomoku.min.js"></script>
    <script>
    $(document).ready(function() {

        // the board size will have the same size as the container element
        new $.gomoku($('#game'), {

            ai_first: null,		// 	should the computer start? true/false/null;
                                //	when set to null will be decided randomly
                                //	whoever starts plays white

            board_size: 15,		//	the size of the board; the board is square

            // the callback function to be executed when somebody wins the game
            endgame: function(ai_wins) {
                alert('You ' + (ai_wins ? 'lost' : 'won') + '!');
            }

        });

    });
    </script>
</body
</html>
```
