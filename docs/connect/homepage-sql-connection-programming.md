---
title: Página principal de programación de cliente SQL | Microsoft Docs
description: Página central con vínculos anotados a descargas y documentación para numerosas combinaciones de idiomas y sistemas operativos, para conectarse a SQL Server o a Azure SQL Database.
author: MightyPen
ms.date: 11/07/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-daveng
ms.author: genemi
ms.openlocfilehash: 6961f8c23b4acfd787958cc9a160faf88362b54c
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451851"
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Página principal de la programación de clientes de Microsoft SQL Server


Esta es la Página principal de la programación de clientes para interactuar con Microsoft SQL Server y con Azure SQL Database en la nube. Este artículo ofrece la siguiente información:

- Enumera y describe las combinaciones de idiomas y controladores disponibles.
    - Se proporciona información para los sistemas operativos Linux (Ubuntu y otros), MacOS y Windows.
- Proporciona vínculos a la documentación detallada para cada combinación.
- Muestra las áreas y subáreas de la documentación jerárquica para determinados idiomas, si procede.


#### <a name="azure-sql-database"></a>Base de datos SQL de Azure

En cualquier lenguaje determinado, el código que se conecta a SQL Server es casi idéntico al código para conectarse a Azure SQL Database.

Para obtener más información acerca de las cadenas de conexión para conectarse a Azure SQL Database, consulte:

