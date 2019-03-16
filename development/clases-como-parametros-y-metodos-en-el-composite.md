# Clases como parámetros y métodos en el composite

A veces necesitamos pasar solo el nombre del controller o el entity a un composite y desde el invocar a métodos específicos que no serán pasados como parámetros.



Definimos los atributos

* controller
* bean 
* clear que es el método que deseamos invocar 

```java
 <composite:attribute name="controller" type="java.lang.Object"/> 
        
 <composite:attribute name="bean" type="java.lang.Object"/>
 
 <composite:attribute name="next"  default="next" />
      
```

## definición del action

```java
action="#{cc.attrs.controller[cc.attrs.next]}" 
```

```java

```

## Definiciòn

```java
    
            <b:commandButton   iconAwesome="fa-play"  
                               oncomplete="remoteshowall();"
                               action="#{cc.attrs.controller[cc.attrs.next]}" 
                               look="primary"
                               update=":form:dataTable " /> 
```





## Uso

Se puede observar que no se necesita pasar como parámetro el método next del Controller

```java
  <jmoordbjsf:paginatormove                   
                    controller="#{rolController}"     
                    bean="#{rolController.rol}"
                    />
```



## Controller o en la Interfaz

* Esta definido el método next\(\)

```java
public String next() {
        try {
           if (page < (rolRepository.sizeOfPage(rowPage))) {
                page++;
          }
            move(page);
        } catch (Exception e) {
            errorServices.errorMessage(nameOfClass(), nameOfMethod(), e.getLocalizedMessage());
        }
        return "";
    }// </editor-fold>
```



