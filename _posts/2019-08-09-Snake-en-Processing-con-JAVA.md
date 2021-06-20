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
//size of the screen
  size(600, 600);
//color of the background
  background(51); 
//framerate of our game
  frameRate(10);
}
void draw() {
}
```

<img src="https://lh3.google.com/u/0/d/1dJxCZmcJZppsQlw5hWwVFLF02NNM_daj=w1920-h942-iv1" style="zoom:50%"/>

Ahora dibujaremos al **player** 

```java
//size of cell
int cellSize = 20;

//ArrayList for store the segments of our snake
ArrayList<PVector> snakeSegments = new ArrayList<PVector>();


void setup() {
  ...
      
  //add elements to our ArrayList    
  snakeSegments.add(new PVector(3, 1));
  snakeSegments.add(new PVector(2, 1));
  snakeSegments.add(new PVector(1, 1));
  
}
void draw() {
  //elements of player
  for(PVector v : snakeSegments) {
      //color of player
      fill(150,255,40);
      //draw a rect
      rect((v.x-1)*cellSize, (v.y-1)*cellSize, cellSize-1,cellSize-1);
    }
}
```

<img src="https://lh3.google.com/u/0/d/1CUETKmXlt2Pa7ZAKaQjlIEPe9XXxSbvt=w1485-h942-iv1" style="zoom:50%" />

Donde `cellSize` es el tamano de cada celda por donde se movera  el snake y `snakeSegments` es un `ArrayList` de objetos  tipo  `PVector`.

Y ahora tenemos que hacer que nuestro player se mueva por nuestra pantalla, por ahora solo se movera a la derecha, pero aun no responde a nuestras ordenes.

Recuerda que movimos el `background(51)` de la funcion `setup()` a la funcion `draw()`.

```java
int cellSize = 20; 

ArrayList<PVector> snakeSegments = new ArrayList<PVector>();

void setup() {

  size(600, 600);
  //we move background to draw()
  frameRate(10);
  //add elements to our ArrayList
  ...
  
}
void draw() {
  background(51);
  //elements of the player
  ...
    }

  PVector nextPosition = snakeSegments.get(0);
  float nextXPosition = nextPosition.x+1;
  float nextYPosition = nextPosition.y;
  snakeSegments.add(0,new PVector(nextXPosition,nextYPosition));
  snakeSegments.remove(3);
}
```

<img src="https://lh3.google.com/u/0/d/1lIXN2hSM2mM2AJQtp8TLdPURIFM24YOe=w958-h910-iv1" style="zoom:50%" />

lo siguiente es mover a nuestro player en todas las direcciones

```java
int cellSize = 20; 
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
      rect((v.x-1)*cellSize, (v.y-1)*cellSize, cellSize-1, cellSize-1);
    }

  //get the head of our player
  PVector nextPosition = snakeSegments.get(0);
  float  nextXPosition = nextPosition.x;
  float nextYPosition = nextPosition.y;
  
  //update our var direccion
  if(direccion == "right"){
    nextXPosition = nextXPosition + 1;
  }else if(direccion == "left"){
    nextXPosition = nextXPosition - 1;
  }else if(direccion == "down"){
    nextYPosition = nextYPosition + 1;
  }else if(direccion == "up"){
    nextYPosition = nextYPosition - 1;
  }
  
  snakeSegments.add(0,new PVector(nextXPosition, nextYPosition));
  snakeSegments.remove(3);
}
//check the key that is pressed
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

<img src="https://lh3.google.com/u/0/d/1ISNu1nSUh9_exBqUBI2ZGssVUAdqFgR4=w657-h930-iv1" style="zoom:50%" />

El código empieza a hacer cada vez más largo y por ende corremos el riesgo que sea más complicado encontrar un error, además hemos añadido una nueva función `keyPressed()` . Por qué no empezar a reordenar todo en funciones.

