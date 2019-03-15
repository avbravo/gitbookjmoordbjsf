# autocompleteWithCalendarDateTime

\* Se usa para mostrar un par de Date y Time hasta 6 elementos en esa secuencia

\* Despliega el primer calendar como Date dd/MM/yyyy

\* Despliega el siguiente como Time  HH:mm:ss a

* Combinaciones: Date/Time Date/Time Date/Time

\* Se debe pasar columnpaneltip= 2 para que muestre el labely el valor

# Atributos



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



