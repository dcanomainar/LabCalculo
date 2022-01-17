# Laboratorio: Cálculo computacional

[TOC]

## 0. Preparación del Laboratorio

La interfaz de Matlab se divide en distintas vistas:
* Consola de comandos (Command Window): Nos permite realizar cálculos directamente
* Workspace

Le vamos a New Script para crear un nuevo fichero Matlab donde vamos a escribir 

## 1. Generar puntos y pintarlos

En el primer script, vamos a ver como pintar una gráfica a trozos.
Para ello definiremos nuestras funciones:

```matlab
f(x) = tan(x) si  -pi/4 <= x <= pi/4
f(x) = cos(x-pi/4) si  pi/4 <= x <= pi/2
f(x) = exp(x) si  pi/2 <= x <= 3 
```

Primero vamos a pintarla generando los valores en una tabla y después pintándolos.
Es decir, generamos una lista de números entre dos valores con el paso que consideremos:

```matlab
x1=-pi/4:pi/200:pi/4;
```

Esta lista irá entre -pi/4 y pi/4 con un salto de pi/200

El punto y coma nos permite que no se vea la salida de ejecución. Si lo quitamos se vería:
{Insertar foto 1}

Después calculamos la y en función de nuestra x1:

```matlab
y1=tan(x1);
```

El otro trozo de función lo generaremos con:

```matlab
x2=pi/4:pi/200:pi/2;
y2=cos(x2-pi/4);
```

También podemos trabajar con linspace que nos permite generar los puntos entre 2 valores (pi/2 y 3):

```matlab
x3=linspace(pi/2,3);
y3=exp(x3);
```

En este caso generaría lo mismo, pero lo haría de forma lineal.

Finalmente, para dibujarlos unimos en un único rango todas las variables y utilizamos la función plot:

```matlab
x=[x1,x2,x3];
y=[y1,y2,y3];
plot(x,y)
```

Con lo que veremos:

{Insertar foto 2}

Lo que veremos es que en la primera zona pinta una tangente, en la segunda zona un coseno y en el tercer trozo una exponencial.

A simple vista parece que es continua, pero si pintamos de manera independiente cada una de las partes, es decir:

```matlab
plot(x1,y1,"b")
hold on
plot(x2,y2,"g")
hold on
plot(x3,y3,"r")
```

Lo que veremos es que la función es discontinua:

{Insertar foto 3}

Esto lo vemos así gracias a la función "hold on", que es la que evita que se vea todo como si estuviese unido.

## 2. Trabajo con variables simbólicas

Ahora vamos a utilizar variables simbólicas en Matlab.

Para ello vamos a trabajar con una librería de Matlab que permite trabajar con cálculo simbólico:

```matlab
syms x
```

Esto le indica que a partir de ahora la x la utilice como una variable

Vamos a definir nuestra función:

```matlab
y = sin(x) + x^2 + 5
```

Que será lo mismo que:

{Insert latex code for function}

Como podemos observar Matlab nos la representa automáticamente:

{Insert image 4}

Y como vemos, para represeentarlo es más sencillo ya que le pasamos la función y le indicamos el rango en el que queremos que lo dibuje:

```matlab
ezplot(y, [-2,2])
```

Y nos mostrará lo siguiente:

{Insert image 5}

Si nosotros la definiésemos entre 100 y -100, veríamos que la función tiene una forma más de parábola:

{insert image 6}

También podemos simplificar automáticamente funciones.

Podemos definir la siguiente función:

```matlab
y = sin(x)^2+cos(x)^2
```

Y al usar la función simplify de la siguiente forma:

```matlab
simplify(y)
```

Nos devolverá:

{insert image 7}

También podemos derivar de la siguiente forma:

```matlab
y = (3*x^2+5)*cos(x)^2
diff(y)
```

Y como resultado obtenemos:

{insert image 8}

Si queremos, podemos hacer también directamente la segunda derivada:

```matlab
y=3*x^3+5*x^2+6
diff(y,2)
```

Lo cuál nos quedará como:

{insert image 9}

Por último, podemos trabajar con límites:

En este primer caso vamos a hacer que el límite tienda a 0

```matlab
y = sin(x)/x
limit(y,x,0)
```

Como resultado tendremos:

{insert image 10}

En este segundo caso vamos a hacer que el límite tienda a infinito:

```matlab
y = (5*x +3)/(2*x+4)
limit(y,x,inf)
```

Como resultado tendremos:

{insert image 11}

## 3. Cálculo de asíntotas

Definimos la siguiente función y la dibujamos entre 10 y -10:

```matlab
y = (x^2+2*x-1)/x
ezplot(y,[-10,10])
```

Como resultado tendremos:

{insert image 12}

Para calcular las asíntotas de esta recta. Para ello habría que dividir por x y calcular el límite:

```matlab
y1 = (x^2+2*x-1)/x^2
mp = limit(y1,x,inf)
```

También se puede calcular cuando el límite tiende a -infinito:

```matlab
mn = limit(y1,x,-inf)
```

Como ambos resultados obtendremos:

{insert image 13}

Para calcular la ordenada:

```matlab
y2 = (x^2+2*x-1)/x -x
np = limit(y2,x,inf)
nn = limit(y2,x,-inf)
```

Obtendremos:

{insert image 14}

Finalmente calculamos la asíntota oblicua y la representamos:

```matlab
yasin = mp*x +np
ezplot(y,[-10,10])
hold on
ezplot(yasin,[-10,10])
```

{insert image 15}

También podemos calcularlas por la derecha y por la izquierda:

```matlab
limit(y,x,0,'left')
```

{insert image 16}

```matlab
limit(y,x,0,'right')
```

{insert image 17}

Como vemos tiene una asíntota horizontal, pero ninguna vertical.

## 4. Estudio de una función

Vamos a estudiar la siguiente función y la dibujamos entre 20 y -20:

```matlab
y = x/(1+x^2)
ezplot(y,[-20,20])
```

Lo que nos dará:

{insert image 18}

Ahora vamos a estudiar los máximos y mínimos. Para ello vamos a derivar la función y que nos la simplifique:

```matlab
y1 = simplify(diff(y))
```

Esto nos dará:

{insert image 19}

Ahora la vamos a igualar a 0 y ver que valores tiene:

```matlab
max_min = solve(y1)
```

Y nos devolverá dos valores en forma de vector:

{insert image 20}

Para comprobar si son máximos o mínimos, hacemos la segunda derivada:

```matlab
y2 = simplify(diff(y,2))
```

Como resultado tenemos:

{insert image 21}

Y pedir que nos los muestre:

{insert image 22}

Si queremos los puntos críticos:

```matlab
puntos_criticos_x = solve(y2)
punto_criticos_y = subs(y,puntos_criticos_y)
```

{insert image 23}
{insert image 24}

Vamos ahora a ver si es concava o convexa.

Para ello vamos a ver que ocurre en cada uno de los puntos críticos

* Entre - infintito y raiz de 3

```matlab
subs(y2,-5)
```

Como resultado tenemos:

{insert image 25}

Al darnos un valor negativo, sabemos que la función es convexa

* Entre -raiz 3 y 0

```matlab
subs(y2,-0.5)
```

Como resultado tenemos:

{insert image 26}

Nos da un valor mayor que 0, por lo que es cóncava

* Entre 0 y raíz de 3:

```matlab
subs(y2,0.5)
```

Como resultado tenemos:

{insert image 27}

Vuelve a pasar a convexa

* Entre sqrt 3 y infinito

```matlab
subs(y2,5)
```

Como resultado tenemos:

{insert image 28}

Vuelve a cóncava