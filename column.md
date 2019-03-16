# &lt;jmoordbjsf:column/&gt;

* Genera una columna para un datatable con los botones edit o delete.
* Se usa dentro de un &lt;b:dataTableColumn/&gt;

```java
 <b:dataTableColumn label="">

                        <jmoordbjsf:column

                            edit="#{rolController.prepare('view',item)}"
                            delete="#{rolController.delete(item,false)}"
                            rendered="#{applicationMenu.rol.delete}"
                            />
  </b:dataTableColumn>

```



