## Zebra Gomoku

#### A ridiculously small JavaScript gomoku AI implementation, as a jQuery plugin

<br>

<img src="https://raw.githubusercontent.com/stefangabos/Zebra_Gomoku/master/screenshot.png" width="420" align="right" alt="Zebra Gomoku">

**Gomoku** is an abstract strategy board game also known as **Gobang** or **Five in a Row**, and it is traditionally played with Go pieces (black and white stones) on a go board with 15x15 cells; because once placed, pieces are not moved or removed from the board, gomoku may also be played as a paper and pencil game. The game is known in several countries under different names.

This is probably one of the shortest implementation of the game, weighing 1720 bytes of JavaScript (not counting jQuery, that is). A **much** shorter version exists at http://js1k.com/2010-first/demo/795 (by Keon Ahn) weighing just 1017 bytes *but* it doesn't has the possibility of changing the board's size, the player who starts the game, nor firing a callback function when the game ends. On the other hand it doesn't require jQuery, which makes it even more cooler *but* my version beats it fair and square, so I'll settle for that.

This started out as a weekend project but turned out to be something that took away 2 or 3 hours a day for two weeks, time spent playing countless games with other AIs (like those by [Steffen Gerlach](http://steffengerlach.de/gomoku/index.html) and [Anton Mudrenok](http://codepen.io/mudrenok/pen/gpMXgg)) in order to adjust the game formula, fixing bugs, optimizing and commenting the code. In the process I found out that there is a [championship for Gomoku AIs](http://gomocup.org/), that the best ever AI is [Yixin](http://www.aiexp.info/pages/yixin.html), and that there's a paper called [Go-Moku and Threat-Space Search](https://chalmersgomoku.googlecode.com/files/allis1994.pdf) where the authors "solved" the game.

While this AI performs decently, given the amount of code used to write it, it doesn't do that well when matched against an AI which implements more complex algorithms and which check A LOT of moves in advance - like the one by [Yao Yujian](http://yjyao.com/2012/06/gomoku-in-html5.html) (which my AI manages to defeat if it is the one starting the game).

You can choose the board's size, the player who makes the first move, and a callback function to be fired when somebody wins the game.

>Currently this implementation does not handle the situation where there are no more moves left. Nothing will happen in that case. That's because I couldn't find a way to handle that without writing more code :)

#### The minified code

>Note that I've used Jed Schmidt's [Byte saving techniques](https://github.com/jed/140bytes/wiki/Byte-saving-techniques) to make the code a bit shorter

```javascript
(function(g){g.gomoku=function(A,B){var C={board_size:15,ai_first:null,endgame:null},h=this,e=[],c,u,v=!1,x=function(c,f){e[c]=f;g(u[c]).addClass("p"+Math.abs(f-h.s.ai_first))};(function(){h.s=g.extend({},C,B);h.board=A;c=h.s.board_size;var y=g('<table id="zebraGomoku">').on("click","td",function(){if(!v||e[u.index(this)])return!1;x(u.index(this),2);var a,q,m,b,r,n,d,k,l,f,g,p,t,w;v=!1;for(a=c*c;a--;)if(1!=e[a]){e[a]||void 0!==p||(p=[a,0,0]);t=[0,0];for(q=4;q--;){w=[0,0];for(m=e[a]?1:5;m--;){k=e[a]||void 0;l=[];for(b=7;b--;)if(r=-5+m+b,n=a%c,!((0===q&&!1!==(d=a+c*r)&&n==d%c||1==q&&!1!==(d=a+r)&&~~(d/c)==~~(a/c)||2==q&&!1!==(d=a-c*r+r)&&(d>a&&d%c<n||d<a&&d%c>n||d==a)||3==q&&!1!==(d=a+c*r+r)&&(d<a&&d%c<n||d>a&&d%c>n)||d==a)&&0<=d&&d<c*c)||e[d]!=k&&(e[a]||e[d]&&void 0!==k)&&b&&6!=b)if(b&&6!=b)break;else l.push(void 0);else l.push(d),b&&b^6&&void 0===k&&e[d]&&(k=e[d]);if(7==l.length&&void 0!==k){r=e[a]?!0:!1;e[a]=k;g=n=f=0;for(b=5;b--;)e[l[b+1]]==k&&n++;for(b=l.indexOf(a)-1;0<=b;b--)if(e[l[b]]==k)f++;else{0===e[l[b]]&&g++;break}for(b=l.indexOf(a);b<l.length;b++)if(e[l[b]]==k)f++;else{0===e[l[b]]&&g++;break}b=[[0,1],[2,3],[4,12],[10,64],[256,256]][f>=n?Math.min(f,5)-1:n-1][f>=n?g?g-1:0:0];r?256<=b&&(b=1024):e[a]=0;b>w[k-1]&&(w[k-1]=b)}}for(m=2;m--;)t[m]+=w[m]}q=t[0]+t[1];m=p[1]+p[2];(q>m||q==m&&t[0]>=p[1])&&(!e[a]||1024<=t[1])&&(p=[a,t[0],t[1]])}1024>p[2]&&x(p[0],1);(256<=p[1]||1024<=p[2])&&"function"==typeof h.s.endgame?h.s.endgame.apply(null,[1024>p[2]]):v=!0}),f,z;for(f=0;f<c*c;f++)e[f]=0,f%c||y.append(z=g("<tr>")),z.append(g("<td>"));h.board.append(y);u=g("td",h.board);h.s.ai_first||null===h.s.ai_first&&Math.random()+.5|0?(h.s.ai_first=1,x(~~(c/2)*(1+c),1)):h.s.ai_first=2;v=!0})()}})(jQuery);
```

Go ahead, [try it yourself](http://stefangabos.github.io/Zebra_Gomoku/)

#### Embedding

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
