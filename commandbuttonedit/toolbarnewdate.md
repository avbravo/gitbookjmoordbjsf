# &lt;jmoordbjsf:toolbarnewdate&gt;

* Se usa en un formulario new.xhtml
* Permite buscar por fecha como llave primaria

![](/assets/newdate.png)

```java
   <jmoordbjsf:toolbarnewDate label="#{msg['field.fechagira']}"
                                    title="#{msg['titleview.solicitudmanualdocente']}"
                                    value="#{solicitudManualDocenteController.solicitud.fecha}"
                                    isnew="#{solicitudManualDocenteController.isNew()}"
                                    disabled="#{solicitudManualDocenteController.writable}"
                                    new="#{solicitudManualDocenteController.prepare('new',solicitudManualDocenteController.solicitud)}"
                                    rendererList="#{applicationMenu.solicitudDocentePorAdministrador.list}"
                                    list="#{solicitudManualDocenteController.prepare('golist',solicitudManualDocenteController.solicitud)}"

                                    />
```



## Controller

* isNew\(\)
* Validar por el atributo fecha.

```java
 @Override
    public String isNew() {
        try {
            writable = true;

            Date idsecond = solicitud.getFecha();
            Integer id = solicitud.getIdsolicitud();

            List<Solicitud> list = solicitudRepository.findBy(new Document("usuario.username", loginController.getUsuario().getUsername()).append("fecha", solicitud.getFecha()));
            if (!list.isEmpty()) {
                JsfUtil.warningDialog(rf.getAppMessage("warning.view"), rf.getMessage("warning.yasolicitoviajeenestafecha"));
            }
            if (DateUtil.fechaMenor(solicitud.getFecha(), DateUtil.getFechaActual())) {
                JsfUtil.warningDialog(rf.getAppMessage("warning.view"), rf.getMessage("warning.fechasolicitudmenorqueactual"));
                writable = false;

            }
          
          ----
        } catch (Exception e) {
            errorServices.errorMessage(nameOfClass(), nameOfMethod(), e.getLocalizedMessage());
        }
        return "";
    }// </editor-fold>
```



