---
title: Snake Game with Processing and Java
author: ethelpoe
date: 2019-08-09 20:55:00 +0800
categories: [Blogging, Tutorial]
tags: [games]
pin: false
---

## Creando el background

Primero crearemos el background en donde se movera nuestro **player**

```java
void setup() {

  size(600, 600);
  background(51); 
  frameRate(10);
}
void draw() {
}
```

![](https://lh3.google.com/u/0/d/1dJxCZmcJZppsQlw5hWwVFLF02NNM_daj=w962-h902-iv1)

ahora dibujaremos al **player** 

```java
int cellSize = 20;

ArrayList<PVector> snakeSegments = new ArrayList<PVector>();


void setup() {
  ...
  snakeSegments.add(new PVector(3, 1));
  snakeSegments.add(new PVector(2, 1));
  snakeSegments.add(new PVector(1, 1));
  
}
void draw() {
  for(PVector v : snakeSegments) {
      fill(150,255,40);
      rect((v.x-1)*cellSize, (v.y-1)*cellSize, cellSize-1, 			cellSize-1);
    }
}
```

Donde `cellSize` es el tamano de cada celda por donde se movera  el snake y `snakeSegments` es un `ArrayList` de objetos  tipo  `PVector`.

y ahora moveremos a nuestro player a la derecha.

```java
int gridXCount = 20;
int gridYCount = 15;
int cellSize = 20; 
int total = 0;
int x = 0;
int y = 0;

ArrayList<PVector> snakeSegments = new ArrayList<PVector>();


void setup() {

  size(600, 600);
 
  frameRate(10);
  snakeSegments.add(new PVector(3, 1));
  snakeSegments.add(new PVector(2, 1));
  snakeSegments.add(new PVector(1, 1));
  
}
void draw() {
  background(51);
  for(PVector v : snakeSegments) {
      fill(150,255,40);
      rect((v.x-1)*cellSize, (v.y-1)*cellSize, cellSize-1, 			cellSize-1);
    }
  if(total > 0){
    snakeSegments.add(new PVector(x, y));
  }
  
  PVector nextPosition = snakeSegments.get(0);
  float nextXPosition = nextPosition.x+1;
  float nextYPosition = nextPosition.y;
  snakeSegments.add(0,new PVector(nextXPosition, 				nextYPosition));
  snakeSegments.remove(3);
}
```

lo siguiente es mover a nuestro player en todas las direcciones

```java
int gridXCount = 20;
int gridYCount = 15;
int cellSize = 20; 
int total = 0;
int x = 0;
int y = 0;
String direccion = "right"; 

ArrayList<PVector> snakeSegments = new ArrayList<PVector>();


void setup() {

  size(600, 600);
 
  frameRate(7);
  snakeSegments.add(new PVector(3, 1));
  snakeSegments.add(new PVector(2, 1));
  snakeSegments.add(new PVector(1, 1));
  
}
void draw() {
  background(51);
  for(PVector v : snakeSegments) {
      fill(150,255,40);
      rect((v.x-1)*cellSize, (v.y-1)*cellSize, cellSize-1, 			cellSize-1);
    }
  if(total > 0){
    snakeSegments.add(new PVector(x, y));
  }
  
  PVector nextPosition = snakeSegments.get(0);
  float  nextXPosition = nextPosition.x;
  float nextYPosition = nextPosition.y;
  
  if(direccion == "right"){
    nextXPosition = nextXPosition + 1;
  }else if(direccion == "left"){
    nextXPosition = nextXPosition - 1;
  }else if(direccion == "down"){
    nextYPosition = nextYPosition + 1;
  }else if(direccion == "up"){
    nextYPosition = nextYPosition - 1;
  }
  
  snakeSegments.add(0,new PVector(nextXPosition, 				nextYPosition));
  snakeSegments.remove(3);
}
void keyPressed(){
  if(key == 'd'){
    direccion = "right";
  }else if(key == 'a'){
    direccion = "left";
  }else if(key == 's'){
    direccion = "down";
  }else if(key == 'w'){
    direccion = "up";
  }
  println(key);
}
```

como veran el codigo empieza a hacer cada vez mas largo y por ende corremos el riesgo que sea mas complicado encontrar un error, ademas hemos anadido una nueva funcion `keyPressed()` por que no empezar a reordenar todo en funciones.

```java
int gridXCount = 20;
int gridYCount = 15;
int cellSize = 20; 
//int total = 0;
int x = 0;
int y = 0;
float nextXPosition;
float nextYPosition;
String direccion = "right"; 

ArrayList<PVector> snakeSegments = new ArrayList<PVector>();


void setup() {
  size(600, 600);
  frameRate(7);
  snakeSegments.add(new PVector(3, 1));
  snakeSegments.add(new PVector(2, 1));
  snakeSegments.add(new PVector(1, 1));
}
void draw() {
  background(51);
  drawSnake();
  update();
  
}
void update(){
  PVector nextPosition = snakeSegments.get(0);
    nextXPosition = nextPosition.x;
    nextYPosition = nextPosition.y;
    direccion();
    snakeSegments.add(0,new PVector(nextXPosition, 					nextYPosition));
    snakeSegments.remove(3);
}
void drawSnake(){
    for(PVector v : snakeSegments) {
      fill(150,255,40);
      rect((v.x-1)*cellSize, (v.y-1)*cellSize, cellSize-1, 			cellSize-1);
    }
    snakeSegments.add(new PVector(x, y));
    
  /*if(total > 0){
    snakeSegments.add(new PVector(x, y));
  }
  */
}
void direccion(){
  if(direccion == "right"){
      nextXPosition = nextXPosition + 1;
    }else if(direccion == "left"){
      nextXPosition = nextXPosition - 1;
    }else if(direccion == "down"){
      nextYPosition = nextYPosition + 1;
    }else if(direccion == "up"){
      nextYPosition = nextYPosition - 1;
    }
}
void keyPressed(){
  if(key == 'd'){
    direccion = "right";
  }else if(key == 'a'){
    direccion = "left";
  }else if(key == 's'){
    direccion = "down";
  }else if(key == 'w'){
    direccion = "up";
  }
}
```

se puede mejorar pero por ahora si algo falla, sera mas facil debuggear el error. sigamos con nuestro juego, como ven nuetro pequeno player verde de pierde una vez tocamos algun borde de la pantalla de juego, algo tenemos que hacer para que esto no pase. 

```java
void direccion(){
  if(direccion == "right"){
      nextXPosition = nextXPosition + 1;
      if(nextXPosition > gridXCount){
        nextXPosition = 1;
      }
    }else if(direccion == "left"){
      nextXPosition = nextXPosition - 1;
      if(nextXPosition < 1){
        nextXPosition = gridXCount;
      }
    }else if(direccion == "down"){
      nextYPosition = nextYPosition + 1;
      if(nextYPosition > gridYCount){
        nextYPosition = 1;
      }
    }else if(direccion == "up"){
      nextYPosition = nextYPosition - 1;
      if(nextYPosition < 1){
        nextYPosition = gridYCount;
      }
    }
}
```

yei!! ahora nuestro amigo verde se ve un poco mejor, y gracias a las funciones no este post no se hara mas largo.

```java
PVector food;
```

```java
void foodLocation(){
  food = new PVector(random(1,gridXCount),random(1,gridYCount));
}
```

el anterior seria el codigo para definir la posicion del cuadrito parpadeante que servira para que nuestro player cresca, pero no es sufuciente para dibujarlo en la pantalla y que interactue con nuestro amigo verde.

```java
int gridXCount = 30;
int gridYCount = 30;
int cellSize = 20; 
//float x = 0;
//float y = 0;
float nextXPosition;
float nextYPosition;
String direccion = "right"; 
int total = 3;
PVector food;

ArrayList<PVector> snakeSegments = new ArrayList<PVector>();


void setup() {
  size(600, 600);
  frameRate(10);
  snakeSegments.add(new PVector(3, 1));
  snakeSegments.add(new PVector(2, 1));
  snakeSegments.add(new PVector(1, 1));
  foodLocation();
  println(snakeSegments.size());
  
}
void draw() {
  background(51);
  drawSnake();
  update();
  println(snakeSegments.size());
  
  if(eat()){
    foodLocation();
  }
  fill(255,0,100);
  rect((food.x -1)*cellSize,(food.y-1)*cellSize,cellSize-1,cellSize-1);

}
void update(){
    PVector nextPosition = snakeSegments.get(0);
    nextXPosition = nextPosition.x;
    nextYPosition = nextPosition.y;
    direccion();
    if(total > 0){
      if(total == snakeSegments.size() && !snakeSegments.isEmpty()){
        snakeSegments.remove(snakeSegments.size()-1);
      }
      snakeSegments.add(0,new PVector(nextXPosition, nextYPosition));
      //snakeSegments.add(new PVector(x, y));
    }
    
}
void drawSnake(){
    fill(150,255,40);
    for(PVector v : snakeSegments) {
      rect((v.x-1)*cellSize, (v.y-1)*cellSize, cellSize-1, cellSize-1);
    }  
}
void direccion(){
  if(direccion == "right"){
      nextXPosition = nextXPosition + 1;
      if(nextXPosition > gridXCount){
        nextXPosition = 1;
      }
    }else if(direccion == "left"){
      nextXPosition = nextXPosition - 1;
      if(nextXPosition < 1){
        nextXPosition = gridXCount;
      }
    }else if(direccion == "down"){
      nextYPosition = nextYPosition + 1;
      if(nextYPosition > gridYCount){
        nextYPosition = 1;
      }
    }else if(direccion == "up"){
      nextYPosition = nextYPosition - 1;
      if(nextYPosition < 1){
        nextYPosition = gridYCount;
      }
    }
}
void foodLocation(){
  food = new PVector(floor(random(1,gridXCount)),floor(random(1,gridYCount)));
  //food.mult(cellSize);
  
  fill(255,0,100);
  rect((food.x -1)*cellSize,(food.y-1)*cellSize,cellSize-1,cellSize-1);
  
}
boolean eat(){
  //float d = dist(x,y,pos.x,pos,y);
  if(nextXPosition == food.x && nextYPosition == food.y){
    total++;
    println(total);
    return true;
  }else{
    return false;
  }
}
void keyPressed(){
  if(key == 'd'){
    direccion = "right";
  }else if(key == 'a'){
    direccion = "left";
  }else if(key == 's'){
    direccion = "down";
  }else if(key == 'w'){
    direccion = "up";
  }
}
```

ahora nuestro juego se ve un poco mas descente y funcional, pero aun es aburrido porque no es posible perder.

```java
void death(){
    for(int i = 3; i < snakeSegments.size();i++ ){
    PVector pos = snakeSegments.get(i);
    if(nextXPosition == pos.x && nextYPosition == pos.y && i != snakeSegments.size() ){
      println("endgame");
      itsAlive = false;
    }
  }

```

debemos poner la funcion `death()` y agregarla a nuestro inicio

```java
void death(){
    for(int i = 3; i < snakeSegments.size();i++ ){
    PVector pos = snakeSegments.get(i);
    if(nextXPosition == pos.x && nextYPosition == pos.y && i != snakeSegments.size() ){
      println("endgame");
      delay(2000);
      itsAlive = false;
    }
  }
  if(itsAlive){
    drawSnake();
    update();
    if(eat()){
      foodLocation();
    }
  }
}
```

asi quedaria la funcion `death()` para que cuando nuestro player choque contra si mismo el juego se pause 2seg. Agregaremos tambien un cambio de color para que la muerte sea mas visible y que el juego se reinicie. Asi se veria nuestro codigo sin la pantallas de gameover y pantalla de inicio.

```java
int gridXCount = 30;
int gridYCount = 30;
int cellSize = 20; 
int x =150;
int y =255;
int z =40;
float nextXPosition;
float nextYPosition;
String direccion = "right"; 
int total = 3;
PVector food;
boolean itsAlive = true;

ArrayList<PVector> snakeSegments = new ArrayList<PVector>();

void setup() {
  size(600, 600);
  frameRate(15);
  snakeSegments.add(new PVector(3, 1));
  snakeSegments.add(new PVector(2, 1));
  snakeSegments.add(new PVector(1, 1));
  foodLocation();
  println(snakeSegments.size()); 
}
void draw() {
  background(51);
  println(snakeSegments.size());
  death();
  fill(255,0,100);
  rect((food.x -1)*cellSize,(food.y-1)*cellSize,cellSize-1,cellSize-1);
}
void update(){
    PVector nextPosition = snakeSegments.get(0);
    nextXPosition = nextPosition.x;
    nextYPosition = nextPosition.y;
    direccion();
    if(total > 0){
      if(total == snakeSegments.size() && !snakeSegments.isEmpty()){
        snakeSegments.remove(snakeSegments.size()-1);
      }
      snakeSegments.add(0,new PVector(nextXPosition, nextYPosition));
    } 
}
void drawSnake(int x,int y,int z){
    fill(x,y,z);
    for(PVector v : snakeSegments) {
      rect((v.x-1)*cellSize, (v.y-1)*cellSize, cellSize-1, 			cellSize-1);
    }  
}
void direccion(){
  if(direccion == "right"){
      nextXPosition = nextXPosition + 1;
      if(nextXPosition > gridXCount){
        nextXPosition = 1;
      }
    }else if(direccion == "left"){
      nextXPosition = nextXPosition - 1;
      if(nextXPosition < 1){
        nextXPosition = gridXCount;
      }
    }else if(direccion == "down"){
      nextYPosition = nextYPosition + 1;
      if(nextYPosition > gridYCount){
        nextYPosition = 1;
      }
    }else if(direccion == "up"){
      nextYPosition = nextYPosition - 1;
      if(nextYPosition < 1){
        nextYPosition = gridYCount;
      }
    }
}
void foodLocation(){
  food = new 												PVector(floor(random(1,gridXCount)),floor(random(1,gridYCount)));

  fill(255,0,100);
  rect((food.x -1)*cellSize,(food.y-1)*cellSize,cellSize-		1,cellSize-1);
}
boolean eat(){
  //float d = dist(x,y,pos.x,pos,y);
  if(nextXPosition == food.x && nextYPosition == food.y){
    total++;
    println(total);
    return true;
  }else{
    return false;
  }
}
void death(){
  for(int i = 3; i < snakeSegments.size();i++ ){
    PVector pos = snakeSegments.get(i);
    if(nextXPosition == pos.x && nextYPosition == pos.y && i != snakeSegments.size() ){
      println("endgame");
      delay(2000);
      itsAlive = false;
      reset();
    }
  }
  if(itsAlive){
    drawSnake(x,y,z);
    update();
    if(eat()){
      foodLocation();
    }
  }
}
void reset(){
  snakeSegments.clear();
  direccion = "right";
  snakeSegments.add(new PVector(3, 1));
  snakeSegments.add(new PVector(2, 1));
  snakeSegments.add(new PVector(1, 1));
  total = 3;
  itsAlive = true;
  foodLocation();
}
void keyPressed(){
  if(key == 'd'){
    direccion = "right";
  }else if(key == 'a'){
    direccion = "left";
  }else if(key == 's'){
    direccion = "down";
  }else if(key == 'w'){
    direccion = "up";
  }
}
```













[PVector]: https://processing.org/reference/PVector.html



