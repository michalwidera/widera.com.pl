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

W moich publikacjach można znaleźć edytor duszków.
Przepisanie tego programu może być udtrudnione.
Tutaj przepisany program:

~~~
100 DIM A$(22),SPRITE(8,22),DANE(22),BIN$(8):CLOSE #1:OPEN #1,4,0,"K:"
110 POKE 106,PEEK(106)-8
120 POKE 82,0:GRAPHICS 0:POKE 53248,0
130 PB=PEEK(106)
140 FOR A=1 TO 22:FOR B=1 TO 8
150 SPRITE(B,A)=0:NEXT B:NEXT A
160 FOR I=PB*256+1024 TO PB*256+2048:POKE I,0:NEXT I
170 FOR A=1 TO 22:A$(A,A)=CHR$(255):NEXT A
180 FOR A=0 TO 7:BIN$(8-A,8-A)=CHR$(2^A):NEXT A
190 POKE 54279,PB:POKE 53277,2
200 POKE 53248,90:POKE 559,58
210 GOSUB 400
220 ? "+--------+":FOR X=1 TO 22:? "|        |":NEXT X:? "+--------+";:X=1:Y=1
230 IF K=42 THEN X=X+1:IF X>8 THEN X=1
240 IF K=43 THEN X=X-1:IF X<1 THEN X=8
250 IF K=45 THEN Y=Y-1:IF Y<1 THEN Y=22
260 IF K=61 THEN Y=Y+1:IF Y<1 THEN Y=1
270 POSITION X,Y:? CHR$(159);
280 Z=PEEK(93):GET #1,K
290 IF K=27 THEN GOSUB 340
300 IF K=125 THEN RUN
310 IF K=155 THEN IF Z=0 THEN POSITION X,Y:? "#";:SPRITE(X,Y)=1
320 IF K=155 THEN IF Z<>0 THEN POSITION X,Y:? " ";:SPRITE(X,Y)=0
330 GOTO 230
340 FOR A=1 TO 22:SUMA=0
350 FOR B=1 TO 8
360 SUMA=SUMA+SPRITE(B,A)*ASC(BIN$(B,B))
370 NEXT B:DANE(A)=SUMA
380 A$(A,A)=CHR$(DANE(A))
390 NEXT A
400 FOR A=1 TO LEN(A$):POKE PB*256+1059+A,PEEK(ADR(A$)+A-1):NEXT A
410 RETURN
~~~

![Wykonanie programu na Atari](/assets/images/atari-ghost-editor.jpg)

Jak mimo wszystko ktoś chce tworzyć dane dla sprite sugeruję użyć czegoś bardziej użytecznego. 
Takie coś [SprEd](https://bocianu.gitlab.io/spred/) z pewnością będzię pomocne.
