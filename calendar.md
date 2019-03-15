# calendar

* Define un &lt;p:calendar&gt; optimizado para jmoordb.

![](/assets/pc.png)

## Atributos

| Atributo | Descripción |
| :--- | :--- |
| id |  |
| value  |  |
| label |  |
| mindate  |  |
| mode default=popup |  |
| required |  |
| update  |  |
| disabled default=false |  |
| selectOtherMonths default=true |  |
| showTodayButton default=true |  |
| navigator default=true |  |
| pattern default=dd/MM/yyyy  |  |
| listener | method-signature=void handleSelect\(org.primefaces.event.SelectEvent\)  |



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