```java
int cellSize = 20; 
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
    snakeSegments.add(0,new PVector(nextXPosition,  nextYPosition));
    snakeSegments.remove(3);
}
void drawSnake(){
    for(PVector v : snakeSegments) {
      fill(150,255,40);
      rect((v.x-1)*cellSize, (v.y-1)*cellSize, cellSize-1, cellSize-1);
    }
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

El código anterior tiene mucho que mejorar, pero por ahora si algo falla, será mas fácil debuggear el error. Sigamos con nuestro juego, como ven nuestro pequeño player verde deja de ser visible una vez tocamos algún borde de la pantalla de juego, algo tenemos que hacer para que esto no pase. No olvidar que para que la función `dirección()` funcione hay que mandarla llamar y las variables `gridXCound` y `gridYCound` serán colocadas como globales.

```java
int gridXCount = 30;
int gridYCount = 30;
```

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

<img src="https://lh3.google.com/u/0/d/1MLDAt2Lsy2sr4MhxvW5hlxoVPwzusww_=w657-h930-iv1" style="zoom:50%" />

Yei!! ahora nuestro amigo verde se ve un poco mejor, y gracias a las funciones no esté post no se hará más largo. Ahora falta poner nuestro item.

```java
PVector food;
```

```java
void setup(){
...
	foodLocation();
}
```

```java
void draw(){
...
  fill(255,0,100);
  rect((food.x -1)*cellSize,(food.y-1)*cellSize,cellSize-1,cellSize-1);
}
```

```java
void foodLocation(){
  food = new PVector(random(1,gridXCount),random(1,gridYCount));
}
```

El anterior seria el código para definir la posición del ítem parpadeante que servirá para que nuestro player crezca, pero no es suficiente para dibujarlo en la pantalla y que interactúe con nuestro amigo verde.

<img src="https://lh3.google.com/u/0/d/1ELcfuweKm5NVmK6wv-vSd9UfKchcExnb=w652-h910-iv1" style="zoom:50%" />

Entonces tenemos que hacer que cada vez que nuestro snake se coma el ítem el largo del snake crezca, específicamente cuando la coordenada del elemento `snakeSegments.get(0)` y la coordenada generada por `foodLocation()` sean iguales. Así se verá el código hasta ahora con todos los cambios hechos.

```java
int gridXCount = 30;
int gridYCount = 30;
int cellSize = 20; 
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
}
boolean eat(){
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

<img src="https://lh3.google.com/u/0/d/172mC6C3qdu0D6I0NJDWq5g10hWzX4aC3=w523-h555-iv1" style="zoom:50%" />

Ahora nuestro juego se ve un poco más decente y funcional, pero aun es aburrido porque no es posible perder, debemos solucionar eso, entonces creamos nuestra función `death()`. Debemos poner la función `death()` y agregarla a nuestro inicio.

```java
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
    drawSnake(colorx,colory,colorz);
    update();
    if(eat()){
      foodLocation();
    }
  }
}
```

Así quedaría nuestro código completo ya con la función `death()` para que cuando nuestro player choque contra si mismo el juego se pause 2seg. Así como también el reinicio del juego. Así se vería nuestro código sin la pantallas de gameover y pantalla de inicio.

```java
int gridXCount = 30;
int gridYCount = 30;
int cellSize = 20; 
int colorx =150;
int colory =255;
int colorz =40;
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
void drawSnake(int colorx,int colory,int colorz){
    fill(colorx,colory,colorz);
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
    drawSnake(colorx,colory,colorz);
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

Podemos agregar también solo para que este un poco más completo una pantallita que simula cuantos puntos hemos generado.

Como actividad puedes intentar que los puntajes funcionen correctamente.

```java
void Scoreboard(){
  fill(250, 250, 250);
  textSize(30);
  text( "Snake Game", width/2.8, 30);
  fill(250, 250, 250);
  textSize(15);
  text( "By: ethel", width/2.8, 50);
  
  fill(250, 250, 250);
  textSize(17);
  text( "Score: " + total, 30, 30);
  
  fill(250, 250, 250);
  textSize(17);
  text( "High Score: " + total, 30, 50);
}
```



[PVector]: https://processing.org/reference/PVector.html

