# jschedule

* Es un archivo java scritp que reemplaza las etiquetas del &lt;p:schedule&gt; por las correspondientes en idioma español
* Nos permite cambiar el idioma del &lt;p:schedule&gt; a a español

Por ejemplo:

* Por defecto se muestra en ingles![](/assets/original.png)

Si implementamos antes del &lt;h:form&gt;

```java
<jmoordbjsf:jsschedule/>
```

automaticamente lo cambia a español.

![](/assets/esa.png)

&lt;p:schedule&gt; no se agrega nada

```java
 <p:schedule id="schedule"       
               rightHeaderTemplate="month,agendaWeek,agendaDay,basicDay"
               value="#{calendarioSolicitudViajesController.eventModel}" widgetVar="myschedule" timeZone="GMT-5" locale="es">

                        <p:ajax  event="eventSelect"  listener="#{calendarioSolicitudViajesController.onEventSelect}" update="eventDetails" oncomplete="PF('solicitudDialog').show();" />                      
                        <!--<p:ajax  event="dateSelect" listener="#{calendarioSolicitudViajesController.onDateSelectCalendar}" update="newDetails" oncomplete="PF('newDialog').show();" />-->
                    </p:schedule>
```



