# &lt;jmoordjsf:login/&gt;

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

## Atributos para un selectOneMenu

```java
 <composite:attribute name="valueone" />
        <composite:attribute name="labelone" />
        <composite:attribute name="idone" />
        <composite:attribute name="requiredMessageone" default=""/>
        <composite:attribute name="requiredone" default="true"/>                 
        <composite:attribute name="selectLabelone" default=""/>
        <composite:attribute name="selectValueone" default=""/>
        <composite:attribute name="selectDisableone" default="true"/>
        <composite:attribute name="selectItemsValueone" default="" />
        <composite:attribute name="selectItemsLabelone" />
        <composite:attribute name="onchangeone" default ="" />
        <composite:attribute name="updateone" default ="" />
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

* # Simple:

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

* # Con un selectOneMenu

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

                    idone="one"
                    requiredMessageone="#{msg['field.idrol']}"
                    selectItemsLabelone="#{item.idrol}"
                    selectItemsValueone="#{usuarioController.rolServices.rolList}"
                    valueone="#{loginContoneler.rol}"
                    labelone="#{msg['field.rol']}"
                    />
```





* # Con dos selectOneMenu

# 



