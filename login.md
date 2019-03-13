# login

* Muestra un componente para el login de los usuarios

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



