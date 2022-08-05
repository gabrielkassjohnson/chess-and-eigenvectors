# chess-and-eigenvectors
A linear algebraic method for calculating the relative strength of each chess piece from a large dataset of high quality games

A Description of the Problem


Much has been written about the relative strength of the chess pieces. Dozens or hundreds of articles, notes, and opinions can be found stretching back hundreds of years.
The earliest reference to the heuristic still commonly used today, of pawns worth 1, bishops and knights worth 3, rooks worth 5, and queens worth 9, has been in use for decades, if not longer [1].


Many other heuristics have been proposed to capture the relative strength of each chess piece, and even some true calculations, such as the space averaging calculation of _____ [cite].

The researchers as DeepMind have performed detailed analyses of their oevre of games played by AlphaZero, their chess playing system. Their estimations of relative piece value are below:

```
In Classical chess, piece values vary based on positional
considerations and game stage.[...] bishops are typically considered to be more
valuable than the knights, and there is usually an additive
adjustment while in possession of a bishop pair. The rook
value varies between 4.5 and 5.5 depending on the system
and the queen values span from 8.5 to 10. The relative
piece values estimated on the AlphaZero game sample for
Classical chess, 3.05–3.33–5.63–9.5, do not deviate much
from the existing systems. [2]
```


The reason why so many approximations exist is that it's hard to encapsulate how the dynamics of the game work into a simple system of numbers. Different approaches will also have differing pros and cons to their perspective.
The obvious advantage of the basic heuristic is in it's heuristic nature, it's simple. It can be taught to anyone, of any level of play, and remembered without effort.
Some of the other approximations have other advantages. The space calculation has the advantage of objectivity, and also representing one critical aspect of how players conceive of the game: the possibility of movement. Players are
constantly considering where to move their pieces. Pieces that can move further clearly have more opportunities for attack and defense, because they can reach more squares.
So this calculation does capture something about the true value of each piece.
The objectivity of the approach is apparent in another detail of it's outcome, the ratios. The proportions of value between all the pieces are somewhat more complicated than the standard heuristic, and we should pay attention to this.


One final historical heuristic to mention is ____(stiegliitz?) [cite]. His approach accounts for another weakness of the standard heuristic, the weakness of the outside pawns.
It is well known that the outside pawns are weaker than the center pawns, but the question is: by how much?
Stieglitz estimates these point advantages as roughly _____ (a quarter point?).
The procedure described below gives an objective way of calculating the difference in strength between pawns, on their starting positions.
The concerns mentioned here lead to a logical conclusion, that the existing heuristics are all useful for different reasons, and all lacking in some respect.
The over-simplicity of the standard heuristic is a problem for all but beginning players.
It would be useful to know the true strength of each piece.
In line with the historical approaches described above, here are the three main (but not exhaustive) hypotheses, which are simple to state, arguing why certain characteristics of a strength heuristic make it innacurate.
These hypotheses can also been seen as a minimum standard by which heuristics can be judged. It all depends on what information you want to capture. 


Hypotheses


1. The white pieces have an overall advantage over blacks pieces, due to the first move tempo advantage. This inequality has been known and discussed for a very long time. It is natural to contend that a calculation of the relative
strengths of the pieces would show this small difference. It is logical to contend that the overall advantage of white will translate to very small advantages for each of white's pieces over each of black's equivalent piece, on average.
That is to say, one can expect the sum of the values of all of white pieces to be slightly higher than the sum of all of black's pieces.
This contention raises two pertinent details. One, a heuristic should be simple, so a difference of half a percent may not be 'heuristic' in nature, in that it can't be described
as a simple integer fraction. This implies the second point:


2.It is natural to expect that any calculation of the relative strengths of the chess pieces will probably not exhibit behavior that conforms to simple fractions of small integers. That is, one can expect the results of any such calculation
to extend to some number of decimal digits (and perhaps even an arbitrary or infinte number of decimal digits, depending on how the calculation is done).


3.The known difference in strength between the outside pawns and the central pawns should be reflected in an approximation or calculation. 



Naturally it is hard to capture subtle information in a heuristic, so this approach is much closer to a pure calculation, yeilding individual strengths for each piece, not necesarily easy to memorize,
but full of usefull information about the pieces on the board, information lacking in simpler heuristics.
I would like to note that the above hypothesis are not the only implied effects of having an accurate calculation of the relative strength of each piece.
There are knock on effects, some predictable, and some not.
One more important implication can be stated as another hypothesis:


4.The kingside and queenside versions of a major piece, on the same side of the board, are not equal in value. They are likely very close, but not identical in strength, for the same reasons that outside pawns are weaker,
they are weaker because of being constrained and innefective in their starting position, and nothing else. They can move the same as any other of the same piece type, it's their starting position that matters.


