# &lt;jmoordbjsf:toolbarnewsavereturn&gt;

* Genera los botones new, save, return.
* Generalmente lo usamos con formularios donde no validamos por un campo en especial si no solamente al guardar

![](/assets/form2.png)

* El &lt;jmoordbjsf:toolbarnewsavereturn/&gt;, se coloca en la parte inferior.
* El método isNew\(\) no valida si existe o no el elemento ya que no hay una busqueda sino al guardar
* el metodo save\(\) debe implementarse la validaciòn para verificar si existe o no.
* En el init\(\) en el switch para new se debe invocar el** isNew\(\)**

```java
case "gonew":
solicitud = new Solicitud();

writable = false;
isNew();
```

## Controller

* Método init\(\) simplificado se elimino parte del código y solo se incluyo la sección que cambia **case "gonew"**

```java
  @PostConstruct
    public void init() {
        try {
          
            if (action != null) {
                switch (action) {
                    case "gonew":
                        solicitud = new Solicitud();

                        writable = false;
                        isNew();

                        //


                        break;
                    case "view":
                      
                        break;
                    case "golist":
                      
                }
            } else {
                move();
            }

        } catch (Exception e) {
            errorServices.errorMessage(nameOfClass(), nameOfMethod(), e.getLocalizedMessage());
        }
    }
```

## isNew\(\)

* No validar si existe o no un registro

```java
 public String isNew() {
        try {
            writable = true;

            Date idsecond = solicitud.getFecha();
            Integer id = solicitud.getIdsolicitud();

//            List<Solicitud> list = solicitudRepository.findBy(new Document("usuario.username", loginController.getUsuario().getUsername()).append("fecha", solicitud.getFecha()));
//            if (!list.isEmpty()) {
//                JsfUtil.warningDialog(rf.getAppMessage("warning.view"), rf.getMessage("warning.yasolicitoviajeenestafecha"));
//            }
//            if (DateUtil.fechaMenor(solicitud.getFecha(), DateUtil.getFechaActual())) {
//                JsfUtil.warningDialog(rf.getAppMessage("warning.view"), rf.getMessage("warning.fechasolicitudmenorqueactual"));
//                writable = false;
//
//            }
            solicitud = new Solicitud();
            solicitudSelected = new Solicitud();
            solicitud.setIdsolicitud(id);
            solicitud.setFecha(idsecond);
            solicitud.setMision("---");
            solicitud.setNumerodevehiculos(1);
            solicitud.setPasajeros(25);
            solicitud.setLugarpartida("UTP-AZUERO");

            solicitud.setFechaestatus(DateUtil.getFechaHoraActual());
            solicita = loginController.getUsuario();
            responsable = solicita;
            responsableOld = responsable;

            usuarioList = new ArrayList<>();
            usuarioList.add(solicita);
            usuarioList.add(responsable);
            solicitud.setUsuario(usuarioList);

            solicitud.setPeriodoacademico(DateUtil.getAnioActual().toString());
            solicitud.setFechahorapartida(solicitud.getFecha());
            solicitud.setFechahoraregreso(solicitud.getFecha());
            unidadList = new ArrayList<>();
            unidadList.add(loginController.getUsuario().getUnidad());

            Integer mes = DateUtil.mesDeUnaFecha(solicitud.getFecha());

            String idsemestre = "V";
            if (mes <= 3) {
                //verano
                idsemestre = "V";

            } else {
                if (mes <= 7) {
                    //primer
                    idsemestre = "I";
                } else {
                    //segundo
                    idsemestre = "II";
                }
            }
            solicitud.setSemestre(semestreServices.findById(idsemestre));
            List<Tipovehiculo> tipovehiculoList = new ArrayList<>();

            tipovehiculoList.add(tipovehiculoServices.findById("BUS"));
            solicitud.setTipovehiculo(tipovehiculoList);

            solicitud.setEstatus(estatusServices.findById("SOLICITADO"));

            String textsearch = "DOCENTE";

            solicitud.setTiposolicitud(tiposolicitudServices.findById(textsearch));
            solicitudSelected = solicitud;

        } catch (Exception e) {
            errorServices.errorMessage(nameOfClass(), nameOfMethod(), e.getLocalizedMessage());
        }
        return "";
    }
```





## Método save\(\)

* Incluir la validación de si existe o no.
* O la validacion que se considere necesaria

