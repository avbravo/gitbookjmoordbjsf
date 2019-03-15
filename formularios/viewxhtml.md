# view.xhtml

* Se usa para la edición de los datos, se llama desde un list.xtml
* No influye que se use un atributo por llave primaria o no, ya que se invoca desde un list.xhtml

# Esquema

```java
<?xml version='1.0' encoding='UTF-8' ?>
<!DOCTYPE html>
<ui:composition template="/layout/template.xhtml" 
                xmlns="http://www.w3.org/1999/xhtml"
                xmlns:h="http://java.sun.com/jsf/html"
                xmlns:f="http://java.sun.com/jsf/core"
                xmlns:b="http://bootsfaces.net/ui"
                xmlns:ui="http://java.sun.com/jsf/facelets"
                xmlns:p="http://primefaces.org/ui"
                xmlns:jmoordbjsf="http://jmoordbjsf.com/taglib">
    <ui:define name="content">
        <!--<h:outputStylesheet library="bsf" name="css/thumbnails.css"/>-->

        <style>
            .thumbnail { max-width: 100%; }
            img.thumbnail:hover, img.thumbnail:focus {
                border: 1px solid;
                border-color: #428BCA;
            }
        </style>

         <b:form id="form"  prependId="false"  rendered="" onkeypress="if (event.keyCode == 13) {
                    return false;
                }">
            <h:panelGroup id="content" layout="block"> 

                <jmoordbjsf:messages id="msg"/>
                <b:panel title="#{msg['titleview.rol']}"  look="primary">
                    <b:panelGrid id="panel" colSpans="2,10" size="xs" rendered=""> 

                       //AGREGUE LOS COMPONENTES AQUI


                    </b:panelGrid>
                    <jmoordbjsf:toolbarview 
                       
                        />
                </b:panel>
            </h:panelGroup>
        </b:form>
 <jmoordbjsf:denegado renderedcondition="" />
        <br/><br/><br/>
    </ui:define>
</ui:composition>
```