This implies one final caveat about understanding the results of the following procedure: they only apply to pieces in their starting positions, at the beginning of the game. They don't show on their face positional strengths.
Once the game starts, and pieces start moving, their actual strength in that situation is not the same as it was when the position was different.
One way to think about this is sacrifice value. In the endgame, just because a pawn started out as a central pawn or an outside pawns doesn't make it more valuable anymore, the position has changed so much, and there are so few pieces on the board that
it doesn't matter anymore, only the position matters.
So if this procedure doesn't capture positional information what does it capture?
It averages all of those positional advantages into a single number that for each piece that represents it's capturing ability, relative to other pieces.
This approach takes as an axiom that capturing pieces,over many games, is what demonstrates a pieces relative strength.
Furthermore, the entire game is advanced by capturing pieces, until the King too is inevitably trapped and captured. So these numbers also represent each piece's 'influence' over the game, from their starting positions.
For example, what exactly is the underlying reason why a queen should be worth so much? Is it because it can move around the board better than other pieces? Yes, but the real effect of that is that it can capture many more pieces than
say, a pawn. There is nothing preventing a pawn from capturing many pieces in any given game, even a piece of high value. But averaged over many, many games, the panws will not be capturing nearly as many pieces as the stronger
pieces are capturing, and weaker pieces will, on average, capture pieces with lower strengths.


A Description of the Procedure


Let's consider this simple version of the procedure to start.
Simply tally up the number of captures for each piece on the board, over a large number of games. That's it!
If you overlay these numbers on a chess board you will see that the queens captured more pieces than any other pieces. The major pieces captured more than any of the pawns. And we can even see that the central pawns had more captures
than the outside pawns.
Even this simple tally shows some of the aspects of our hypotheses.
But this is not how we normally think of chess values. Usually a pawn is equal to one. To scale down our values to the point where a pawn is equal to one, we need to normalize our values.
That means we divide every value on the board by the same number, keeping all the proportions the same, but lowering the numbers to a point where they're easy to make sense of.
We can normalize to any value, and normalizing to certain pieces on the board will make certain information more obvious. We'll discuss those differences at the end, when we have our final data.
For now, let's normalize to the value of the average pawn. That way, when we see the proportional values of the major pieces, they will be on the same scale as all the historical heuristics (in which pawns are worth 1), and we can compare them.
After the values are normalized, the average of all the pawns is 1, but their values are either above or below 1, depending on their position (hypothsis 3). Voila! Our hypothesis are beginning to appear in the data.
These numbers are not simple fractions of integers (hypothesis 2).
The numbers for white are larger than the numbers for black, both overall, and for certain pairs of pieces (hypothesis 1).
The kingside and queenside versions of each major piece have different numbers of captures (hypothesis 4).

Even this simple tallying procedure has results that confirm our hypothesis, and that contain fine-grained information about the relative strengths of the pieces.
But there is an obvious problem, the proportions of the pieces are not correct.
A simple tally considers all captures to be the same, but capturing stronger pieces is more significant, and a simple tally doesn't register that.
We contented that the stronger pieces tended to capture stronger pieces, on average.
So how can we calculate the tally, including all the strengths of the pieces that were captured?
Just that, we need weights for each piece, so that when a strong piece is captured, the capturing piece gets tally points proportional to the strength of the piece that it captured.
So when a piece captures another piece, it gets the weight of the captured piece addded to it's tally.
But how can we know what the weights are?
When we try to go do the tally, we have no idea what weights to use, since we haven't calculated them yet.
If you want to tally a capture, it adds value to the weight of the capturing piece, and then, uh-oh, you have to reconsider all the times that piece was captured, changing all the values of all the other pieces. Big uh-oh!
What to do?
This problem is exemplified by the epigram on the wonderful article about chess piece strength in the online blog ______ [cite]
The author starts this article, which I encourage you to read, with a quote from _______ about the nature of balancing all the interconnected relationships on the chess board.
""

This perfectly encapsulates the tallying problem we just described, and shows a keyhole into how this problem can be solved.
Enter Liner Algebra!
This structure of problem is perfectly suited for linear algebra.
The interlocking connections in our weighted tallying system, where each change of a single value changes every other value, is, in fact, an Homogeneous System of Linear Equations. 
It is a list of 32 equations, one for each of the pieces. On the left side of each equation is the weight of each individual chess piece, multipled by an implied 1.
On the right side of the equation is the sum of all of that piece's captures, 16 terms, one for each of the opposing pieces that it could capture (a side can't capture it's own pieces)
where each capture is multuplied by the weight of the piece captured. 
The beauty of linear algebra is that it can solve all the equations at once, bypassing the shifting weights issue.
Every homogeneous system of linear equations has at least one solution, the zero vector. But that has no interest for us, it doesn't contain useful information.
(Except perhaps on a philosophical level, suggesting that the game is somewhow reducible in it's entirety)
To find a non-trivial solution, one can use a matrix factorization.
Each eigenvector is a solution. In our case, all eigenvectors except one contain imaginary values.
Let's choose the real-valued eigenvector, and take it's entries as solutions to each equation.
These are the true relative strengths of each chess piece.
The quality of the games used in the calculation will change the values slighly. We aim to use games above a minimum quality level to capture the truer essence of the piece's strength.

## References

[1] Capablanca, J. and de Firmian, N. Chess Fundamentals:
Completely Revised and Updated for the 21st Century.
Chess Series. Random House Puzzles & Games, 2006.

[2] Tomašev, N., Paquet, U., Hassabis, D., & Kramnik, V. (2020). Assessing Game Balance with AlphaZero: Exploring Alternative Rule Sets in Chess. ArXiv, abs/2009.04374.