# Crear composite distribuible con Maven

Crear el proyecto Maven

![](/assets/6405b374-0c38-4b9f-8c7c-4981fb972b84.png)

Indicamos el nombre del proyecto

![](/assets/340faf01-2d03-47b8-9eb5-5789bc3e4143.png)

al darle finalizar se crea el proyecto jmoordbjsf

![](/assets/164206d3-696f-4196-a65b-f1363ae1d7c7.png)

Revisamos las propiedades del proyecto

![](/assets/2cb9234e-f4e4-4ecf-a8ff-02e8ff92d5e8.png)

## Editar el archivo pom.xml

![](/assets/af264050-e321-402c-8c98-558929030f67.png)

## Agregar dependencias

* primefaces
* bootfaces

```css
dependencies>
        <dependency>
            <groupId>org.primefaces</groupId>
            <artifactId>primefaces</artifactId>
            <version>6.2</version>
        </dependency>
          <dependency>
            <groupId>net.bootsfaces</groupId>
            <artifactId>bootsfaces</artifactId>
            <version>1.4.0</version>
        </dependency>
    </dependencies>
```

* **Agregar la seccion build**

```java
<build>
    <finalName>${project.artifactId}</finalName> 
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.0</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                    <compilerArguments>
                        <endorseddirs>${endorsed.dir}</endorseddirs>
                    </compilerArguments>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-ejb-plugin</artifactId>
                <version>3.0.1</version>
                <configuration>
                    <ejbVersion>3.1</ejbVersion>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <version>3.1.1</version>
                <executions>
                    <execution>
                        <phase>validate</phase>
                        <goals>
                            <goal>copy</goal>
                        </goals>
                        <configuration>
                            <outputDirectory>${endorsed.dir}</outputDirectory>
                            <silent>true</silent>
                            <artifactItems>
                                <artifactItem>
                                    <groupId>javax</groupId>
                                    <artifactId>javaee-endorsed-api</artifactId>
                                    <version>7.0</version>
                                    <type>jar</type>
                                </artifactItem>
                            </artifactItems>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
```

## Dependencias

![](/assets/a98769bf-2f73-4bba-82b4-0837abbede17.png)

## En la pestaña Files de NetBeans

![](/assets/4f721f25-8c61-45a9-b943-f7f8ca96fe4a.png)

Dar clic derecho New--&gt; Folder...

![](/assets/b825b1a1-e840-476b-9e08-c216963d99e5.png)

indicar resources/META-INF

![](/assets/01852e70-6045-441b-bd8d-b84866949e0b.png)

## Creamos los archivos xml:

* faces-config.xml
* jmoordbjsf.tablib.xml

![](/assets/2a1c3d3a-9302-4646-beb2-0435d37bdb53.png)

### faces-config.xml

```java
<?xml version="1.0"?>
<faces-config xmlns="http://java.sun.com/xml/ns/javaee"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
            http://java.sun.com/xml/ns/javaee/web-facesconfig_2_0.xsd"
        version="2.0">

    <!-- Empty config file to enable JSF annotation scanning -->

</faces-config>
```

### jmoordbjsf.tablib.xml

* Indicamos el namespace
* library-name

```java
<?xml version="1.0"?>
<facelet-taglib version="2.0"
        xmlns="http://java.sun.com/xml/ns/javaee"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-facelettaglibrary_2_0.xsd">

    <namespace>http://jmoordbjsf.com/taglib</namespace>
    <composite-library-name>jmoordbjsf</composite-library-name>
</facelet-taglib>
```

## Dentro de la carpeta META-INF

* creamos la carpeta resources/jmoordbjsf

![](/assets/1562bcc3-f2c2-49df-a29d-714f32183185.png)

indicamos los nombres de carpeta

![](/assets/65674363-1991-464d-88da-aea752660b73.png)

## En este directorio agregamos:

* composite
* imagenes
* css
* js

![](/assets/879cd8fe-67e9-4c2f-b0be-f25cdf96ef72.png)

## Creando el primer componente

* Creamos un componente selectOneMenu de bootfaces simplificando las opciones si/no.
* Ubicarse en la carpeta jmoordbjsf
* Clic derecho --&gt; New --&gt;Other

![](/assets/cb9225f3-4fba-45ab-9a0e-1bcfe6d875b9.png)

**Categories**: Java Server Faces

**File Types: **JSF Page

![](/assets/81aee574-cb98-45e2-ad02-9af4625a5854.png)

Nota: Si seleccionamos JSF Composite Component, no permitirá finalizar porque no es un proyecto web, por esta razon seleccionamos JSF  Page.

## File Name: yesno

![](/assets/f7de43b7-99e6-43e5-aa95-d603500ff08e.png)

se crea el archivo yesno.xhtml, sobre el que vamos a editar para agregar el composite.

