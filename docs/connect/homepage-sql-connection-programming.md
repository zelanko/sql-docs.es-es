---
title: Programación de cliente SQL en la página principal | Microsoft Docs
description: Página de concentrador con anotado vínculos a descargas y documentación de numerosas combinaciones de idiomas y sistemas operativos, para conectarse a SQL Server o a Azure SQL Database.
author: MightyPen
ms.date: 11/07/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-daveng
ms.author: genemi
ms.openlocfilehash: d773e05a3ed953e5210c0ade3226b4a32e82aeab
ms.sourcegitcommit: 8cc38f14ec72f6f420479dc1b15eba64b1a58041
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 11/08/2018
ms.locfileid: "51289905"
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Página principal de cliente de programación para Microsoft SQL Server


Le damos la bienvenida a nuestra página principal sobre programación para interactuar con Microsoft SQL Server y con Azure SQL Database en la nube del cliente. En este artículo se proporciona la siguiente información:

- Enumera y describe las combinaciones de idioma y el controlador disponibles.
    - Se proporciona información para los sistemas operativos de Windows, MacOS y Linux (Ubuntu y otros).
- Proporciona vínculos a la documentación detallada para cada combinación.
- Muestra las áreas y las subáreas de la documentación jerárquica para determinados idiomas, si procede.


#### <a name="azure-sql-database"></a>Base de datos SQL de Azure

En cualquier lenguaje determinado, el código que se conecta a SQL Server es casi idéntico al código para conectarse a Azure SQL Database.

Para obtener más información acerca de las cadenas de conexión para conectarse a Azure SQL Database, consulte:

