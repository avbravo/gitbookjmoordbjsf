# Clases como parámetros y métodos en el composite

* Invocando métodos definidos en la interface.

* A veces necesitamos pasar solo el nombre del controller o el entity a un composite y desde el invocar a métodos específicos que no serán pasados como parámetros.

Definimos los atributos

* controller

* Si el método necesita leer atributos lo podemos pasar  mediante &lt;**f:attribute&gt;**
* en esos métodos los obtenemos

```java
 <composite:attribute name="controller" type="java.lang.Object"/> 


 <composite:attribute name="next"  default="next" />
```

## definición del action

```java
action="#{cc.attrs.controller[cc.attrs.next]}"
```

```java

```



## Componente paginator

```java
<?xml version='1.0' encoding='UTF-8' ?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:f="http://java.sun.com/jsf/core"
      xmlns:p="http://primefaces.org/ui"
      xmlns:composite="http://java.sun.com/jsf/composite"
      xmlns:b="http://bootsfaces.net/ui"
      xmlns:c="http://xmlns.jcp.org/jsp/jstl/core"
      xmlns:h="http://xmlns.jcp.org/jsf/html">
    <composite:interface >

        <composite:attribute name="controller" type="java.lang.Object"/> 

          <composite:attribute name="sizeOfPage" default="25" />
        <composite:attribute name="page" />
        <composite:attribute name="rowPage" default="25" />

        <composite:attribute name="pages" type="java.util.List" />

        <composite:attribute name="skip" />
        <composite:attribute name="renderednew" default="true"/>
        <composite:attribute name="renderedClear" default="true"/>
        <composite:attribute name="renderedPrint" default="true"/>

        <composite:attribute name="clear"  default="clear" />
        <composite:attribute name="first" default="first"/>
        <composite:attribute name="back" default="back" />
        <composite:attribute name="next" default="next" />
        <composite:attribute name="last" default="last" />
        <composite:attribute name="new" 
                             method-signature="java.lang.String action()" />


        <composite:attribute name="printAll" default="printAll" />


    </composite:interface>
    <composite:implementation>



       
        <b:panel>   

            <p:remoteCommand  update=":form:dataTable :form:content "
                              name="remoteshowall" />
            <p:remoteCommand  update=":form:content"
                              name="remotecontent" />

 <b:commandButton   iconAwesome="fa-step-backward" 
                               styleClass="ui-priority-primary"
                               look="primary"
                               oncomplete="remoteshowall();"
                               action="#{cc.attrs.controller[cc.attrs.first]}"
                               update=":form:dataTable " > 

            </b:commandButton>


            <b:commandButton   iconAwesome="fa-caret-left" 
                               styleClass="ui-priority-primary"
                               look="primary"
                               oncomplete="remoteshowall();"
                               action="#{cc.attrs.controller[cc.attrs.back]}"
                               update=":form:dataTable " > 
                <f:attribute name="page" value="#{cc.attrs.page}"/>
            </b:commandButton>

            <b:commandButton   iconAwesome="fa-play"  
                               oncomplete="remoteshowall();"
                               action="#{cc.attrs.controller[cc.attrs.next]}" 
                               look="primary"
                               update=":form:dataTable " > 
                <f:attribute name="page" value="#{cc.attrs.page}"/>
                <f:attribute name="sizeOfPage" value="#{cc.attrs.sizeOfPage}"/>
            </b:commandButton>

            <b:commandButton  iconAwesome="fa-step-forward"  
                              oncomplete="remoteshowall();"
                              look="primary"
                              action="#{cc.attrs.controller[cc.attrs.last]}"  
                              update=":form:dataTable " > 
                        <f:attribute name="page" value="#{cc.attrs.page}"/>
                <f:attribute name="sizeOfPage" value="#{cc.attrs.sizeOfPage}"/>
            </b:commandButton>

           <b:selectOneMenu id="pages"

                             value="#{cc.attrs.page}"                                                  
                             colMd="1"
                             onchange="#{cc.attrs.skip}"
                             oncomplete="remoteshowall();"
                             update=":form:dataTable" 
                             >

                <f:selectItems  value="#{cc.attrs.pages}" />

            </b:selectOneMenu> 

            <b:commandButton iconAwesome="fa-plus"  
                             action="#{cc.attrs.new}"
                             look="primary"
                             rendered="#{cc.attrs.renderednew}"
                             oncomplete="remotecontent()"
                             > 

            </b:commandButton>



            <b:commandButton iconAwesome="fa-print"                                                                                                         
                             title="#{app['button.print']}"    
                             rendered="#{cc.attrs.renderedPrint}"  
                             action="#{cc.attrs.controller[cc.attrs.printAll]}"  
                             ajax="false"
                             look="primary"
                             style="width:60px"/> 


            <b:commandButton  iconAwesome="fa-list-alt"                                                
                              action="#{cc.attrs.controller[cc.attrs.clear]}"     
                              rendered="#{cc.attrs.renderedClear}"    
                              look="primary"
                              title="#{app['button.all']}"
                              update=":form:dataTable :form:content"
                              oncomplete="remoteshowall()"
                              > 
                <f:ajax />
            </b:commandButton>

             <b:selectOneMenu colMd="1"
                             value="#{cc.attrs.rowPage}"
                             onchange="#{cc.attrs.skip}"
                              oncomplete="remoteshowall();"
                             update=":form:dataTable" 
                >

                <f:selectItem itemLabel="#{app['rows.l25']}" itemValue="25" />
                <f:selectItem itemLabel="#{app['rows.l15']}" itemValue="15" />
                <f:selectItem itemLabel="#{app['rows.l10']}" itemValue="10" />
                <f:selectItem itemLabel="#{app['rows.l5']}" itemValue="5" />
                <f:selectItem itemLabel="#{app['rows.l40']}" itemValue="40" />

            </b:selectOneMenu>
        </b:panel>
    </composite:implementation>

</html>
```

