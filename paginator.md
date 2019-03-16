# &lt;jmoordb:paginator&gt;

![](/assets/pagi.png)

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

* Los movimientos entre las paginas las controlamos mediante los métodos siguientes.

```java
// <editor-fold defaultstate="collapsed" desc="last">
    @Override
    public String last() {
        try {
            page = rolRepository.sizeOfPage(rowPage);
            move();
        } catch (Exception e) {
            errorServices.errorMessage(nameOfClass(),nameOfMethod(), e.getLocalizedMessage());
        }
        return "";
    }// </editor-fold>
// <editor-fold defaultstate="collapsed" desc="first">

    @Override
    public String first() {
        try {
            page = 1;
            move();
        } catch (Exception e) {
            errorServices.errorMessage(nameOfClass(),nameOfMethod(), e.getLocalizedMessage());
        }
        return "";
    }// </editor-fold>
// <editor-fold defaultstate="collapsed" desc="next">

    @Override
    public String next() {
        try {
            if (page < (rolRepository.sizeOfPage(rowPage))) {
                page++;
            }
            move();
        } catch (Exception e) {
            errorServices.errorMessage(nameOfClass(),nameOfMethod(), e.getLocalizedMessage());
        }
        return "";
    }// </editor-fold>
// <editor-fold defaultstate="collapsed" desc="back">

    @Override
    public String back() {
        try {
            if (page > 1) {
                page--;
            }
            move();
        } catch (Exception e) {
            errorServices.errorMessage(nameOfClass(),nameOfMethod(), e.getLocalizedMessage());
        }
        return "";
    }// </editor-fold>
// <editor-fold defaultstate="collapsed" desc="skip(Integer page)">

    @Override
    public String skip(Integer page) {
        try {
            this.page = page;
            move();
        } catch (Exception e) {
            errorServices.errorMessage(nameOfClass(),nameOfMethod(), e.getLocalizedMessage());
        }
        return "";
    }// </editor-fold>
// <editor-fold defaultstate="collapsed" desc="move">

    @Override
    public void move() {
        try {

            Document doc;
            switch (loginController.get("searchrol")) {
                case "_init":
                case "_autocomplete":
                    rolList = rolRepository.findPagination(page, rowPage);

                    break;

                case "idrol":
                    if (lookupServices.getIdrol() != null) {
                        doc = new Document("idrol", lookupServices.getIdrol());
                        rolList = rolRepository.findPagination(doc, page, rowPage, new Document("idrol", -1));
                    } else {
                        rolList = rolRepository.findPagination(page, rowPage);
                    }

                    break;

                default:

                    rolList = rolRepository.findPagination(page, rowPage);
                    break;
            }

            rolFiltered = rolList;

            rolDataModel = new RolDataModel(rolList);

        } catch (Exception e) {
            errorServices.errorMessage(nameOfClass(),nameOfMethod(), e.getLocalizedMessage());
        }
    }// </editor-fold>
```

## Componente

```java
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
                <p:commandButton value="Sumar " action="#{rolController.suma(rolController.page)}"/>
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



