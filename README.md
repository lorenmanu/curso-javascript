## ** Curso Para afianzar conceptos de javascript ** ##

Autor: Lorenzo Manuel Rosas Rodríguez

## Breve Descripción/Introducción Tiendas
Curso realizado de un tutorial cogido de internet para saber más y repasar JavaScript.

## DOM : Document Object Model
Necesario para saber como el código html y el código javascritp interectua entre si.

En la jerarquía de esta parte, cada parte del document web es un objeto que mantiene una relación jerárquica con el resto. Esto nos permitirá acceder a cada parte del document de manera precisa e inequívoca.

![img1](https://www.dropbox.com/s/vbmr1v4isg1yh2g/img1.png?dl=1)

Por lo tanto podemos decir que es una representación interna que el navegador crea cada vez que carga una página. El objeto **Window** será el padre de todos y el hijo de este será **Document**.

### Objeto Document, propiedades y métodos

Para verlo en profundidad partimos de la siguiente página web:

```
<!DOCTYPE html>
<html>
  <head>
    <title>Título</title>
    <meta charset="UTF-8">
    </head>

    <body>
      <h1> Cosas para hacer </h1>
      <ol id="listaTareas">
        <li> Terminar el guión </li>
        <li> Preparar los gráficos </li>
        <li> Grabar la primera parte </li>
        </ol>
        <p id="notasLista"> Asegúrate de    terminar antes de las nueve
        </p>
    </body>
</html>

```

Esta página web tendrá el siguiente aspecto:

![img2](https://www.dropbox.com/s/0di1c007un94agu/img2.png?dl=1)

El esquema que tendrá el DOM de esta página web será el siguiente:


![img3](https://www.dropbox.com/s/lnp3j1h9d6d8lc0/img3.png?dl=1)

Una propiedad importante del DOM es childnodes que devulve una array con los nodos hijos. El array es **vivo**, lo que significa que cualquier cambio que realice en los nodos se reflejará de manera automática en la lista. Vamos a ver esta propiedad trabajando sobre un elemento concreto de la página web, este es:

```

<ol id="listaTareas">
        <li> Terminar el guión </li>
        <li> Preparar los gráficos </li>
        <li> Grabar la primera parte </li>
</ol>

```
Examinaremos el elemento de la lista ordenada(**ol**), escribiremos una función que lea los nodos **childs** y que nos devuelve el número total de elementos en la lista. Para ello realizaremos un scritp, este puede estar en un archivo incrustado en la página html o puede estar en un archivo externo, como veremos en apartados siguientes.

Obtendremos la lista ordenda por el **identificador**. Recordamos que el identificador **id en html** sirve también para identificar un elemento para trabajar con el también en CSS. Como podemos ver, lo utilizaremos en javascript para identificarlo, y con ello acceder a él.

Llamamos al nodo hijo del **Window**( ventana del navegador) y le decimos que nos devuelva todos los elementos de la página que tengan como **id =listasTareas** .

```
<script>
  var elementoOl = document.getElementById("listasTareas");
</script>

```
Posteriormente accederemos a los nodos hijos del nodo seleccionado e implementaremos un bucle para contarlos. Contaremos solo los que formen parte de esa lista ordenada **NODE TYPE == 1** . **NODE TYPE** indicará el tipo de elemento seleccionado, como podemos ver en la siguiente imagen:

![img4](https://www.dropbox.com/s/0dqs7lslp840szn/img4.png?dl=1)

Podemos ver más información sobre **NODE TYPE** [aquí](https://developer.mozilla.org/es/docs/Web/API/Node/nodeType).

En este caso queremos saber si es un nodo hijo, y como podemos contrastar con la anterior imagen, podemos comprobar el motivo por el cual hemos puesto **NODE TYPE == 1** .

Con la anterior condición ignoramos los demás elementos que pueda tener la lista ordenada, y contaremos solo los que tengan la etiqueta ```<li>```:

```
<script>

  function contarListaItems(){
    var elementOl = document.getElemtById("listaTareas");
    var cuenta = 0;

    for(var i=0; i< elementOl.childNodes.length; ++i){
      if(elementOl.chilNodes[i].nodeType==1){
        ++cuenta;
      }
    }
  }

</script>

```

Finalmente, indicaremos usando el padre de la página **window**, que cargue dicha función cuando cargue la página web:

```
<script>

  ....

  window.onLoad = contarListaItems:

</script>

```

La pagina web global quedaría:

```
<!DOCTYPE html>
<html>
  <head>
    <title>Título</title>
    <meta charset="UTF-8">
    <script>

      function contarListaItems(){
        var elementOl = document.getElementById("listaTareas");
        var cuenta = 0;

        for(var i=0; i< elementOl.childNodes.length; ++i){
          if(elementOl.childNodes[i].nodeType==1){
            ++cuenta;
          }
        }

      function obtenerPrimerElemento(){
        var list = document.getElementById("listaTareas").firstChild.innerHTML;
        document.getElementById("demo").innerHTML=list;
      }
        function obtenerUltimo(){
          var list = document.getElementById("listaTareas").lastChild.innerHTML;
          document.getElementById("demo").innerHTML=list;
        }

        window.alert("Número de items --> " + cuenta);
      }

      window.onload = contarListaItems;

      window.alert("hola");

    </script>
  </head>

    <body>
      <h1> Cosas para hacer </h1>
      <ol id="listaTareas">
        <li> Terminar el guión </li>
        <li> Preparar los gráficos </li>
        <li> Grabar la primera parte </li>
        </ol>
        <p id="notasLista"> Asegúrate de    terminar antes de las nueve
        </p>
        <p id="primerElemento"> Primer elemento de la lista. </p>
        <button onclick="obtenerPrimerElemto()"> Obtener el primer elemento de la lista </button>
        <button onclick="obtenerUltimoElemento()"> Obtener el primer elemento de la lista </button>
    </body>
</html>

```

<ol> Podemos también seleccionar el primer y último elemento de un childNodes, la siguiente manera:

<li> Acceder al primer elemento de la lista:

```
<script>
  /*
    First child: es el primer elemento del ChilnNotes.
    innerHTML: accedemos a su contenido.
  */
  var list = document.getElementById("listaTareas").firstChild.innerHTML

```

</li>

<li> Acceder al último elemento de la lista:

```
<script>
  /*
    First child: es el primer elemento del ChilnNotes.
    innerHTML: accedemos a su contenido.
  */
  var list = document.getElementById("listaTareas").lastChild.innerHTML

```

</li>

Procederemos ahora con un ejemplo, en veremos como acceder a los elementos de un div mediante sus atributos,
la declaración del div es la siguiente:

```

<div id="example" title="informe"> Bloque a modificar con el botón </div>

```
Los hijos de los tres nodos lo podemos ver en la siguiente imagen:
