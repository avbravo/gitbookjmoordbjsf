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

![](/assets/column.png)

* Contiene un dialogo de confirmación

![](/assets/congr.png)



## Ejemplo:

```java
 <b:panel id="dataTable" look="primary">
                <jmoordbjsf:paginator 
                    rowPage="#{rolController.rowPage}"
                    clear="#{rolController.clear()}"
                    first="#{rolController.first()}"
                    back="#{rolController.back()}"
                    next="#{rolController.next()}"
                    last="#{rolController.last()}"
                    page="#{rolController.page}"
                    pages="#{rolController.pages}"
                    skip="ajax:rolController.skip(rolController.page)" 
                    new="#{rolController.prepare('gonew',rolController.rol)}"
                    printAll="#{rolController.printAll()}"
                    />
                <b:dataTable value="#{rolController.rolDataModel}"
                             var="item"
                             id="dataTable2"
                             paginated="false"
                             onpage="console.log('page');">

                    <b:dataTableColumn value="#{item.idrol}" label="#{msg['field.idrol']}"/>
                    <b:dataTableColumn value="#{item.rol}" label="#{msg['field.rol']}" />
                    <b:dataTableColumn value="#{item.activo}" label="#{msg['field.activo']}" />

                    <b:dataTableColumn label="">

                        <jmoordbjsf:column

                            edit="#{rolController.prepare('view',item)}"
                            delete="#{rolController.delete(item,false)}"
                            rendered="#{applicationMenu.rol.delete}"
                            />
                    </b:dataTableColumn>

                </b:dataTable>
```





