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

```java
  @PostConstruct
    public void init() {
        try {
            String action = loginController.get("solicitud");
            String id = loginController.get("idsolicitud");
            String pageSession = loginController.get("pagesolicitud");
            //Search

            if (loginController.get("searchsolicitud") == null || loginController.get("searchsolicitud").equals("")) {
                loginController.put("searchsolicitud", "_init");
            }
            writable = false;

            solicitudList = new ArrayList<>();
            solicitudFiltered = new ArrayList<>();
            solicitud = new Solicitud();
            solicitudDataModel = new SolicitudDataModel(solicitudList);

            if (pageSession != null) {
                page = Integer.parseInt(pageSession);
            }
            Integer c = solicitudRepository.sizeOfPage(rowPage);
            page = page > c ? c : page;
            if (action != null) {
                switch (action) {
                    case "gonew":
                        solicitud = new Solicitud();

                        writable = false;
                        isNew();

                        //


                        break;
                    case "view":
                        if (id != null) {
                            Optional<Solicitud> optional = solicitudRepository.find("idsolicitud", Integer.parseInt(id));
                            if (optional.isPresent()) {
                                solicitud = optional.get();
                                unidadList = solicitud.getUnidad();
                                usuarioList = solicitud.getUsuario();
                                solicita = usuarioList.get(0);
                                responsable = usuarioList.get(1);
                                responsableOld = responsable;
                                facultadList = solicitud.getFacultad();
                                carreraList = solicitud.getCarrera();

                                solicitudSelected = solicitud;
                                _old = solicitud.getFecha();
                                writable = true;

                            }
                        }
                        break;
                    case "golist":
                        move();
                        break;
                }
            } else {
                move();
            }

        } catch (Exception e) {
            errorServices.errorMessage(nameOfClass(), nameOfMethod(), e.getLocalizedMessage());
        }
    }
```



