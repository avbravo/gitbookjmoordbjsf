# autocomplete

Genera autocomplete basados en &lt;p:autocomplete&gt; optimizados para jmoordb

* Permite dropdown
* Multiples 
* Simples
* Indicar desde que caracter iniciar la busqueda
* Mostrar todos
* field: indicamos el campo que deseamos que se realice la busqueda
* Se muestran las etiquetas a desplegar
* Cuando lo usas desde un list.xhtml  el listener\(Generalmente queremos pasarlo a un  datatable\)

```
listener="#{rolController.handleAutocompleteOfListXhtml}"
```

* Cuando lo usas desde un new.xthml o view.xhtml \(seria el entity seleccionado\)

```
listener="#{rolController.handleSelect}"
```

```java

```

## Interface composite

```java
 <composite:interface >
        <composite:attribute name="value" />
        <composite:attribute name="disabled" default="false" />
        <composite:attribute name="multiple" default="false" />
        <composite:attribute name="dropdown"  default="false"/>
        <composite:attribute name="minQueryLength"  default="1"/>
        <composite:attribute name="itemLabel" />
        <composite:attribute name="update" />

        <composite:attribute name="rendered"/>
        <composite:attribute name="field"/>
        <composite:attribute name="converter"/>
          <composite:attribute name="columnpaneltip" default="1"/>
        <composite:attribute name="labeltip1" />

        <composite:attribute name="labeltip2" default=""/>
        <composite:attribute name="labeltip3" default=""/>
        <composite:attribute name="labeltip4" default=""/>
        <composite:attribute name="labeltip5" default=""/>
        <composite:attribute name="labeltip6" default=""/>

        <composite:attribute name="fromstart" default="true"/>
        <composite:attribute name="required" default="false" />
        <composite:attribute name="size"  default="25"/>
        <composite:attribute name="listener"  
                             method-signature="void handleSelect(org.primefaces.event.SelectEvent)" />
        <composite:attribute name="completeMethod"  
                            method-signature="java.util.List complete(java.lang.String)" />

    </composite:interface>
```

## Ejemplos

* ## Simple desde un list.xhtml

![](/assets/rol.png)

```java
  <p:outputLabel value="#{msg['field.idrol']}"/>
  <jmoordbjsf:autocomplete converter="#{rolConverter}"
                           completeMethod="#{rolController.rolServices.complete}"
                           labeltip1="#{msg['field.idrol']} #{p.idrol}"
                           labeltip2="#{msg['field.rol']} #{p.rol}" 
                           listener="#{rolController.handleAutocompleteOfListXhtml}"
                           value="#{rolController.rolSelected}"
                           itemLabel="#{p.idrol}"
                           field="idrol"
                           update=":form:dataTable"/>
```



## RolController.java

```java
 public void handleAutocompleteOfListXhtml(SelectEvent event) {
        try {
           rolList.removeAll(rolList);
            rolList.add(rolSelected);
            rolFiltered = rolList;
           rolDataModel = new RolDataModel(rolList);
            
            loginController.put("searchrol", "idrol");
            lookupServices.setIdrol(rolSelected.getIdrol());
        } catch (Exception e) {
            errorServices.errorMessage(nameOfClass(),nameOfMethod(), e.getLocalizedMessage());
        }
    }
```

### RolServices.java

```java
        List<Rol> suggestions = new ArrayList<>();
             try {
          suggestions=repository.complete(query);
        } catch (Exception e) {
            JsfUtil.errorMessage("complete() " + e.getLocalizedMessage());
        }

           return suggestions;
    }
```





## Ejemplo 2:

* ## Usaremos para generar múltiples roles para el usuario.

## ![](/assets/suu.png)

```java
<p:outputLabel  value="#{msg['field.rol']}" />
<jmoordbjsf:autocomplete converter="#{rolConverter}"
                       completeMethod="#{rolController.rolServices.complete}"
                       labeltip1="#{msg['field.idrol']} #{p.idrol}"
                       labeltip2="#{msg['field.rol']} #{p.rol}"   
                       listener="#{usuarioController.handleSelect}"
                       value="#{usuarioController.rolList}"
                       itemLabel="#{p.idrol}"
                       dropdown="true"
                       multiple="true"
                       required="true"
                       minQueryLength="0"
                       field="idrol"
                       />
```



## UsuarioController.java

```java
 public void handleSelect(SelectEvent event) {
        try {

        } catch (Exception e) {
            errorServices.errorMessage(nameOfClass(),nameOfMethod(), e.getLocalizedMessage());
        }
    }
```



