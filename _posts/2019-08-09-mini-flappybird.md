---
title: Mini FlappyBird
author: ethelpoe
date: 2019-08-09 20:55:00 +0800
categories: [Blogging, Tutorial]
tags: [games]
pin: false

---

# Dibujando el background.

Un rectangulo de color azul sera nuestro background.

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

ahora dibujamos el pichon o pochito

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
void bird(){
  fill(224,214,68);
  rect(62,200,30,25);
}
```

ahora lo movemos

```java
int pochitoPosY = 200;

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
  pochitoPosY += 30;
}
```

agregando gravedad

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
  //actualizamos la gravedad
  pochitoYSpeed += gravity;
  //actualiazamos la posicion en y de player
  pochitoPosY += pochitoYSpeed;
}

```

flapping

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
  //actualizamos la gravedad
  pochitoYSpeed += gravity;
  //actualiazamos la posicion en y de player
  pochitoPosY += pochitoYSpeed;
}
//al presionar cualquier tecla el player se desplaza hacia arriba
void keyPressed(){
  pochitoYSpeed = -5.5f;
}

```

el player no deberia ser capaz de salir de la pantalla

```java
void keyPressed(){
  //comprobamos si el player esta dentro del area de juego
  if(pochitoPosY > 0){
    pochitoYSpeed = -5.5f;
  }
}
```

dibujando tuberia

> [Learning Processing 2nd Edition](http://learningprocessing.com/)

> [Collision Detection (jeffreythompson.org)](http://jeffreythompson.org/collision-detection/table_of_contents.php)

