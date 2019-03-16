# &lt;jmoordb:paginator&gt;

* Controla la paginacion para un datatable
* Se debe desabilitar la paginaciòn en el componente datatable
* Se debe indicar la cantidad de filas por pagina 
* Llevar el control de la pagina actual

```java
  Integer page = 1;
  Integer rowPage = 25;
```

* Cuando se crea el método set/get de page debe devolver el numero de documentos en la coleccion

```java
public List<Integer> getPages() {

        return rolRepository.listOfPage(rowPage);
}
```

![](/assets/pagi.png)





