# &lt;jmoordbjsf:toolbarnewlowercase&gt;

Se usa para los formularios de login si queremos garantizar que sea solo en minusculas.

![](/assets/miesrdd.png)

```java
      <jmoordbjsf:toolbarnewlowercase label="#{msg['field.username']}"
                                         title="#{msg['titleview.usuario']}"
                                         value="#{usuarioController.usuario.username}"
                                         isnew="#{usuarioController.isNew()}"
                                         disabled="#{usuarioController.writable}"
                                         new="#{usuarioController.prepare('new',usuarioController.usuario)}"
                                         rendererList="#{applicationMenu.usuario.list}"
                                         list="#{usuarioController.prepare('golist',usuarioController.usuario)}"

                                         />
```

# 



