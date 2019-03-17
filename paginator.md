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
    
   
   
```

## sizeOfPage

```java
@Override
    public Integer sizeOfPage() {
     return rolRepository.sizeOfPage(rowPage);
    }/
```

## move\(Integer page\)

```java
 @Override
    public void move(Integer page) {
        try {
            this.page =page;
            System.out.println("llamo al move");
              JsfUtil.warningDialog("rolController.move", "page: "+page.toString());
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
            errorServices.errorMessage(nameOfClass(), nameOfMethod(), e.getLocalizedMessage());
        }
    }
```

## 

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