- [Use .net Core (C#) para consultar una base de datos SQL de Azure](/azure/sql-database/sql-database-connect-query-dotnet-core).
- Otros Azure SQL Database que están cerca del artículo anterior en la tabla de contenido, sobre otros lenguajes. Por ejemplo, consulte [uso de php para consultar una base de datos SQL de Azure](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php).


#### <a name="build-an-app-webpages"></a>Páginas web de compilación a aplicación

Nuestras páginas web de *compilación-de-aplicación* presentan ejemplos de código, junto con información de configuración, en un formato alternativo. Para obtener más información, vea más adelante en este artículo la sección sobre la [ *creación de un sitio web*](#an-204-aka-ms-sqldev)de la aplicación.



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>Idiomas y controladores para programas cliente


En la tabla siguiente, cada imagen de idioma es un vínculo a los detalles sobre cómo usar el lenguaje con SQL Server. Cada vínculo salta a una sección posterior de este artículo.

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| &nbsp; [logotipoC# de ![][image-ref-320-csharp]](#an-110-ado-net-docu) | &nbsp; [![ORM Entity Framework, de .NET Framework][image-ref-333-ef]](#an-116-csharp-ef-orm) | &nbsp; [![Logotipo de Java][image-ref-330-java]](#an-130-jdbc-docu) |
| logotipo de &nbsp; [![Node. js][image-ref-340-node]](#an-140-node-js-docu) | &nbsp; [ **`ODBC for C++`** ](#an-160-odbc-cpp-docu)<br/>[![cpp-big-plus][image-ref-322-cpp]](#an-160-odbc-cpp-docu) | &nbsp; [logotipo de ![PHP][image-ref-360-php]](#an-170-php-docu) |
| &nbsp; [![Logotipo de Python][image-ref-370-python]](#an-180-python-docu) | &nbsp; [logotipo de ![Ruby][image-ref-380-ruby]](#an-190-ruby-docu) | &nbsp; ... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>Descargas e instalaciones

El siguiente artículo se dedica a la descarga e instalación de varios controladores de conexión de SQL, para su uso en los lenguajes de programación:

- [Controladores de SQL Server](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![C#logotipo][image-ref-320-csharp] C# con ADO.NET

Los lenguajes administrados de .NET C# , como y Visual Basic, son los usuarios más comunes de ADO.net. *ADO.net* es un nombre casual para un subconjunto de clases .NET Framework.

#### <a name="code-examples"></a>Ejemplos de código

|||
| :-- | :-- |
| [Prueba de concepto de la conexión a SQL mediante ADO.NET](./ado-net/step-3-connect-sql-ado-net.md) | Un pequeño ejemplo de código centrado en la conexión y consulta de SQL Server. |
| [Conectar de forma resistente a SQL con ADO.NET](./ado-net/step-4-connect-resiliently-sql-ado-net.md) | Lógica de reintento en un ejemplo de código, ya que en ocasiones las conexiones pueden experimentar momentos de pérdida de conectividad.<br /><br />La lógica de reintento se aplica bien a las conexiones que se mantienen a través de Internet a cualquier base de datos en la nube, como Azure SQL Database. |
| [Azure SQL Database: demostración de cómo usar .NET Core en Windows, Linux y macOS para crear un C# programa, conectarse y consultar](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Azure SQL Database ejemplo. |
| [Compilación-a-aplicación: C#, ADO.net, Windows](https://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | Información de configuración, junto con ejemplos de código. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentación

|||
| :-- | :-- |
| [C# con ADO.NET](./ado-net/index.md)| Raíz de la documentación. |
| [Espacio de nombres: System. Data](https://docs.microsoft.com/dotnet/api/system.data) | Un conjunto de clases usadas para ADO.NET. |
| [Namespace: System.Data.SqlClient](https://docs.microsoft.com/dotnet/api/system.data.SqlClient) | Conjunto de clases que son más directamente el centro de ADO.NET. |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Logotipo de Entity Framework][image-ref-333-ef] Entity Framework (EF) con C&#x23;

Entity Framework (EF) proporciona asignación relacional de objetos (ORM). ORM facilita a su código fuente de programación orientada a objetos (OOP) la manipulación de los datos que se recuperaron de una base de datos SQL relacional.

EF tiene relaciones directas o indirectas con las siguientes tecnologías:

- .NET Framework
- [LINQ to SQL](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/)o [LINQ to Entities](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- Mejoras en la sintaxis del lenguaje, como el operador **=>** C#en.
- Programas útiles que generan código fuente para las clases que se asignan a las tablas de la base de datos SQL. Por ejemplo, [EdmGen. exe](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe).


#### <a name="original-ef-and-new-ef"></a>EF original y nuevo EF

La [Página de inicio de Entity Framework](https://docs.microsoft.com/ef/) presenta EF con una descripción similar a la siguiente:

- Entity Framework es un asignador relacional de objetos (O/RM) que permite a los desarrolladores de .NET trabajar con una base de datos mediante objetos .NET. Elimina la necesidad de la mayor parte del código fuente de acceso a datos que los desarrolladores normalmente deben escribir.

*Entity Framework* es un nombre compartido por dos bifurcaciones de código fuente independientes. Una rama EF es más antigua y el público ahora puede mantener su código fuente. El otro EF es nuevo. Los dos EFs se describen a continuación:

|     |     |
| :-- | :-- |
| [EF 6.x](https://docs.microsoft.com/ef/ef6/) | Microsoft lanzó por primera vez EF en agosto de 2008. En marzo 2015, Microsoft anunció que EF 6. x era la versión final que desarrollaría Microsoft. Microsoft publicó el código fuente en el dominio público.<br /><br />Inicialmente, EF formaba parte de .NET Framework. Pero EF 6. x se quitó de .NET Framework.<br /><br />[Código fuente EF 6. x en Github, en el repositorio *ASPNET/EntityFramework6*](https://github.com/aspnet/EntityFramework6) |
| [EF Core](https://docs.microsoft.com/ef/core/) | Microsoft lanzó el EF Core recién desarrollado en junio de 2016. EF Core está diseñado para ofrecer una mayor flexibilidad y portabilidad. EF Core puede ejecutarse en sistemas operativos más allá de solo Microsoft Windows. Y EF Core pueden interactuar con bases de datos más allá de Microsoft SQL Server y otras bases de datos relacionales.<br /><br />**Ejemplos&#x23; de código de C:**<br />[Introducción con Entity Framework Core](https://docs.microsoft.com/ef/core/get-started/index)<br />[Introducción a EF Core en .NET Framework con una base de datos existente](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF y las tecnologías relacionadas son eficaces y son mucho para el desarrollador que desea dominar todo el área.

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Logotipo de Java][image-ref-330-java] Java y JDBC

Microsoft proporciona un controlador Java Database Connectivity (JDBC) para su uso con SQL Server (o con Azure SQL Database, por supuesto). Se trata de un controlador JDBC de tipo 4 que proporciona conectividad a bases de datos mediante las interfaces de programación de aplicaciones (API) estándar JDBC.

#### <a name="code-examples"></a>Ejemplos de código

|||
| :-- | :-- |
| [Ejemplos de código](./jdbc/code-samples/index.md) | Ejemplos de código que enseñan sobre los tipos de datos, los conjuntos de resultados y los datos de gran tamaño. |
| [Ejemplo de URL de conexión](./jdbc/connection-url-sample.md) | Describe cómo usar una dirección URL de conexión para conectarse a SQL Server. A continuación, úselo para usar una instrucción SQL para recuperar datos. |
| [Ejemplo de origen de datos](./jdbc/data-source-sample.md) | Describe cómo utilizar un origen de datos para conectarse a SQL Server. A continuación, use un procedimiento almacenado para recuperar los datos. |
| [Uso de Java para consultar una base de datos SQL de Azure](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Azure SQL Database ejemplo. |
| [Creación de aplicaciones de Java con SQL Server en Ubuntu](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | Información de configuración, junto con ejemplos de código. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentación

La documentación de JDBC incluye las siguientes áreas principales:

|||
| :-- | :-- |
| [Java Database Connectivity (JDBC)](./jdbc/index.md) | Raíz de nuestra documentación de JDBC. |
| [Referencia](./jdbc/reference/index.md) | Interfaces, clases y miembros. |
| [Guía de programación del controlador JDBC para SQL](./jdbc/programming-guide-for-jdbc-sql-driver.md) | Información de configuración, junto con ejemplos de código. |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Logotipo de node. js][image-ref-340-node] Node.js

Con node. js puede conectarse a SQL Server desde Windows, Linux o Mac. La raíz de nuestra documentación de node. js está [aquí](./node-js/index.md).

El controlador de conexión de node. js para SQL Server se implementa en JavaScript. El controlador usa el protocolo TDS, que es compatible con todas las versiones modernas de SQL Server. El controlador es un proyecto de código abierto que está [disponible en github](https://tediousjs.github.io/tedious/).

#### <a name="code-examples"></a>Ejemplos de código

|||
| :-- | :-- |
| [Prueba de concepto de la conexión a SQL mediante Node.js](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | Código fuente sin sistema operativo para conectarse a SQL Server y ejecutar una consulta. |
| [Azure SQL Database: uso de node. js para consultar](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | Ejemplo de Azure SQL Database en la nube. |
| [Creación de aplicaciones de node. js para usar SQL Server en macOS](https://www.microsoft.com/sql-server/developer-get-started/node/mac/) | Información de configuración, junto con ejemplos de código. |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>ODBC paraC++ 

![Logotipo de ODBC][image-ref-350-odbc] ![cpp-big-plus][image-ref-322-cpp]

Open Database Connectivity (ODBC) se desarrolló en los años noventa y .NET Framework. ODBC está diseñado para ser independiente de cualquier sistema de base de datos determinado e independiente del sistema operativo.

A lo largo de los años, se han creado y publicado muchos controladores ODBC en grupos dentro y fuera de Microsoft. El intervalo de controladores implica varios lenguajes de programación de cliente. La lista de destinos de datos va más allá SQL Server.

Otros controladores de conectividad usan ODBC internamente.

#### <a name="code-example"></a>Ejemplo de código

- [Ejemplo de código de C++, con ODBC](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>Esquema de documentación

El contenido ODBC de esta sección se centra en el acceso a SQL Server o Azure SQL Database, C++desde. En la tabla siguiente se muestra un esquema aproximado de la documentación principal de ODBC.


| Área | Subárea | Descripción |
| :--- | :------ | :---------- |
| [ODBC paraC++](./odbc/index.md) | Raíz de la documentación. |
| [Linux-Mac](./odbc/linux-mac/index.md) | &nbsp; | Información sobre el uso de ODBC en los sistemas operativos Linux o MacOS. |
| [Windows](./odbc/windows/index.md)     | &nbsp; | Información sobre el uso de ODBC en el sistema operativo Windows. |
| [Administración](../odbc/admin/index.md) | &nbsp; | Herramienta administrativa para administrar orígenes de datos ODBC. |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | Varios controladores ODBC creados y proporcionados por Microsoft. |
| [Conceptual y referencia](../odbc/reference/index.md) | &nbsp; | Información conceptual sobre la interfaz ODBC, además de la referencia tradicional. |
| &nbsp; " | [Apéndices](../odbc/reference/appendixes/index.md)    | Tablas de transición de estado, biblioteca de cursores ODBC, etc. |
| &nbsp; " | [Desarrollo de aplicaciones](../odbc/reference/develop-app/index.md)  | Funciones, identificadores y mucho más. |
| &nbsp; " | [Desarrollo de controladores](../odbc/reference/develop-driver/index.md) | Cómo desarrollar su propio controlador ODBC, si tiene un origen de datos especializado. |
| &nbsp; " | [Instalar](../odbc/reference/install/index.md) | Instalación de ODBC, subclaves y mucho más. |
| &nbsp; " | [Sintaxis](../odbc/reference/syntax/index.md)   | API para el programa de instalación, el instalador, la traducción y el acceso a datos. |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![Logotipo de PHP][image-ref-360-php] PHP

Puede usar PHP para interactuar con SQL Server. La raíz de la documentación de PHP está [aquí](./php/index.md).

#### <a name="code-examples"></a>Ejemplos de código

|||
| :-- | :-- |
| [Prueba de concepto de la conexión a SQL mediante PHP](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | Un pequeño ejemplo de código centrado en la conexión y consulta de SQL Server. |
| [Paso 4: Conectar de forma resistente a SQL con PHP](./php/step-4-connect-resiliently-to-sql-with-php.md) | Lógica de reintento en un ejemplo de código, ya que las conexiones a través de Internet y la nube pueden experimentar ocasionalmente momentos de pérdida de conectividad. |
| [Azure SQL Database: uso de PHP para consultar](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Azure SQL Database ejemplo. |
| [Creación de aplicaciones PHP para usar SQL Server en RHEL](https://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | Información de configuración, junto con ejemplos de código. |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Logotipo de Python][image-ref-370-python] Python


Puede usar Python para interactuar con SQL Server.

#### <a name="code-examples"></a>Ejemplos de código

|||
| :-- | :-- |
| [Prueba de concepto que se conecta a SQL con Python mediante pyodbc](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | Un pequeño ejemplo de código centrado en la conexión y consulta de SQL Server. |
| [Azure SQL Database: uso de Python para consultar](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Azure SQL Database ejemplo. |
| [Creación de aplicaciones PHP para usar SQL Server en SLES](https://www.microsoft.com/sql-server/developer-get-started/python/sles/) | Información de configuración, junto con ejemplos de código. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentación

| Área | Descripción |
| :--- | :---------- |
| [Python para SQL Server](./python/index.md) | Raíz de la documentación. |
| [controlador pymssql](./python/pymssql/index.md) | Microsoft no mantiene ni prueba el controlador pymssql.<br /><br />El controlador de conexión pymssql es una interfaz sencilla para las bases de datos SQL, para su uso en programas de Python. Pymssql se basa en FreeTDS para proporcionar una interfaz de Python DB-API (PEP-249) para Microsoft SQL Server. |
| [controlador pyodbc](./python/pyodbc/index.md)   | El controlador de conexión pyodbc es un módulo de Python de código abierto que facilita el acceso a las bases de datos ODBC. Implementa la especificación de DB API 2,0, pero está empaquetada con mayor comodidad de Python. |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Logotipo de Ruby][image-ref-380-ruby] Ruby

Puede usar Ruby para interactuar con SQL Server. La raíz de nuestra documentación de Ruby está [aquí](./ruby/index.md).

#### <a name="code-examples"></a>Ejemplos de código

|||
| :-- | :-- |
| [Prueba de concepto de la conexión a SQL con Ruby](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | Un pequeño ejemplo de código centrado en la conexión y consulta de SQL Server. |
| [Azure SQL Database: uso de Ruby para consultar](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Azure SQL Database ejemplo. |
| [Creación de aplicaciones de Ruby para usar SQL Server en MacOS](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | Información de configuración, junto con ejemplos de código. |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-developmenthttpswwwmicrosoftcomsql-serverdeveloper-get-started"></a>[Crear un sitio web de la aplicación para el desarrollo de clientes SQL](https://www.microsoft.com/sql-server/developer-get-started/)


En nuestras páginas web de la [*aplicación de compilación*](https://www.microsoft.com/sql-server/developer-get-started/) , puede elegir entre una larga lista de lenguajes de programación para conectarse a SQL Server. Y el programa cliente de puede ejecutar varios sistemas operativos.

*Compilación: una aplicación* destaca la simplicidad y la integridad del desarrollador que se está iniciando. En los pasos se explican las tareas siguientes:

1. Cómo instalar Microsoft SQL Server
2. Cómo descargar e instalar herramientas y controladores.
3. Cómo realizar las configuraciones necesarias, según sea necesario para el sistema operativo elegido.
4. Cómo compilar el código fuente proporcionado.
5. Cómo ejecutar el programa.

A continuación se muestran un par de contornos aproximados de los detalles proporcionados en el sitio web:

#### <a name="java-on-ubuntu"></a>Java en Ubuntu:

1. Configurar el entorno
    - Paso 1.1: instalar SQL Server
    - Paso 1,2 Instalación de Java
    - Paso 1,3 instalación del kit de desarrollo de Java (JDK)
    - Paso 1,4 Instalación de Maven
2. Creación de una aplicación Java con SQL Server
    - Paso 2,1 creación de una aplicación de Java que se conecta a SQL Server y ejecuta consultas
    - Paso 2,2 creación de una aplicación de Java que se conecta a SQL Server con el popular marco de hibernación
3. Haga que su aplicación de Java sea más rápida 100 veces
    - Paso 3,1 creación de una aplicación de Java para mostrar los índices de almacén de columnas

#### <a name="python-on-windows"></a>Python en Windows:

1. Configurar el entorno
    - Paso 1.1: instalar SQL Server
    - Paso 1,2 Instalación de Python
    - Paso 1,3 instalar el controlador ODBC y la utilidad de línea de comandos SQL para SQL Server
2. Creación de una aplicación de Python con SQL Server
    - Paso 2,1 instalación del controlador de Python para SQL Server
    - Paso 2,2 creación de una base de datos para la aplicación
    - Paso 2,3 creación de una aplicación de Python que se conecta a SQL Server y ejecuta consultas
3. Haga que su aplicación de Python se 100 veces más rápido
    - Paso 3,1 creación de una nueva tabla con 5 millones mediante SQLCMD
    - Paso 3,2 creación de una aplicación de Python que consulta esta tabla y mide el tiempo empleado
    - Paso 3,3 Mida cuánto tiempo se tarda en ejecutar la consulta
    - Paso 3,4 agregar un índice de almacén de columnas a la tabla
    - Paso 3,5 mida cuánto tiempo se tarda en ejecutar la consulta con un índice de almacén de columnas

Las siguientes capturas de pantallas le ofrecen una idea del aspecto que tiene nuestro sitio web de documentación de desarrollo de SQL.

#### <a name="choose-a-language"></a>Elija un idioma:

![Sitio web de desarrollo de SQL, introducción][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>Elija un sistema operativo:

![Sitio web de desarrollo de SQL, Ubuntu de Java][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>Otro desarrollo


En esta sección se proporcionan vínculos sobre otras opciones de desarrollo. Esto incluye el uso de estos mismos idiomas para el desarrollo de Azure en general. La información va más allá de tener como destino solo Azure SQL Database y Microsoft SQL Server.

#### <a name="developer-hub-for-azure"></a>Centro para desarrolladores de Azure

- [Centro para desarrolladores de Azure](https://docs.microsoft.com/azure/)
- [Azure para desarrolladores de .NET](https://docs.microsoft.com/dotnet/azure/)
- [Azure para desarrolladores de Java](https://docs.microsoft.com/java/azure/)
- [Azure para desarrolladores de node. js](https://docs.microsoft.com/nodejs/azure/)
- [Azure para desarrolladores de Python](https://docs.microsoft.com/python/azure/)
- [Creación de una aplicación Web de PHP en Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>Otros idiomas

- [Creación de aplicaciones de Go con SQL Server en Windows](https://www.microsoft.com/sql-server/developer-get-started/go/windows/)



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

