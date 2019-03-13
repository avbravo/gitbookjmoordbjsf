# cssschedule

Es un conjunto de css que se usan con los componentes &lt;p:schedule&gt; para darle colores diferentes.

Para usarlo simplemente agregar antes del &lt;h:form&gt;

```java
<jmoordbjsf:cssschedule/>
```

Colores disponibles:

* schedule-orange
* schedule-yellow
* schedule-blue
* schedule-gray
* schedule-magenta
* schedule-green
* schedule-red

![](/assets/colores.png)

![](/assets/colores.png)

![](/assets/colores.png)

![](/assets/colores.png)

## Segmento del &lt;p:schedule&gt;

```java
 <p:schedule id="schedule"       
             rightHeaderTemplate="month,agendaWeek,agendaDay,basicDay"
             value="#{calendarioSolicitudViajesController.eventModel}"
             widgetVar="myschedule" timeZone="GMT-5" locale="es">

           <p:ajax  event="eventSelect"  
           listener="#{calendarioSolicitudViajesController.onEventSelect}" update="eventDetails" oncomplete="PF('solicitudDialog').show();" />                      
           <!--<p:ajax  event="dateSelect" listener="#{calendarioSolicitudViajesController.onDateSelectCalendar}" update="newDetails" oncomplete="PF('newDialog').show();" />-->
 </p:schedule>
```

## CONTROLLER

Declar un objeto de tipo ScheduleModel

```java
private ScheduleModel eventModel;
```

init\(\)

```java
@PostConstruct
    public void init() {
        try {
         cargarSchedule(true);

        } catch (Exception e) {
            errorServices.errorMessage(nameOfClass(), nameOfMethod(), e.getLocalizedMessage());
        }
    }
```

Para indicarle los colores usamos el nombre del tema desde el componente.

```
tema = "schedule-orange";
```

* Lo cargamos con el addEvent\(\)

```java
public void cargarSchedule(Boolean start) {
        try {
            totalAprobado = 0;
            totalSolicitado = 0;
            totalRechazadoCancelado = 0;
            totalViajes = 0;
            Document doc;
            Document docViajes = new Document("activo", "si");

            doc = new Document("activo", "si");

            List<Viaje> list = viajesRepository.findBy(docViajes, new Document("fecha", 1));

            solicitudList = solicitudRepository.findBy(doc, new Document("fecha", 1));
            eventModel = new DefaultScheduleModel();
            if (!solicitudList.isEmpty()) {
                solicitudList.forEach((a) -> {
                    String car = "{ ";
                    car = a.getTipovehiculo().stream().map((t) -> t.getIdtipovehiculo() + " ").reduce(car, String::concat);
                    car += " }";
                    String tema = "schedule-blue";
                    switch (a.getEstatus().getIdestatus()) {
                        case "SOLICITADO":
                            totalSolicitado++;
                            tema = "schedule-orange";

                            break;
                        case "APROBADO":
                            totalAprobado++;
                            String viajest = "{";
                            viajest = a.getViaje().stream().map((t) -> t.getIdviaje() + " ").reduce(viajest, String::concat);
                            viajest = "}";
                            car += viajest;
                            tema = "schedule-green";
                            break;
                        case "RECHAZADO":
                            totalRechazadoCancelado++;
                            tema = "schedule-red";
                            break;
                        case "CANCELADO":
                            totalRechazadoCancelado++;
                            tema = "schedule-red";
                            break;
                    }

                    eventModel.addEvent(
                        new DefaultScheduleEvent("# " + a.getIdsolicitud() + " Mision: " + a.getMision() + " Responsable: " + a.getUsuario().get(1).getNombre() + " " + a.getEstatus().getIdestatus()
                               + car,
                              a.getFechahorapartida(), a.getFechahoraregreso(), tema)
                    );
                });
            }
            //Viajes

            if (!list.isEmpty()) {
                list.forEach((v) -> {
                    totalViajes++;
                    String car = v.getVehiculo().getMarca() + " " + v.getVehiculo().getModelo() + " " + v.getVehiculo().getPlaca();
                    String chofer = "{";
                    chofer = v.getConductor().getNombre();
                    chofer += " }";
                    eventModel.addEvent(
                         new DefaultScheduleEvent("#" + v.getIdviaje() + " Viaje: " + car + " " + chofer,
                                    v.getFechahorainicioreserva(), v.getFechahorafinreserva(), "schedule-blue")
                    );
                }
                );

            }

        } catch (Exception e) {
            errorServices.errorDialog(nameOfClass(), nameOfMethod(), "cargarSchedule", e.getLocalizedMessage());
        }
    }
// </editor-fold>
```



