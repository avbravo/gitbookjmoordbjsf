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

## Interface composite

| Atributo | Descripción |
| :--- | :--- |
| value  |  |
| disabled default= false |  |
| multiple default= false |  |
| dropdown  default= false |  |
| minQueryLength   default= 1  |  |
| itemLabel |  |
| update |  |
| rendered |  |
| field |  |
| converter |  |
| columnpaneltip  default= 1 |  |
| labeltip1 |  |
| labeltip2 |  |
| labeltip3 |  |
| labeltip4 |  |
| labeltip5 |  |
| labeltip6 |  |
| fromstart default= true |  |
| required  default= false |  |
| size   default= 25 |  |
| listener      method-signature= void handleSelect\(org.primefaces.event.SelectEvent\)  |  |
| completeMethod method-signature= java.util.List complete\(java.lang.String\)  |  |

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

* ## Usaremos para generar múltiples roles para el usuario
* Multiple

* Dropdwon

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



