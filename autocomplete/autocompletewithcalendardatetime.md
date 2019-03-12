# autocompleteWithCalendarDateTime

\* Se usa para mostrar un par de Date y Time hasta 6 elementos en esa secuencia

\* Despliega el primer calendar como Date dd/MM/yyyy

\* Despliega el siguiente como Time  HH:mm:ss a

* Combinaciones: Date/Time Date/Time Date/Time

\* Se debe pasar columnpaneltip= 2 para que muestre el labely el valor



# Interfaz composite

```java
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
        <composite:attribute name="labelvalue1" default=""/>
        <composite:attribute name="labelvalue2" default=""/>
        <composite:attribute name="labelvalue3" default=""/>
        <composite:attribute name="labelvalue4" default=""/>
        <composite:attribute name="labelvalue5" default=""/>
        <composite:attribute name="labelvalue6" default=""/>


        <composite:attribute name="calendardatelabel1" default=""/>
        <composite:attribute name="calendardatelabel2" default=""/>
        <composite:attribute name="calendardatelabel3" default=""/>
        <composite:attribute name="calendartimelabel1" default=""/>
        <composite:attribute name="calendartimelabel2" default=""/>
        <composite:attribute name="calendartimelabel3" default=""/>

        <composite:attribute name="calendardatevalue1" default=""/>
        <composite:attribute name="calendardatevalue2" default=""/>
        <composite:attribute name="calendardatevalue3" default=""/>
        <composite:attribute name="calendartimevalue1" default=""/>
        <composite:attribute name="calendartimevalue2" default=""/>
        <composite:attribute name="calendartimevalue3" default=""/>



        <composite:attribute name="calendarpatternDate" default="dd/MM/yyyy"/>
        <composite:attribute name="calendarpatternTime" default="HH:mm:ss a"/>
        <composite:attribute name="calendarsize" default="8"/>


        <composite:attribute name="fromstart" default="true"/>
        <composite:attribute name="required" default="false" />
        <composite:attribute name="size"  default="25"/>
        <composite:attribute name="listener"  
                             method-signature="void handleSelect(org.primefaces.event.SelectEvent)" />
        <composite:attribute name="completeMethod"  
                             method-signature="java.util.List complete(java.lang.String)" />

    </composite:interface>
```

# Ejemplo:

* Mostrar en el panel del autocomente sugerencia sobre fechas y horas formateadas con un &lt;p:calendar-

![](/assets/autocalendar.png)

```java
        <p:outputLabel  value="#{msg['field.copiardesde']}" />
                            <jmoordbjsf:autocompleteWithCalendarDateTime
                                converter="#{solicitudConverter}"
                                completeMethod="#{solicitudAdministrativoController.completeSolicitudParaCopiar}"
                                labeltip1="#{msg['field.idsolicitud']}"
                                labelvalue1="#{p.idsolicitud}"   
                                labeltip2="#{msg['field.solicitadopor']}" 
                                labelvalue2="#{p.usuario.get(0).nombre}"
                                labeltip3="#{msg['field.responsable']}"
                                labelvalue3="#{p.usuario.get(1).nombre}"
                                labeltip4="#{msg['field.mision']} "
                                labelvalue4="#{p.mision}" 
                                labeltip5="#{msg['field.lugares']}" 
                                labelvalue4="#{p.lugares}"

                                calendardatelabel1="#{msg['field.fechapartida']}" 
                                calendardatevalue1="#{p.fechahorapartida}" 

                                calendartimelabel1="#{msg['field.horapartida']}"
                                calendartimevalue1="#{p.fechahorapartida}"  

                                calendardatelabel2="#{msg['field.fecharegreso']}" 
                                calendardatevalue2="#{p.fechahoraregreso}"  


                                calendartimelabel2="#{msg['field.horaregreso']}" 
                                calendartimevalue2="#{p.fechahoraregreso}"  


                                listener="#{solicitudAdministrativoController.handleSelectCopiarDesde}"
                                value="#{solicitudAdministrativoController.solicitudCopiar}"
                                itemLabel=" #{p.mision}"
                                field="mision"
                                dropdown="true"
                                minQueryLength="0"
                                update=":form:panel"
                                />
```



