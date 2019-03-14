# login

* Muestra un componente para el login de los usuarios
* Permite que se agregue un selectOneMenu para los roles
* simple=true indica que es un login simple sin roles

## Atributos para un login simple

```java
        <composite:attribute name="update" default=":form:growl"/>
        <composite:attribute  name="simple" default="true"  type="java.lang.Boolean"/>

        <composite:attribute name="fieldusername" />
        <composite:attribute name="labelusername" />
        <composite:attribute name="fieldpassword" />

      
```

## Atributos para un selectOneMenu con roles

```java
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

## 

## 

## Atributos para un segundo selectOneMenu

```java
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



