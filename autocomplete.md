# autocomplete

Genera autocomplete basados en &lt;p:autocomplete&gt; optimizados para jmoordb

* Permite dropdown
* Multiples 
* Simples
* Indicar desde que caracter iniciar la busqueda
* Mostrar todos

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

* simple desde un list.xhtml

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



