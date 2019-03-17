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

![](/assets/260b805a-29da-4ed3-a8fe-fc86f2dd65ba.png)