## Llamado desde el xhtml

```java
 <jmoordbjsf:paginator
                    controller="#{rolController}"     
                    sizeOfPage="#{rolController.sizeOfPage()}"
                    rowPage="#{rolController.rowPage}"                   
                    page="#{rolController.page}"
                    pages="#{rolController.pages}"
                    skip="ajax:rolController.skip(rolController.page)" 
                    new="#{rolController.prepare('gonew',rolController.rol)}"
                    />
```

La implementacion anterior usaba todos estos parámetros.

* se necesitaban pasar los métodos firts, back, next,last, printAll,clear
* No es necesario se invocan automáticamente desde el componente paginator

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
```

## CONTROLLER

* Se elminaron los metodos
* firts
* next
* last

Estos tiene el codigo para controlar el desplazamiento entre las paginas.

public class RolController implements Serializable, IController {

}

# INTERFAZ

```java
/*
* To change this license header, choose License Headers in Project Properties.
* To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package com.avbravo.store.controller.interfaces;

import com.avbravo.jmoordbutils.JsfUtil;
import java.util.Map;
import javax.faces.component.UIComponent;
import javax.faces.context.FacesContext;

/**
 *
 * @authoravbravo
 */
public interface IController<T> {

    public String preRenderView(String action);

    default public String refresh() {
        return "";
    }

    public String isNew();

    public void reset();

    public String showAll();

    public String save();

    public String edit();

    public String delete(Object item, Boolean deleteonviewpage);

    public String deleteAll();

    public String print();

    public String printAll();

    public String clear();

    // <editor-fold defaultstate="collapsed" desc="last">

    default public String last() {
        try {
              Integer page= 0;
            Integer sizeOfPage = (Integer) UIComponent.getCurrentComponent(FacesContext.getCurrentInstance()).getAttributes().get("sizeOfPage");

            page = sizeOfPage;
            move(page);
        } catch (Exception e) {
           JsfUtil.errorDialog(nameOfMethod(), e.getLocalizedMessage());
        }
        return "";
    }// </editor-fold>

  // <editor-fold defaultstate="collapsed" desc="first">


   default public String first() {
        try {
          Integer  page = 1;
            move(page);
        } catch (Exception e) {
           JsfUtil.errorDialog(nameOfMethod(), e.getLocalizedMessage());
        }
        return "";
    }// </editor-fold>

     // <editor-fold defaultstate="collapsed" desc="next">
    default public String next() {      
        try {
            Integer page= (Integer) UIComponent.getCurrentComponent(FacesContext.getCurrentInstance()).getAttributes().get("page");
            Integer sizeOfPage = (Integer) UIComponent.getCurrentComponent(FacesContext.getCurrentInstance()).getAttributes().get("sizeOfPage");

            if (page < sizeOfPage) {
                page++;
            }
            JsfUtil.warningDialog("IController.next", "page: " + page.toString());
            move(page);
        } catch (Exception e) {
            JsfUtil.errorDialog(nameOfMethod(), e.getLocalizedMessage());
        }
        return "";
    }// </editor-fold>



     // <editor-fold defaultstate="collapsed" desc="back">
   default public String back() {
        try {
              Integer page= (Integer) UIComponent.getCurrentComponent(FacesContext.getCurrentInstance()).getAttributes().get("page");

            if (page > 1) {
                page--;
            }
            move(page);
        } catch (Exception e) {
             JsfUtil.errorDialog(nameOfMethod(), e.getLocalizedMessage());
        }
        return "";
    }// </editor-fold>

    public String skip(Integer page);

    // <editor-fold defaultstate="collapsed" desc="skip(Integer page)">


//   default public String skip() {
//        try {
//              Integer page= (Integer) UIComponent.getCurrentComponent(FacesContext.getCurrentInstance()).getAttributes().get("page");
//            move(page);
//        } catch (Exception e) {
//           JsfUtil.errorDialog(nameOfMethod(), e.getLocalizedMessage());
//        }
//        return "";
//    }// </editor-fold>

    public void move(Integer page);

    public String searchBy(String field);

    public default String nameOfClassAndMethod() {
        final StackTraceElement e = Thread.currentThread().getStackTrace()[2];
        final String s = e.getClassName();
        return s.substring(s.lastIndexOf('.') + 1, s.length()) + "." + e.getMethodName();
    }

    public default String nameOfClass() {
        final StackTraceElement e = Thread.currentThread().getStackTrace()[2];
        final String s = e.getClassName();
        return s.substring(s.lastIndexOf('.') + 1, s.length());
    }

    public default String nameOfMethod() {
        final StackTraceElement e = Thread.currentThread().getStackTrace()[2];
        final String s = e.getClassName();
        return e.getMethodName();
    }


   public Integer sizeOfPage();

}
```