![](/assets/9cfbb1d6-2882-4a6b-9eaa-4ac8208889a9.png)

Reemplazamos por el código

```java
<?xml version='1.0' encoding='UTF-8' ?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:p="http://primefaces.org/ui"
      xmlns:composite="http://java.sun.com/jsf/composite"
      xmlns:b="http://bootsfaces.net/ui"
      xmlns:f="http://xmlns.jcp.org/jsf/core"
      xmlns:h="http://xmlns.jcp.org/jsf/html">
    <composite:interface >

        <composite:attribute name="value" />

        <composite:attribute name="required"/>
        <composite:attribute name="rendered"/>
        <composite:attribute name="disabled" default="false"/>
        <composite:attribute name="id"/>
        <composite:attribute name="colMd" default="2"/>
        <composite:attribute name="labelColMd" default="2"/>

    </composite:interface>
    <composite:implementation>


        <b:selectOneMenu value="#{cc.attrs.value}"
                         disabled="#{cc.attrs.disabled}"
                         colMd="#{cc.attrs.colMd}" 
                         required="#{cc.attrs.required}" 
                         requiredMessage="#{app['title.sexo']} #{app['info.notnull']}"
                         labelColMd="#{cc.attrs.labelColMd}" >
            <f:selectItem itemLabel="#{app['button.yes']}" itemValue="si" />
            <f:selectItem itemLabel="#{app['button.no']}" itemValue="no" />

        </b:selectOneMenu>
        <h:graphicImage library="jsflive" name="add.png"/>

    </composite:implementation>

</html>
```

**Nota: **El componente tiene asociados etiquetas definidas en avbravoutils y esta orientado a ejbjmoordb.

## Construir el proyecto

Clic derecho--&gt; Clearn & Build

![](/assets/b66aff34-afe7-4b11-bd71-33e4c37b1170.png)

## CSS

* Creamos un archivo css dentro de resources/jmoordbjsf

![](/assets/264c18cb-82b6-4e50-8fbb-c4ea431f226a.png)

Ejemplo de css

![](/assets/260b805a-29da-4ed3-a8fe-fc86f2dd65ba.png)Agregarlo al composite

* usar el   &lt;h:outputStylesheet library=**"jmoordbjsf**" name=**"jmoordbjsf.css"**/&gt;
* Mediante el styleClass de cada componente usamos la propiedad deseada. &lt;p:datatable **styleClass="ui-datatable"**&gt;

```java
<?xml version='1.0' encoding='UTF-8' ?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:p="http://primefaces.org/ui"
      xmlns:composite="http://java.sun.com/jsf/composite"
      xmlns:b="http://bootsfaces.net/ui"
      xmlns:f="http://xmlns.jcp.org/jsf/core">
    <composite:interface >

    <cc:interface >
        <cc:attribute name="id"/>

    </cc:interface>

    <cc:implementation>
       <p:dataTable styleClass="ui-datatable"/>
        <h:outputStylesheet library="jmoordbjsf" name="jmoordb.css"/>
    </cc:implementation>

</ui:composition>
```

## IMAGENES

* Las imagenes las agregamos dentro de resources/jmoordbjsf

![](/assets/91e8c17a-ca1b-483d-981e-dcbf85f8d73c.png)

Usar la imágenes en el componente componente

```java
 <h:graphicImage library="jmoordbjsf" name="add.png"/>
```

Si ejecutamos un proyecto, se vería la imagen

![](/assets/9d793a86-dfa9-4d5e-9470-3ae111d55b9c.png)

# Probar el Componente

* Creamos un proyecto Web
* Agregarmos la dependencia jmordbjsf
* Agregar el componente a una pagina.
* En este ejemplo usaremos el plugin de PayaraMicro para generar el proyecto
* Repositorio del proyecto

