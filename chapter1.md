# Instalación

* Recuerde que muchos componentes estan optimizados para trabajar con
* jmoordb
* jmoordbutils

Solo agregue a su proyecto maven

* Dependencia

```java
          <dependency>
            <groupId>com.github.avbravo</groupId>
            <artifactId>jmoordbjsf</artifactId>
            <version>0.3.2</version>
        </dependency>
```

* repository

```java
  <repository>
            <id>jitpack.io</id>
            <url>https://jitpack.io</url>
 </repository>
```

en la pagina.xhtml

* namespace

```java
 xmlns:jmoordbjsf="http://jmoordbjsf.com/taglib"
```

puede utilizar el componte que desee

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



