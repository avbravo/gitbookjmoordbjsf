# &lt;jmoordjsf:login/&gt;

* Muestra un componente para el login de los usuarios
* Permite que se agregue dos selectOneMenu 

## Atributos para un login simple

|  |  |
| :--- | :--- |
| fieldusername |  |
| labelusername |  |
| fieldpassword |  |
| update |  |
| dologin | método para el login |
| showone | false --&gt; no muestra el selectOneMenu |
| valueone | valor a recibir  |
| labelone | etiqueta  |
| idone | nombre del id |
| requiredMessageone | mensaje para requerido |
| requiredone | true--&gt; es requerido |
| selectLabelone |  |
| selectValueone |  |
| selectDisableone |  |
| selectItemsValueone |  |
| selectItemsLabelone |  |
| onchangeone |  |
| updateone |  |



## Atributos para un segundo selectOneMenu

```java
 <composite:attribute  name="showtwo" default="false"  type="java.lang.Boolean"/>
        <composite:attribute name="labeltwo" default=""/>
        <composite:attribute name="valuetwo" default="" />
        <composite:attribute name="idtwo" default="" />
        <composite:attribute name="requiredMessagetwo" default=""/>
        <composite:attribute name="requiredtwo" default="true"/>                 
        <composite:attribute name="selectLabeltwo" default=""/>
        <composite:attribute name="selectValuetwo" default=""/>
        <composite:attribute name="selectDisabletwo" default="true"/>
        <composite:attribute name="selectItemsValuetwo" default="" />
        <composite:attribute name="selectItemsLabeltwo" />
        <composite:attribute name="onchangetwo" default ="" />
        <composite:attribute name="updatetwo" default ="" />
```

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



