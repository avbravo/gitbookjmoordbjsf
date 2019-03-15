# &lt;jmoordjsf:login/&gt;

* Muestra un componente para el login de los usuarios
* Permite que se agregue dos selectOneMenu 

## Atributos para un login simple

| Atributo | Descripción |
| :--- | :--- |
| fieldusername |  |
| labelusername |  |
| fieldpassword |  |
| update |  |
| dologin  **method-signature="java.lang.String action\(\)** | método para el login |
| **showone** | **false --&gt; no muestra el selectOneMenu** |
| valueone | entity que guarda el entity seleccionado |
| labelone | etiqueta que se mostrara a la izquierda del selectOneMenu |
| idone | nombre del id |
| requiredMessageone | mensaje para requerido |
| requiredone | true--&gt; es requerido |
| selectLabelone |  |
| selectValueone |  |
| selectDisableone |  |
| selectItemsValueone | List&lt;&gt; del entity con los valores que se mostraran |
| selectItemsLabelone | Texto que se mostrara del entity seleccionado |
| onchangeone |  |
| updateone |  |
| **showtwo** | **false --&gt; no muestra el segundo selectOneMenu** |
| labeltwo |  |
| valuetwo |  |
| idtwo |  |
| requiredMessagetwo |  |
| requiredtwo |  |
| selectLabeltwo |  |
| selectValuetwo |  |
| selectDisabletwo |  |
| selectItemsValuetwo |  |
| selectItemsLabeltwo |  |
| onchangetwo |  |
| updatetwo |  |

## 

* # Simple:

![](/assets/simplre.png)

```java
 <jmoordbjsf:login
                    id="username"
                    fieldusername="#{loginController.username}"
                    labelusername="#{app['login.username']}"
                    fieldpassword="#{loginController.password}"
                    dologin="#{loginController.doLogin()}"


                    />
```

* # Con un selectOneMenu

![](/assets/login.png)

## Codigo

```java
 <jmoordbjsf:login
                    id="username"
                    fieldusername="#{loginController.username}"
                    labelusername="#{app['login.username']}"
                    fieldpassword="#{loginController.password}"
                    dologin="#{loginController.doLogin()}"

                    showone="true"
                    idone="rol"
                    requiredMessageone="#{msg['field.idrol']}"
                    selectItemsLabelone="#{item.idrol}"
                    selectItemsValueone="#{usuarioController.rolServices.rolList}"
                    valueone="#{loginController.rol}"
                    labelone="#{msg['field.rol']}"
                    />
```

* # Con dos selectOneMenu

# ![](/assets/dosele.png)

```java
  <jmoordbjsf:login                                         
                    id="username"
                    fieldusername="#{loginController.username}"
                    labelusername="#{app['login.username']}"
                    fieldpassword="#{loginController.password}"
                    dologin="#{loginController.doLogin()}"

                    showone="true"
                    idone="rol"
                    requiredMessageone="#{msg['field.idrol']}"
                    selectItemsLabelone="#{item.idrol}"
                    selectItemsValueone="#{usuarioController.rolServices.rolList}"
                    valueone="#{loginController.rol}"
                    labelone="#{msg['field.rol']}"

                    showtwo="true"
                    idtwo="almacen"
                    requiredMessagetwo="#{msg['field.almacen']}"
                    selectItemsLabeltwo="#{item.descripcion}"
                    selectItemsValuetwo="#{usuarioController.almacenServices.almacenList}"
                    valuetwo="#{loginController.almacen}"
                    labeltwo="#{msg['field.almacen']}"

                    />
```