- [Usar .NET Core (C#) para consultar una base de datos de SQL Azure](/azure/sql-database/sql-database-connect-query-dotnet-core).
- Otra base de datos de SQL de Azure que están cercanos en el artículo anterior de la tabla de contenido, acerca de otros lenguajes. Por ejemplo, ver [uso de PHP para consultar una base de datos SQL de Azure](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php).


#### <a name="build-an-app-webpages"></a>Páginas Web de una aplicación compilada

Nuestro *una aplicación compilada* las páginas Web contienen ejemplos de código, junto con información de configuración, en un formato alternativo. Para obtener más información, vea más adelante en este artículo el [sección con la etiqueta *sitio Web de una aplicación compilada*](#an-204-aka-ms-sqldev).



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>Controladores para los programas cliente y lenguajes


En la tabla siguiente, cada imagen de lenguaje es un vínculo a los detalles sobre cómo usar el lenguaje con SQL Server. Cada vínculo lleva a una sección más adelante en este artículo.

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| &nbsp; [![Logotipo de C#][image-ref-320-csharp]](#an-110-ado-net-docu) | &nbsp; [![ORM Entity Framework de .NET Framework][image-ref-333-ef]](#an-116-csharp-ef-orm) | &nbsp; [![Logotipo de Java][image-ref-330-java]](#an-130-jdbc-docu) |
| &nbsp; [![Logotipo de Node.js][image-ref-340-node]](#an-140-node-js-docu) | &nbsp; [**`ODBC for C++`**](#an-160-odbc-cpp-docu)<br/>[![CPP más grande][image-ref-322-cpp]](#an-160-odbc-cpp-docu) | &nbsp; [![Logotipo PHP][image-ref-360-php]](#an-170-php-docu) |
| &nbsp; [![Logotipo de Python][image-ref-370-python]](#an-180-python-docu) | &nbsp; [![Logotipo de Ruby][image-ref-380-ruby]](#an-190-ruby-docu) | &nbsp; ... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>Descarga e instala

El siguiente artículo se dedica a la descarga e instalar varios controladores de conexión de SQL, para su uso con lenguajes de programación:

- [Controladores de SQL Server](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![Logotipo de C#][image-ref-320-csharp] C# mediante ADO.NET

Los lenguajes administrados de. NET, como C# y Visual Basic, son los usuarios más comunes de ADO.NET. *ADO.NET* es un nombre para un subconjunto de clases de .NET Framework casual.

#### <a name="code-examples"></a>Ejemplos de código

|||
| :-- | :-- |
| [Prueba de concepto de la conexión a SQL mediante ADO.NET](./ado-net/step-3-proof-of-concept-connecting-to-sql-using-ado-net.md) | Un ejemplo de código pequeño centrado sobre cómo conectar y consultar SQL Server. |
| [Conectar de forma resistente a SQL con ADO.NET](./ado-net/step-4-connect-resiliently-to-sql-with-ado-net.md) | Lógica de reintento en un ejemplo de código, porque las conexiones en ocasiones, pueden experimentar momentos de pérdida de conectividad.<br /><br />Lógica de reintento se aplica también a las conexiones que mantiene a través de internet en cualquier base de datos en la nube, como a Azure SQL Database. |
| [Base de datos SQL Azure: Demostración de cómo usar .NET Core en Windows, Linux y macOS para crear un programa de C#, para conectarse y consultar](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Ejemplo de Azure SQL Database. |
| [Generar una aplicación: Windows C#, ADO.NET,](https://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | Información de configuración, junto con ejemplos de código. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentación

|||
| :-- | :-- |
| [C# mediante ADO.NET](./ado-net/index.md)| Raíz de nuestra documentación. |
| [Namespace: System.Data](https://docs.microsoft.com/dotnet/api/system.data) | Un conjunto de clases que se usan para ADO.NET. |
| [Namespace: System.Data.SqlClient](https://docs.microsoft.com/dotnet/api/system.data.SqlClient) | El conjunto de clases que son más directamente el centro de ADO.NET. |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Logotipo de Entity Framework][image-ref-333-ef] Entity Framework (EF) con C&#x23;

Entity Framework (EF) proporciona la asignación relacional de objetos (ORM). ORM facilita el código fuente de programación orientada a objetos (OOP) manipular los datos que se recuperaron de una base de datos relacional de SQL.

EF tiene relaciones directas o indirectas con las siguientes tecnologías:

- .NET Framework
- [LINQ to SQL](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/), o [LINQ to Entities](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- Mejoras de sintaxis del lenguaje, como el **=>** operador en C#.
- Programas útiles que generan código fuente para las clases que se asignan a las tablas de la base de datos SQL. Por ejemplo, [EdmGen.exe](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe).


#### <a name="original-ef-and-new-ef"></a>EF original y EF nuevo

El [página de inicio para Entity Framework](https://docs.microsoft.com/ef/) presenta EF con una descripción similar al siguiente:

- Entity Framework es un asignador relacional de objetos (O/RM) que permite a los desarrolladores de .NET trabajar con una base de datos mediante objetos. NET. Elimina la necesidad para la mayoría del código fuente de acceso a datos que los desarrolladores normalmente deben escribir.

*Entity Framework* es un nombre compartido por dos bifurcaciones de código fuente independiente. Una bifurcación EF es anterior, y ahora se puede mantener su código fuente público. Otro EF es nuevo. El dos EFs se describen a continuación:

|     |     |
| :-- | :-- |
| [EF 6.x](https://docs.microsoft.com/ef/ef6/) | Microsoft por primera vez EF en agosto de 2008. En marzo de 2015, Microsoft anunció que EF 6.x era la versión final que Microsoft desarrolla. Microsoft publicó el código fuente en el dominio público.<br /><br />Inicialmente, EF formaba parte de .NET Framework. Pero EF 6.x se ha quitado de .NET Framework.<br /><br />[EF 6.x de código fuente en Github, en el repositorio *aspnet/EntityFramework6*](https://github.com/aspnet/EntityFramework6) |
| [EF Core](https://docs.microsoft.com/ef/core/) | Microsoft publicó el núcleo de EF recién desarrollada en junio de 2016. EF Core está diseñado para una mayor flexibilidad y portabilidad. EF Core puede ejecutar en sistemas operativos más allá de simplemente Microsoft Windows. Y EF Core puede interactuar con bases de datos más allá de simplemente Microsoft SQL Server y otras bases de datos relacionales.<br /><br />**C&#x23; ejemplos de código:**<br />[Introducción a Entity Framework Core](https://docs.microsoft.com/ef/core/get-started/index)<br />[Introducción a EF Core en .NET Framework con una base de datos existente](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF y tecnologías relacionadas son eficaces y son mucho que aprender para los desarrolladores que quieran controlar toda el área.

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Logotipo de Java][image-ref-330-java] Java y JDBC

Microsoft proporciona un controlador Java Database Connectivity (JDBC) para su uso con SQL Server (o con Azure SQL Database, por supuesto). Se trata de un controlador JDBC de tipo 4 que proporciona conectividad a bases de datos mediante las interfaces de programación de aplicaciones (API) estándar JDBC.

#### <a name="code-examples"></a>Ejemplos de código

|||
| :-- | :-- |
| [Ejemplos de código](./jdbc/code-samples/index.md) | Ejemplos de código que enseñan a los tipos de datos, conjuntos de resultados y datos de gran tamaño. |
| [Ejemplo de URL de conexión](./jdbc/connection-url-sample.md) | Describe cómo usar una dirección URL de conexión para conectarse a SQL Server. A continuación, usarla para usar una instrucción SQL para recuperar datos. |
| [Ejemplo de origen de datos](./jdbc/data-source-sample.md) | Describe cómo usar un origen de datos para conectarse a SQL Server. A continuación, utilizar un procedimiento almacenado para recuperar datos. |
| [Use Java para consultar una base de datos SQL de Azure](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Ejemplo de Azure SQL Database. |
| [Crear aplicaciones de Java con SQL Server en Ubuntu](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | Información de configuración, junto con ejemplos de código. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentación

La documentación de JDBC incluye las siguientes áreas principales:

|||
| :-- | :-- |
| [Java Database Connectivity (JDBC)](./jdbc/index.md) | Raíz de la documentación de JDBC. |
| [Referencia](./jdbc/reference/index.md) | Interfaces, clases y miembros. |
| [Guía de programación del controlador JDBC para SQL](./jdbc/programming-guide-for-jdbc-sql-driver.md) | Información de configuración, junto con ejemplos de código. |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Logotipo de Node.js][image-ref-340-node] Node.js

Con Node.js puede conectarse a SQL Server de Windows, Linux o Mac. Es la raíz de la documentación de Node.js [aquí](./node-js/index.md).

El controlador de conexión de Node.js para SQL Server se implementa en JavaScript. El controlador utiliza el protocolo TDS, que es compatible con todas las versiones actuales de SQL Server. El controlador es un proyecto de código abierto, [disponible en Github](https://tediousjs.github.io/tedious/).

#### <a name="code-examples"></a>Ejemplos de código

|||
| :-- | :-- |
| [Prueba de concepto de la conexión a SQL mediante Node.js](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | Desnuda código para conectarse a SQL Server y ejecutar una consulta de origen. |
| [La base de datos SQL Azure: uso de Node.js para la consulta](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | Ejemplo de Azure SQL Database en la nube. |
| [Crear aplicaciones de Node.js para usar SQL Server en macOS](https://www.microsoft.com/sql-server/developer-get-started/node/mac/) | Información de configuración, junto con ejemplos de código. |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>ODBC de C++ 

![Logotipo ODBC][image-ref-350-odbc] ![CPP más grande][image-ref-322-cpp]

Conectividad abierta de base de datos (ODBC) se desarrolló en la década de 1990, y es anterior a .NET Framework. ODBC está diseñado para ser independiente de cualquier sistema de base de datos determinada e independiente del sistema operativo.

En los años numerosos controladores ODBC se han creado y publicado por grupos dentro y fuera de Microsoft. El intervalo de controladores implican varios lenguajes de programación de cliente. La lista de destinos de datos va más allá de SQL Server.

Algunos otros controladores de conectividad usan ODBC internamente.

#### <a name="code-example"></a>Ejemplo de código

- [Ejemplo de código de C++, con ODBC](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>Esquema de la documentación

El contenido ODBC en esta sección se centra en obtener acceso a SQL Server o Azure SQL Database, desde C++. La tabla siguiente muestra un esquema aproximado de la documentación principal para ODBC.


| Área | Subárea | Descripción |
| :--- | :------ | :---------- |
| [ODBC de C++](./odbc/index.md) | Raíz de nuestra documentación. |
| [Mac-Linux](./odbc/linux-mac/index.md) | &nbsp; | Información sobre cómo usar ODBC en los sistemas operativos Linux o MacOS. |
| [Windows](./odbc/windows/index.md)     | &nbsp; | Información sobre cómo usar ODBC en el sistema operativo Windows. |
| [Administración](../odbc/admin/index.md) | &nbsp; | La herramienta administrativa para administrar orígenes de datos ODBC. |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | Varios controladores ODBC que se crean y proporcionados por Microsoft. |
| [Conceptual y referencia](../odbc/reference/index.md) | &nbsp; | Información conceptual acerca de la interfaz ODBC, además de referencia tradicional. |
| &nbsp; " | [Apéndices](../odbc/reference/appendixes/index.md)    | Tablas de transición de estado, biblioteca de cursores ODBC y mucho más. |
| &nbsp; " | [Desarrollar la aplicación](../odbc/reference/develop-app/index.md)  | Las funciones, identificadores y mucho más. |
| &nbsp; " | [Desarrollo de controladores](../odbc/reference/develop-driver/index.md) | Cómo desarrollar su propio controlador ODBC, si tiene un origen de datos especializado. |
| &nbsp; " | [Instalar](../odbc/reference/install/index.md) | Instalación de ODBC, subclaves y mucho más. |
| &nbsp; " | [Sintaxis](../odbc/reference/syntax/index.md)   | API para el acceso a datos, instalador, traducción y el programa de instalación. |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![Logotipo PHP][image-ref-360-php] PHP

Puede usar PHP para interactuar con SQL Server. Es la raíz de la documentación de PHP [aquí](./php/index.md).

#### <a name="code-examples"></a>Ejemplos de código

|||
| :-- | :-- |
| [Prueba de concepto de la conexión a SQL mediante PHP](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | Un ejemplo de código pequeño centrado sobre cómo conectar y consultar SQL Server. |
| [Paso 4: Conectar de forma resistente a SQL con PHP](./php/step-4-connect-resiliently-to-sql-with-php.md) | Lógica de reintento en un ejemplo de código, porque las conexiones a través de Internet y en la nube en ocasiones, pueden experimentar momentos de pérdida de conectividad. |
| [La base de datos SQL Azure: uso de PHP para consulta](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Ejemplo de Azure SQL Database. |
| [Crear aplicaciones PHP para utilizar SQL Server en RHEL](https://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | Información de configuración, junto con ejemplos de código. |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Logotipo de Python][image-ref-370-python] Python


Puede usar Python para interactuar con SQL Server.

#### <a name="code-examples"></a>Ejemplos de código

|||
| :-- | :-- |
| [Prueba de concepto que se conecta a SQL con Python mediante pyodbc](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | Un ejemplo de código pequeño centrado sobre cómo conectar y consultar SQL Server. |
| [La base de datos SQL Azure: uso de Python para la consulta](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Ejemplo de Azure SQL Database. |
| [Crear aplicaciones PHP para utilizar SQL Server en SLES](https://www.microsoft.com/sql-server/developer-get-started/python/sles/) | Información de configuración, junto con ejemplos de código. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentación

| Área | Descripción |
| :--- | :---------- |
| [Python para SQL Server](./python/index.md) | Raíz de nuestra documentación. |
| [controlador pymssql](./python/pymssql/index.md) | Microsoft no mantener o probar el controlador pymssql.<br /><br />El controlador pymssql de conexión es una interfaz sencilla para las bases de datos SQL, para su uso en programas de Python. Pymssql se basa en FreeTDS para proporcionar una interfaz de DB-API de Python (PEP-249) a Microsoft SQL Server. |
| [controlador pyodbc](./python/pyodbc/index.md)   | El controlador de conexión de pyodbc es un módulo de Python de código abierto que simplifica el acceso a las bases de datos ODBC. Implementa la especificación de API de DB 2.0, pero está equipado con incluso más comodidad de Python. |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Logotipo de Ruby][image-ref-380-ruby] Ruby

Puede usar Ruby para interactuar con SQL Server. Es la raíz de la documentación de Ruby [aquí](./ruby/index.md).

#### <a name="code-examples"></a>Ejemplos de código

|||
| :-- | :-- |
| [Prueba de concepto de la conexión a SQL con Ruby](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | Un ejemplo de código pequeño centrado sobre cómo conectar y consultar SQL Server. |
| [La base de datos SQL Azure: uso de Ruby para consulta](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Ejemplo de Azure SQL Database. |
| [Crear aplicaciones de Ruby para usar SQL Server en MacOS](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | Información de configuración, junto con ejemplos de código. |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-developmenthttpswwwmicrosoftcomsql-serverdeveloper-get-started"></a>[Sitio Web de una aplicación compilada para el desarrollo de cliente SQL](https://www.microsoft.com/sql-server/developer-get-started/)


En nuestro [ *una aplicación compilada* ](https://www.microsoft.com/sql-server/developer-get-started/) puede elegir entre una larga lista de lenguajes para conectarse a SQL Server de programación de las páginas Web. Y el programa cliente puede ejecutar una variedad de sistemas operativos.

*Una aplicación compilada* enfatiza la simplicidad y la integridad para el desarrollador que se acaba de empezar. Los pasos explican las tareas siguientes:

1. Cómo instalar Microsoft SQL Server
2. Cómo descargar e instalar las herramientas y los controladores.
3. Cómo hacer que las configuraciones necesarias, según corresponda para el sistema operativo elegido.
4. Cómo compilar el código fuente proporcionado.
5. Cómo ejecutar el programa.

A continuación son un par contornos aproximados de los detalles proporcionados en el sitio Web:

#### <a name="java-on-ubuntu"></a>Java en Ubuntu:

1. Configurar el entorno
    - Paso 1.1: instalar SQL Server
    - Paso 1.2 instalar Java
    - Paso 1.3 instalar el Kit de desarrollo de Java (JDK)
    - Paso 1.4 instalar Maven
2. Crear aplicación de Java con SQL Server
    - Crear una aplicación Java que se conecta a SQL Server y ejecuta consultas de paso 2.1
    - Paso 2.2 Creación de una aplicación Java que se conecta a SQL Server mediante el marco de trabajo popular Hibernar
3. Hacer que la aplicación de Java hasta 100 veces más rápido
    - Paso 3.1 crear una aplicación de Java para demostrar los índices de almacén de columnas

#### <a name="python-on-windows"></a>Python en Windows:

1. Configurar el entorno
    - Paso 1.1: instalar SQL Server
    - Paso 1.2 instale Python
    - Paso 1.3 instalar el controlador ODBC y la utilidad de línea de comandos SQL para SQL Server
2. Crear aplicación de Python con SQL Server
    - Paso 2.1 instalación del controlador Python para SQL Server
    - Paso 2.2 crear una base de datos para la aplicación
    - Paso 2.3 Creación de una aplicación de Python que se conecta a SQL Server y ejecuta las consultas
3. Hacer que la aplicación de Python hasta 100 veces más rápido
    - Paso 3.1 Creación de una nueva tabla con 5 millones mediante sqlcmd
    - Paso 3.2 Creación de una aplicación de Python que consulta esta tabla y mide el tiempo empleado
    - Paso 3.3 medir cuánto tarda en ejecutar la consulta
    - Paso 3.4 agregar un índice de almacén de columnas a la tabla
    - Paso 3.5 medir cuánto se tarda en ejecutar la consulta con un índice de almacén de columnas

Las capturas de pantalla siguientes darle una idea del aspecto de nuestro sitio Web documentación de desarrollo de SQL.

#### <a name="choose-a-language"></a>Elija un idioma:

![Sitio Web de desarrollo de SQL, introducción][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>Elija un sistema operativo:

![Sitio Web de desarrollo de SQL, Java Ubuntu][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>Otros entornos de desarrollo


Esta sección proporciona vínculos sobre otras opciones de desarrollo. Estos incluyen el uso estos mismos lenguajes de desarrollo de Azure en general. La información va más allá de destino es simplemente Azure SQL Database y Microsoft SQL Server.

#### <a name="developer-hub-for-azure"></a>Centro para desarrolladores de Azure

- [Centro para desarrolladores de Azure](https://docs.microsoft.com/azure/)
- [Azure para desarrolladores de .NET](https://docs.microsoft.com/dotnet/azure/)
- [Azure para desarrolladores de Java](https://docs.microsoft.com/java/azure/)
- [Azure para desarrolladores de Node.js](https://docs.microsoft.com/nodejs/azure/)
- [Azure para desarrolladores de Python](https://docs.microsoft.com/python/azure/)
- [Crear una aplicación web PHP en Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>Otros idiomas

- [Crear aplicaciones de Go con SQL Server en Windows](https://www.microsoft.com/sql-server/developer-get-started/go/windows/)



<!-- Image references. -->

[image-ref-322-cpp]: ./media/homepage-sql-connection-drivers/gm-cpp-4point-p61f.png
[image-ref-320-csharp]: ./media/homepage-sql-connection-drivers/gm-csharp-c10c.png
[image-ref-333-ef]: ./media/homepage-sql-connection-drivers/gm-entity-framework-ef20d.png
[image-ref-330-java]: ./media/homepage-sql-connection-drivers/gm-java-j18c.png
[image-ref-340-node]: ./media/homepage-sql-connection-drivers/gm-node-n30.png
[image-ref-350-odbc]: ./media/homepage-sql-connection-drivers/gm-odbc-ic55826-o35.png
[image-ref-360-php]: ./media/homepage-sql-connection-drivers/gm-php-php60.png
[image-ref-370-python]: ./media/homepage-sql-connection-drivers/gm-python-py72.png
[image-ref-380-ruby]: ./media/homepage-sql-connection-drivers/gm-ruby-un-r82.png
[image-ref-390-aka-ms-sqldev-choose-language]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-400-aka-ms-sqldev-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png

