# calendar

* Define un &lt;p:calendar&gt; optimizado para jmoordb.

![](/assets/pc.png)

## Composite

```java
    <composite:interface >


        <composite:attribute name="id" />
        <composite:attribute name="value" />
        <composite:attribute name="label"/>
        <composite:attribute name="mindate" default=""/>
        <composite:attribute name="mode" default="popup"/>
        <composite:attribute name="required"/>
        <composite:attribute name="update" default=""/>
        <composite:attribute name="disabled" default="false"/>

        <composite:attribute name="selectOtherMonths" default="true"/>
        <composite:attribute name="showTodayButton" default="true"/>
        <composite:attribute name="navigator" default="true"/>
        <composite:attribute name="pattern" default="dd/MM/yyyy" />
        <composite:attribute name="listener"  
                             method-signature="void handleSelect(org.primefaces.event.SelectEvent)" />
    </composite:interface>
```



## Ejemplo:

```java
 <jmoordbjsf:calendar 
             pattern="dd/MM/yyyy HH:mm a" value="#{viajeController.viaje.fechahorafinreserva}"    
             label="#{msg['field.fechahorafinreserva']}" 
             listener="#{viajeController.handleSelect}"
             update=":form:vehiculo, :form:conductor, :form:msg"/>

```

* Podemos usar un evento en ViajeController.java

```java
public void handleSelect(SelectEvent event) {
        try {
            viajeServices.isValidDate(viaje);

        } catch (Exception e) {
            errorServices.errorMessage(nameOfClass(), nameOfMethod(), e.getLocalizedMessage());
        }
    }// <
```



