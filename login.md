# login

* Muestra un componente para el login de los usuarios
* Permite que se agregue un selectOneMenu para los roles
* simple=true indica que es un login simple sin roles

## Composite

```java
        <composite:attribute name="update" default=":form:growl"/>
        <composite:attribute  name="simple" default="true"  type="java.lang.Boolean"/>

        <composite:attribute name="fieldusername" />
        <composite:attribute name="labelusername" />
        <composite:attribute name="fieldpassword" />

        <composite:attribute name="valuerol" />
        <composite:attribute name="idrol" />
        <composite:attribute name="requiredMessagerol" default=""/>
        <composite:attribute name="requiredrol" default="true"/>                 
        <composite:attribute name="selectLabelrol" default=""/>
        <composite:attribute name="selectValuerol" default=""/>
        <composite:attribute name="selectDisablerol" default="true"/>

        <composite:attribute name="selectItemsValuerol" default="" />
        <composite:attribute name="selectItemsLabelrol" />
        <composite:attribute name="onchangerol" default ="" />
        <composite:attribute name="updaterol" default ="" />

        <composite:attribute name="dologin" 
                             method-signature="java.lang.String action()" />
```

# 

# Simple:

![](/assets/simplre.png)

```java
 <jmoordbjsf:login
                    simple="true"
                    id="username"
                    fieldusername="#{loginController.username}"
                    labelusername="#{app['login.username']}"
                    fieldpassword="#{loginController.password}"
                    dologin="#{loginController.doLogin()}"


                    />
```

# Multiple:

![](/assets/login.png)

## Codigo

```java
 <jmoordbjsf:login
                    simple="false"
                    id="username"
                    fieldusername="#{loginController.username}"
                    labelusername="#{app['login.username']}"
                    fieldpassword="#{loginController.password}"
                    dologin="#{loginController.doLogin()}"

                    idrol="rol"
                    requiredMessagerol="#{msg['field.idrol']}"                    
                    selectItemsLabelrol="#{item.idrol}"
                    selectItemsValuerol="#{usuarioController.rolServices.rolList}"
                    valuerol="#{loginController.rol}"
                    />
```



