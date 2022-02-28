# Set

To connect two sets, we always use function to map one set to another. If you learn linear algebra or set before, you should familiar with that.

1. Let function $f$ maps set $A$ to set $B$ 
   - Surjective(Onto) Function: $\forall b\in B,\exist a\in A,f(a)=b$
   - Injective(one-to-one) Function: $\forall a_1,a_2\in A,a_1\ne a_2\implies f(a_1)\ne f(a_2)$
     - Equivalent: $\forall a_1,a_2\in A,f(a_1)=f(a_2)\implies a_1=a_2$
2. If a set $A$ and a set $B$ has a bijective function, then $A$ and $B$ have the same cardinality.
   - Recall cardinality is used to refer to the size of a set
3. If a set $A$ has a bijective function $f$ where $f:\mathbb{N}\mapsto A$, then A is countable.
   - Notice infinite set can be countable, e.g. $\mathbb{N},\mathbb{Q}$
   - $\mathbb{R}$ is uncountable
4. **Schroder-Bernstein Theorem**: For sets $A$ and $B$, there exist a injective function $f:A\mapsto B$ and another injective function $g:B\mapsto A$, then $A$ and $B$ have the same cardinality.
5. Power Set: denote $P(A)$ as the power set of set A, where $P(A)=$ the set of all subset of $A$
6. **Cantor's Theorem**: There is no such surjective function $f$ of set $A$ that $f:A\mapsto P(A)$

## Property

Given $a\in \mathbb{R}$, a set $S\sube \mathbb{R}$ and $\epsilon>0$

1. $\epsilon-neighborhood$ is the set $V_{\epsilon}(a)=\{x\in\mathbb{R}:|x-a|<\epsilon\}$
2. $S$ is $open$ set if $\forall s\in S$, $\exists V_{\epsilon}(s)\sube S$
   - The union of an arbitrary collection of open sets is open
   - The intersection of a finite collection of open sets is open
3. A point $x$ is a $limit \ point$ of $A$ if $\forall V_{\epsilon}(x)\ \cap A \ne x$ (here$\ne$ try to present except x, there is another value)
   - let $L=$ all limit points of $A$. The $closure$ of $A$ can present as $\bar A= A \cup L$
4. $x$ is a limit point of $A$ $\iff$ A sequence$\{a_n\}, a_n\ne x$, $x=\lim a_n$ 
5. $a$ is a $isolated \ point$ if it is not a limit point
6. $A$ is $closed$ if it contains all of its limit points
   - the closure set is closed, and is the smallest closed set contain itself without limit points.
   - The union of a finite collection of closed sets is closed
   - The intersection of arbitrary collection of closed sets is closed
7. $A$ is closed $\iff$ Every Cauchy Sequence $\in A$ has a limit to an element of $A$
8. The complement of $A$ denote as $A^c = \{x\in\mathbb{R}:x\notin A\}$
9.  $A$ is open $\iff$ $A^c$ is closed
10. $A$ is $bounded$ if $\exist M>0, \forall a\in A, |a|\le M$
11.  $A$ is $compact$ if every sequence in $A$ has a subsequence that converges to a limit $\in A$
12. $A$ is compact $\iff$ $A$ is closed and bounded
13. $open \ cover$ is a collection of open set that union contains the set $A$. Let  $\{L_n\}$ be the open cover then $A\sube \cup_n L_n$ 
14. $finite \ subcover$ is a finite sub-collection of open sets from open cover that union still contain $A$. 
15. **Heine-Borel Theorem**: any one of following can implies other two
    - $A$ is compact
    - $A$ is closed and bounded
    - every open cover for $A$ has a finite subcover

## Cantor Set

We define the Cantor Set $C$ to be the intersection $C=\bigcap_{n=0}^{\infin}C_n$
