# &lt;jmoordbjsf:toolbarnew/&gt;

* Dibuja los botones new, caja de texto y regresar
* Se usa para formulario new.xthml simple
* Se coloca el campo llave a buscar
* Se puede usar un campo secundario en ese caso se debe modificar el método isNew \(cuando usamos autoincrementables generalmente.\)

![](/assets/componente.png)

## Ejemplo con llave primaria  @Id

```java
 <jmoordbjsf:toolbarnew label="#{msg['field.idrol']}"
                        title="#{msg['titleview.rol']}"
                        value="#{rolController.rol.idrol}"
                        isnew="#{rolController.isNew()}"
                        disabled="#{rolController.writable}"
                        new="#{rolController.prepare('new',rolController.rol)}"
                        rendererList="#{applicationMenu.rol.list}"
                        list="#{rolController.prepare('golist',rolController.rol)}"
                        />
```

Al ingresar un valor no existente y presionar Enter se habilita el panel con los demás datos.

![](/assets/test.png)

## RolController.java

* **isNew\(\), valida por la llave primaria.**

```java
public String isNew() {
        try {
            writable = true;
            if (JsfUtil.isVacio(rol.getIdrol())) {
                writable = false;
                return "";
            }
            rol.setIdrol(rol.getIdrol().toUpperCase());
            Optional<Rol> optional = rolRepository.findById(rol);
            if (optional.isPresent()) {
                writable = false;

                JsfUtil.warningMessage(rf.getAppMessage("warning.idexist"));
                return "";
            } else {
                String id = rol.getIdrol();
                rol = new Rol();
                rol.setIdrol(id);
                rolSelected = new Rol();
            }

        } catch (Exception e) {
            errorServices.errorMessage(nameOfClass(),nameOfMethod(), e.getLocalizedMessage());
        }
        return "";
    }
```

* **prepare\(\)**
* Validar el new, y golist.

```java
public String prepare(String action, Rol item) {
        String url = "";
        try {
            loginController.put("pagerol", page.toString());
            loginController.put("rol", action);
            switch (action) {
                case "new":
                    rol = new Rol();
                    rolSelected = new Rol();

                    writable = false;
                    break;

                case "view":

                    rolSelected = item;
                    rol = rolSelected;
                    loginController.put("idrol", rol.getIdrol());

                    url = "/pages/rol/view.xhtml";
                    break;
                case "golist":

                    url = "/pages/rol/list.xhtml";
                    break;

                case "gonew":
                    rol = new Rol();
                    rolSelected = new Rol();
                    url = "/pages/rol/new.xhtml";
                    break;
            }

        } catch (Exception e) {
            errorServices.errorMessage(nameOfClass(),nameOfMethod(), e.getLocalizedMessage());
        }

        return url;
    }
```