[https://github.com/avbravo/jmoordbjsftest](https://github.com/avbravo/jmoordbjsftest)

Crear el proyecto: jmoordbjsftest

![](/assets/85462f5c-de93-4fed-bcce-01b5cc3695f3.png)

Indicar el nombre del proyecto

![](/assets/7489e900-3077-4323-b905-5cb85212667a.png)

PayaraMicro en este ejemplo la versión 5.183 o superior

![](/assets/4d60c80e-4e9f-4945-81b3-92bdf1d1d2c2.png)

En las propiedades del proyecto activamos la configuracion, revisamos la versiòn del JDK, y seleccionamos primefaces como framework

![](/assets/718165d3-152c-4e24-b4f0-7a58f69737c2.png)

## Editamos el archivo pom.xml

* **Actualizar la version de primefaces**

```java
<dependency>
            <groupId>org.primefaces</groupId>
            <artifactId>primefaces</artifactId>
            <version>6.2</version>
        </dependency>
```

* **Agregar avbravoutls**

```java
    <dependency>
        <groupId>com.github.avbravo</groupId>
        <artifactId>avbravoutils</artifactId>
        <version>0.39.4</version>
    </dependency>
```

* **Agregar jmoordbjsf \(mediante jitpack\)**

```java
      <dependency>
        <groupId>com.github.avbravo</groupId>
        <artifactId>jmoordbjsf</artifactId>
        <version>0.4.1</version>
    </dependency
```

* **Agregar el repository jitpack**

```java
  <repository>
            <id>jitpack.io</id>
            <url>https://jitpack.io</url>
        </repository>
```

### En el build

* Actualizar las versiones de los plugins de  maven a las ultimas

```java
 <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.0</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                    <compilerArguments>
                        <endorseddirs>${endorsed.dir}</endorseddirs>
                    </compilerArguments>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>3.2.2</version>
                <configuration>
                    <failOnMissingWebXml>false</failOnMissingWebXml>
                </configuration>
            </plugin>
```

* Agregar el final name

```java
<finalName>jmoordbjsfg</finalName>
```

## Crearemos un Controller para manejar los datos

* Ubicarse en el paquete com.avbravo.jmoordbjsftest
* Dar clic derecho 
* Seleccionar --&gt;New --&gt;JSF Managed Bean

![](/assets/aeabb31b-60ee-4966-ab07-6debf1e9350d.png)

Lo denominamos MyController en el scope: Request

Se crea la clase MyController.java

```java
package com.avbravo.jmoordbjsftest;

import javax.inject.Named;
import javax.enterprise.context.RequestScoped;

/**
 *
 * @author avbravo
 */
@Named(value = "myContoller")
@RequestScoped
public class MyContoller {

    /**
     * Creates a new instance of MyContoller
     */
    public MyContoller() {
    }

}
```

* Implemenamos Serializable
* Agregamos una propiedad para almacenar la opción seleccionada 
* Creamos un método para mostrar el mensaje
* Utilizar JsfUtil para enviar mensajes

## Código Final

```java
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package com.avbravo.jmoordbjsftest;

import com.avbravo.avbravoutils.JsfUtil;
import java.io.Serializable;
import javax.inject.Named;
import javax.enterprise.context.RequestScoped;

/**
 *
 * @author avbravo
 */
@Named
@RequestScoped
public class MyController implements Serializable{
private String seleccion;

    public String getSeleccion() {
        return seleccion;
    }

    public void setSeleccion(String seleccion) {
        this.seleccion = seleccion;
    }




    /**
     * Creates a new instance of MyContoller
     */
    public MyController() {
    }

    public String mostrar(){
        JsfUtil.errorDialog("Seleccion:", seleccion); 
        return "";
    }
}
```

## Ahora editamos el archivo index.xhtml

![](/assets/80f1eb25-44dc-4bc5-8b2d-0ce0b6382d82.png)



Archivo inicial

```java
<?xml version='1.0' encoding='UTF-8' ?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:h="http://xmlns.jcp.org/jsf/html">
    <h:head>
        <title>Facelet Title</title>
    </h:head>
    <h:body>
        Hello from Facelets
        <br />
        <h:link outcome="welcomePrimefaces" value="Primefaces welcome page" />
    </h:body>
</html>
```

* Agregar el namespace jm: para usarlo con los componentes  y el taglib.

```java
xmlns:jm="http://jmoordbjsf.com/taglib"
```

* Agregar el &lt;f:view&gt;

```java
 <f:view contentType="text/html">
```

* Agregar un &lt;h:form&gt;

```java
 </h:form>
```

* Agregamos un &lt;p:message&gt;

```java
<p:messages id="msg"/>
```

* Agregar el componente

```java
 <jm:yesno id="a" value="#{myController.seleccion}"/>
```

* &lt;p:commandButton&gt; para mostrar la opcion seleccionada por el usuario

```java
 <p:commandButton value="Mostrar" update="msg" action="#{myController.save()}"/>
```

## Cogido completo

```
<?xml version='1.0' encoding='UTF-8' ?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:h="http://xmlns.jcp.org/jsf/html"
      xmlns:jm="http://jmoordbjsf.com/taglib" 
      xmlns:f="http://xmlns.jcp.org/jsf/core"
      xmlns:p="http://primefaces.org/ui">
    <f:view contentType="text/html">
        <h:head>
            <title>Facelet Title</title>
        </h:head>
        <h:body>
            <h:form>
                <p:messages id="msg"/>
                <jm:yesno id="a" value="#{myController.seleccion}"/>


                <p:commandButton value="Mostrar" update="msg" action="#{myController.mostrar()}"/>
            </h:form>
        </h:body>
    </f:view>
</html>
```

## Ejecutar el proyecto

* Se muestra el componente
* Al dar clic en el botón se despliega un mensaje con la selección.

![](/assets/ff3e4830-2261-4b95-a628-ae22daf697ce.png)



