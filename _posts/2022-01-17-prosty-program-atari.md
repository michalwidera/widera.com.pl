---
title: "Prosty program na Atari"
excerpt_separator: "<!--more-->"
toc: true
toc_label: "Napis - Muro"
categories:
  - Blog
tags:
  - atari
---

~~~
10 GRAPHICS 3
20 COLOR 3
30 READ M
40 IF M<0 THEN MODE=M
41 IF MODE=-3 THEN GOTO 100
45 IF M<0 THEN READ X
50 IF M>=0 THEN X=M
55 READ Y
60 IF MODE=-1 THEN PLOT X,Y
70 IF MODE=-2 THEN DRAWTO X,Y
90 GOTO 30
100 PRINT "END."
110 DATA -1,0,6
111 DATA -2,0,0,3,3,6,0,6,6
112 DATA -1,8,3
113 DATA -2,8,6,11,6,11,3
114 DATA -1,13,6
115 DATA -2,13,3,15,3
116 DATA -1,17,6
117 DATA -2,17,3,20,3,20,6,17,6
130 DATA -3
~~~

![Wykonanie programu na Atari](/assets/images/atari-simple-prog.jpg)

