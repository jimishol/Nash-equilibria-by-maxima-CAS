# Pure-Nash-by-maxima-CAS</p>
Finding pure Nash
equilibriums for multiplayer games using Computer Algebra System
(maxima CAS).

Whoever starts to
study game theory, starts to solve many exercises about finding pure
Nash equilibrium in particular models. It is funny at the start but
after one gets the essentials of the process, the process start to
feel very repetitive. In that case, either because the student would
like verification of his manual solution either he wants to avoid
repetition of the same process, it seems nice to let the calculation
to be done by his software. In this repository I use the free and
very nice Computer Algebra System
[maxima](https://maxima.sourceforge.io/index.html) or his equally
very nice graphical interface [wxmaxima](https://wxmaxima-developers.github.io/wxmaxima/).

(The files were created by using exclusively the lovely 'wxmaxima' graphical interface. To acquire the equilibriums one does not
actually need the 'wxmaxima' interface and the corresponded .wxmx files.)


<p style="line-height: 100%; margin-bottom: 0cm">The model of the
game is given by a file, in comma separated values format, called
<b>NashData.csv</b></p>
<p style="line-height: 100%; margin-bottom: 0cm">It can be edited by
hand. The first row is a series of numbers where the first one is the
number of players and the next ones gives, sequentially, how many
actions are available to each one of the players. So,</p>
<p style="line-height: 100%; margin-bottom: 0cm">7,8,9,3,6,2,9,6</p>
<p style="line-height: 100%; margin-bottom: 0cm">1,1,1,1,1,1,1,1,2</p>
<p style="line-height: 100%; margin-bottom: 0cm">…</p>
<p style="line-height: 100%; margin-bottom: 0cm">means a 7 players
game, with 8 actions for 1<sup>st</sup> player, 9 for 2<sup>nd</sup>,
3 for 3nd, 6 for 4<sup>th</sup> and so on.</p>
Next rows give the rewards of each player for each profile. So, from the example above,
the <b>NashData.csv</b> file should have the first row plus other 7(players)
* (8*9*3*6*2*9*6) (profiles per player) = 7 * 139968 =  979776 rows.
That means exactly 979777 rows. (About 1 million rewards is the
maximum that either 'maxima' or my laptop can handle in about 7 minutes
of calculations. Above that limit, calculations are interrupted with
a message that informs that Lisp can not collect or handle some
garbage data)

<p style="line-height: 100%; margin-bottom: 0cm">Each row points, by
its first number, to the number of a player, by the rest numbers, excluded
the last one, points to the profile the particular player is facing and
by the last number to the reward that this player has for that
particular profile.  So, with the exception of the first row that has 8 numbers, with 7 players each row, has 9 numbers. (1 for the player, 7 for the
profile and 1 for the reward.)</p>
<p align="center" style="line-height: 100%; margin-top: 0.11cm; margin-bottom: 0.21cm; page-break-after: avoid">
<font face="Liberation Sans, sans-serif"><font size="5" style="font-size: 18pt">Data
input</font></font></p>
A convenient way to input the data is to use maxima to create, excluding the rewards, all other
data automatically.

Edit and execute the file <b>Pure_Nash_create_data.wxmx</b> (to use it by 'wxmaxima')
or the <b>Pure_Nash_create_data.wxm</b> (to use it by 'maxima).

The execution will create <span lang="en-US"><b>NashData.csv</b> </span><span lang="en-US">file
with random, 1 digit, rewards.</span>
<p><span lang="en-US">After that, one only needs to replace the 1
digit rewards by the desired ones.</span></p>
<p><span lang="en-US">On the basic use, one edits the
  </span><span lang="en-US"><i>Pure_Nash_create_data</i> </span><span lang="en-US">file
and gives the first row as a list. For the example above the first
row of data should be given as</span></p>
<p><span lang="en-US">n:[</span><span lang="en-US">7,8,9,3,6,2,9,6</span><span lang="en-US">]</span></p>
<p><span lang="en-US">(Alternatively, by commenting the basic row, where ‘n’ list is defined, and un-commenting the next two rows,
one can give only the number of players, for example, as</span></p>
<p><span lang="en-US">N:7</span></p>
<p><span lang="en-US">and the execution of </span><span lang="en-US"><i>Pure_Nash_create_data</i>
</span><span lang="en-US">file will create random, from to 2 to 9,
number of actions for each player too.)</span></p>
<p align="center" style="line-height: 100%; margin-top: 0.11cm; margin-bottom: 0.21cm; page-break-after: avoid">
<font face="Liberation Sans, sans-serif"><font size="5" style="font-size: 18pt">Pure
Nash equilibriums</font></font></p>
<p>To find pure Nash equilibriums one loads the <b>Pure_Nash.wxmx</b> by 'wxmaxima' and run it
  or</p>
execute


<p><span lang="en-US"><B>maxima -b ~/Pure_Nash.wxm</B></span></p>
<p><span lang="en-US">in a terminal.</span></p>
<p><span lang="en-US">The equilibriums are given as a list of
equilibrium lists. For example in</span></p>
<p><span lang="en-US">[[7, 2, 3], [6, 9, 2], …]
  
we see that the second equilibrium, in a 3 players’ game, consists of decisions
where 1</span><sup><span lang="en-US">st</span></sup><span lang="en-US">
player chooses his 6</span><sup><span lang="en-US">th</span></sup><span lang="en-US">
action, 2</span><sup><span lang="en-US">nd</span></sup><span lang="en-US">
player chooses his 9</span><sup><span lang="en-US">th</span></sup><span lang="en-US">
and 3nd player chooses his 2</span><sup><span lang="en-US">nd </span></sup><span lang="en-US">action.</span></p>
<p align="center" style="line-height: 100%; margin-top: 0.11cm; margin-bottom: 0.21cm; page-break-after: avoid">
<font face="Liberation Sans, sans-serif"><font size="4" style="font-size: 14pt">Internally
used process</font></font></p>
<p>Lucking sufficient knowledge on my hobbies of maths and
programming, I used ‘brutal’ force to acquire the results. I let 'maxima' to create, as strings, sequences of ‘for’
loops and ‘if’ conditions, depending on the number of players and the number of actions that each one has in his disposal.</span></p>
<p><span lang="en-US">The process consist of creating, from the input
data,</span></p>
<p style="line-height: 100%; margin-top: 0.42cm; margin-bottom: 0.21cm; page-break-after: avoid">
<font face="Liberation Sans, sans-serif"><font size="4" style="font-size: 14pt"><i>the
  R list</i>.</font></font></p>
<p><span lang="en-US">Every element of R consist of two lists</span></p>
<p><span lang="en-US">[list1, [r1,...,r_ak]]</span></p>
<p><span lang="en-US">where list1, on the form of [k, s1,s2, ... (-sk) ...,sn], informs that when player k is facing the si_th action of ith other
player, (-sk) means the profile that does not include the actions of the player himself, gets rewards r1 for his 1st action, r2 for his
2nd and so on till the reward r_ak  for his last available 'ak' action.</span></p>
<p><span lang="en-US">So, [[2,1,2],[17,22]] is from a 3 players game.
It means that the player 2 has two actions, with rewards 17 for his first one and 22 for his second. He gets these rewards when he is facing
the 1st action of player 1 and the 2nd action of player 3 [2,1,2].</span></p>
<p style="line-height: 100%; margin-top: 0.42cm; margin-bottom: 0.21cm; page-break-after: avoid">
  <font face="Liberation Sans, sans-serif"><font size="4" style="font-size: 14pt"><i>The BR list</i></font></font></p>
<p><span lang="en-US">is created from the R list. BR has the same
format as that of list R [list1, list2].</span></p>
<p><span lang="en-US">list1 is the same [k, s1,s2, ... (-sk) ...,sn]
.</span></p>
<p><span lang="en-US">However, list2 consists of the list of indexes
of actions that gives the maximum reward.</span></p>
<p><span lang="en-US">For example if the list of the rewards [r1,...,r_ak] was
[1,3,-2,3] then list2 would be equal to [2,4].</span></p>
<p style="line-height: 100%; margin-top: 0.42cm; margin-bottom: 0.21cm; page-break-after: avoid">
<font face="Liberation Sans, sans-serif"><font size="4" style="font-size: 14pt">Equilibrium
criteria</font></font></p>
<p>are created as string. Every profile, so every combination of
actions, is checked against Nash equilibrium criteria by executing
that string.</p>
