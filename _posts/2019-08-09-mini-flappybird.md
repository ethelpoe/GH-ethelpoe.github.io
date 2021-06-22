---
title: Mini FlappyBird
author: ethelpoe
date: 2019-08-09 20:55:00 +0800
categories: [Blogging, Tutorial]
tags: [games]
pin: false

---

## Dibujando el background.

lo primero que haremos es dibujar el background de nuestro juego, un cuadro de 600 x 600 color azul será nuestro fondo.

```java
void setup(){
  //size of the screen
  size(600,600);
}
void draw(){
  //background color
  background(35,92,118);
}
```

<img src="https://lh3.google.com/u/0/d/1UdiXBIrQ_oQPBGbwZWNlnt1GAhKwTFIU=w1485-h942-iv1" style="zoom:50%"/>

Lo siguiente es dibujar en pantalla nuestro player que esta ocasión será un cuadrito color amarillo.

```java
void setup(){
  //size of the screen
  size(600,600);
}
void draw(){
  //color del background
  background(35,92,118);
  bird();
}

//funtion that draw our player
void bird(){
  fill(224,214,68);
  rect(62,200,30,25);
}
```

<img src="https://lh3.google.com/u/0/d/1EbqLX6d1QEoMFrb1etuXPbgcYm7v1iyW=w1485-h942-iv1" style="zoom:50%"/>

Estaremos acomodando nuestro código en funciones para que sea más fácil el encontrar cualquier bug que pueda tener. El código de abajo ahora permitirá que el player se desplace hacia abajo 3 unidades por frame.

```java
//pos y of player
int pochitoPosY = 200;

//speed for player
float pochitoYSpeed = 3;

void setup(){
  //size of the screen
  size(600,600);
  //framerate
  frameRate(60);
}
void draw(){
  //color del background
  background(35,92,118);
  birdDraw();
  move();
}
//funtion that draw our player
void birdDraw(){
  fill(224,214,68);
  rect(62,pochitoPosY,30,25);
}
//funtion that update the var pochitPosY
void move(){
  pochitoPosY += pochitoYSpeed;
}
```

<img src="https://lh3.google.com/u/0/d/1AFNX-64TtGUewUNRFGYv2m3FlyIiXqee=w1485-h942-iv1" style="zoom:50%"/>

Pero nuestro player solo parece que cae en caída libre tenemos que agregar algo para que la caída se vea un poco más real, tenemos que simular gravedad y eso lo logramos de la siguiente manera, presta atencion a la nueva variable que agregamosy `gravity` y la forma en que actulizamos la posicion Y del player.

```java
int pochitoPosY = 200;
float pochitoYSpeed = 0;
float gravity = 0.12f;

void setup(){
  //size of the screen
  size(600,600);
  //framerate
  frameRate(60);
}
void draw(){
  //color of background
  background(35,92,118);
  birdDraw();
  move();
}
void birdDraw(){
  fill(224,214,68);
  rect(62,pochitoPosY,30,25);
}
void move(){
  //update gravity
  pochitoYSpeed += gravity;
  //update position y of player
  pochitoPosY += pochitoYSpeed;
}

```

<img src="https://lh3.google.com/u/0/d/1tiiyV_4HxM3LSvouW21ao3og3pdVrCZ6=w1485-h942-iv2" style="zoom:50%"/>

Notas como el player parece acelerar conforme cae ese es el efecto de la gravedad. Ahora ocupamos que nuestro player realice algo que vamos a llamar "flapping" que es como el aleteo que haría un pájaro en el aire.

```java
int pochitoPosY = 200;
float pochitoYSpeed = 0;
float gravity = 0.12f;

void setup(){
  //size of the screen
  size(600,600);
  //framerate
  frameRate(60);
}
void draw(){
  //color del background
  background(35,92,118);
  birdDraw();
  move();
}
void birdDraw(){
  fill(224,214,68);
  rect(62,pochitoPosY,30,25);
}
void move(){
  //update gravity
  pochitoYSpeed += gravity;
  //update position y of player
  pochitoPosY += pochitoYSpeed;
}
//every time we press any key the player move upwards
void keyPressed(){
  pochitoYSpeed = -5.5f;
}

```

<img src="https://lh3.google.com/u/0/d/1VAIAqj9leQeFoEGG8Ez37Xca6tXX8TDm=w1485-h942-iv1" style="zoom:50%"/>

El player no debería ser capaz de salir de la pantalla volando, así que lo vamos a limitar actualizando la función `keyPressed()`

```java
void keyPressed(){
  //check if the player is out of the screen
  if(pochitoPosY > 0){
    pochitoYSpeed = -5.5f;
  }
}
```

Lo que falta ahora es dibujar los obstáculos en este caso serán tuberías, que representaremos como rectángulos verdes.

```java
int pochitoPosY = 200;
float pochitoYSpeed = 0;
float gravity = 0.12f;

//dimensions of obstacles
int obstacleWidth = 54;
int obstacleSpaceHeight = 100;
int obstacle1Height = 150;
int obstacleSpaceMin = 54;
int obstacle1PosX;
int obstaclePosY = 0;

//dimensions of second obstacles
int obstacle2PosX;
int obstacle2Height = 250;

int gameAreaWidth = 600;
int gameAreaHeight = 600;

void setup(){
  //size of the screen
  size(600,600);
  //framerate
  frameRate(60);
  
  obstacle1PosX = 300;
}
void draw(){
  //color del background
  background(35,92,118);
  birdDraw();
  move();
  obstacleDraw(obstacle1PosX,obstacle1Height);
}
void birdDraw(){
  fill(224,214,68);
  rect(62,pochitoPosY,30,25);
}
void move(){
  //updtate the gravity
  pochitoYSpeed += gravity;
  //update the pos of the player
  pochitoPosY += pochitoYSpeed;
}
//if we press any key this funtion is trigger
void keyPressed(){
  //check if the player is out of the screen
  if(pochitoPosY > 0){
    pochitoYSpeed = -5.5f;
  }
}
void obstacleDraw(int obstaclePosX,int obstacleHeight){
  fill(94,201,72);
  //coordinates top
  rect(obstaclePosX,obstaclePosY,obstacleWidth,obstacleHeight);
  //space between pipes
  fill(94,201,72);
  rect(obstaclePosX,obstacleHeight + obstacleSpaceHeight ,obstacleWidth,gameAreaHeight - obstacleHeight - obstacleSpaceHeight);
}
```



> [Learning Processing 2nd Edition](http://learningprocessing.com/)

> [Collision Detection (jeffreythompson.org)](http://jeffreythompson.org/collision-detection/table_of_contents.php)

