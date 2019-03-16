# Clases como parámetros y métodos en el composite

A veces necesitamos pasar solo el nombre del controller o el entity a un composite y desde el invocar a métodos específicos que no serán pasados como parámetros.

Definimos los atributos

* controller
* bean 
* clear que es el método que deseamos invocar 
* Si el método necesita leer atributos lo podemos pasar  mediante &lt;f:attribute&gt;

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

* D**efiniciòn**

```java
 <b:commandButton   iconAwesome="fa-play"  
                               oncomplete="remoteshowall();"
                               action="#{cc.attrs.controller[cc.attrs.next]}" 
                               look="primary"
                              
                               update=":form:dataTable " >
                               <f:attribute name="page" value="#{cc.attrs.page}"/>
                              <f:attribute name="sizeOfPage" value="#{cc.attrs.sizeOfPage}"/>

                               </b:commandButton>
```

## 

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
 default public String next() {      
        try {
            Integer page= (Integer) UIComponent.getCurrentComponent(FacesContext.getCurrentInstance()).getAttributes().get("page");
            Integer sizeOfPage = (Integer) UIComponent.getCurrentComponent(FacesContext.getCurrentInstance()).getAttributes().get("sizeOfPage");

            if (page < sizeOfPage) {
                page++;
            }
            JsfUtil.warningDialog("IController.next", "page: " + page.toString());
            move(page);
        } catch (Exception e) {
            JsfUtil.errorDialog(nameOfMethod(), e.getLocalizedMessage());
        }
        return "";
    }
```