```java
 @Override
    public String save() {
        try {
            List<Solicitud> list = solicitudRepository.findBy(new Document("usuario.username", loginController.getUsuario().getUsername()).append("fecha", solicitud.getFechahorapartida()));
            if (!list.isEmpty()) {
                JsfUtil.warningDialog(rf.getAppMessage("warning.view"), rf.getMessage("warning.yasolicitoviajeenestafecha"));
            }
            if (DateUtil.fechaMenor(solicitud.getFechahorapartida(), DateUtil.getFechaActual())) {
                JsfUtil.warningDialog(rf.getAppMessage("warning.view"), rf.getMessage("warning.fechasolicitudmenorqueactual"));
                return "";

            }
            solicitud.setFecha(DateUtil.getFechaActual());
            solicitud.setActivo("si");
            solicitud.setUnidad(unidadList);
            solicitud.setFacultad(facultadList);
            solicitud.setCarrera(carreraList);
            usuarioList = new ArrayList<>();
            usuarioList.add(solicita);
            usuarioList.add(responsable);
            solicitud.setUsuario(usuarioList);
            List<Tipovehiculo> tipovehiculoList = new ArrayList<>();
            for (int i = 0; i < solicitud.getNumerodevehiculos(); i++) {
                tipovehiculoList.add(tipovehiculoServices.findById("BUS"));
            }
            solicitud.setTipovehiculo(tipovehiculoList);
            if (!solicitudServices.isValid(solicitud)) {
                return "";
            }
            solicitud.setSolicitudpadre(0);
            Integer solicitudesGuardadas = 0;
            for (Integer index = 0; index < solicitud.getNumerodevehiculos(); index++) {
                //Verificar si tiene un viaje en esas fechas
//            Optional<Solicitud> optionalRango = solicitudServices.coincidenciaResponsableEnRango(solicitud);
//            if (optionalRango.isPresent()) {
//                JsfUtil.warningDialog(rf.getAppMessage("warning.view"), rf.getMessage("warning.solicitudnumero") + " " + optionalRango.get().getIdsolicitud().toString() + "  " + rf.getMessage("warning.solicitudfechahoraenrango"));
//                return "";
//            }

                Integer idsolicitud = autoincrementableTransporteejbServices.getContador("solicitud");
                solicitud.setIdsolicitud(idsolicitud);
                Optional<Solicitud> optional = solicitudRepository.findById(solicitud);
                if (optional.isPresent()) {
                    JsfUtil.warningMessage(rf.getAppMessage("warning.idexist"));
                    return null;
                }

                //Lo datos del usuario
                solicitud.setUserInfo(userInfoServices.generateListUserinfo(loginController.getUsername(), "create"));
                if (solicitudRepository.save(solicitud)) {
                    //guarda el contenido anterior
                    revisionHistoryTransporteejbRepository.save(revisionHistoryServices.getRevisionHistory(solicitud.getIdsolicitud().toString(), loginController.getUsername(),
                            "create", "solicitud", solicitudRepository.toDocument(solicitud).toString()));
//enviarEmails();

                    //si cambia el email o celular del responsable actualizar ese usuario
                    if (!responsableOld.getEmail().equals(responsable.getEmail()) || !responsableOld.getCelular().equals(responsable.getCelular())) {
                        usuarioRepository.update(responsable);
                        //actuliza el que esta en el login
                        if (responsable.getUsername().equals(loginController.getUsuario().getUsername())) {
                            loginController.setUsuario(responsable);
                        }
                    }
//                JsfUtil.successMessage(rf.getAppMessage("info.save"));
//                reset();
                } else {
                    JsfUtil.successMessage("save() " + solicitudRepository.getException().toString());
                }
                //Asigna la solicitud padre para las demas solicitudes
                if (index.equals(0)) {
                    solicitud.setSolicitudpadre(solicitud.getIdsolicitud());
                }
            }
            JsfUtil.successMessage(rf.getMessage("info.savesolicitudes") + " : " + solicitudesGuardadas.toString() + " " + rf.getMessage("info.solicitudesde") + solicitud.getNumerodevehiculos());
            reset();
        } catch (Exception e) {
            errorServices.errorMessage(nameOfClass(), nameOfMethod(), e.getLocalizedMessage());
        }
        return "";
    }
```



