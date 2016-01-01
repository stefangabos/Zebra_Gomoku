## Zebra Gomoku

#### A ridiculously small JavaScript gomoku AI implementation, as a jQuery plugin

<br>

<img src="https://raw.githubusercontent.com/stefangabos/Zebra_Gomoku/master/screenshot.png" width="420" align="right" alt="Zebra Gomoku">

**Gomoku** is an abstract strategy board game also known as **Gobang** or **Five in a Row**, and it is traditionally played with Go pieces (black and white stones) on a go board with 15x15 cells; because once placed, pieces are not moved or removed from the board, gomoku may also be played as a paper and pencil game. The game is known in several countries under different names.

This is probably one of the shortest implementation of the game, weighing 1848 bytes of JavaScript (not counting jQuery, that is). A **much** shorter version exists at http://js1k.com/2010-first/demo/795 weighing just 1017 bytes *but* it doesn't has the possibility of changing the board's size, the player who starts the game, nor firing a callback function when the game ends. On the other hand it doesn't require jQuery, which makes it even more amazing *but* my version beats it fair and square, so I'll settle for that.

This started out as a weekend project but turned out to be something that took away  2 or 3 hours a day for two weeks, time spent playing endless games with other AIs (mostly [this](http://steffengerlach.de/gomoku/index.html) and [this](http://codepen.io/mudrenok/pen/gpMXgg)) in order to adjust the game formula, fixing bugs, optimizing and commenting the code. In the process I found out that there is a [championship for Gomoku AIs](http://gomocup.org/) that the best ever AI is [Yixin](http://www.aiexp.info/pages/yixin.html) and that there's a paper called [Go-Moku and Threat-Space Search](https://chalmersgomoku.googlecode.com/files/allis1994.pdf) where the authors "solved" the game.

Currently this implementation does not handle the situation where there are no more moves left. Nothing will happen in that case. That's because I couldn't find a way to handle that without writing more code :)

[Play Zebra_Gomoku now](http://stefangabos.github.io/Zebra_Gomoku/)

###### How to use

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
