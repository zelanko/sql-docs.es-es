---
title: Bibliotecas de conexiones de bases de datos de Microsoft SQL | Microsoft Docs
description: Proporciona vínculos de descarga de módulos que permiten la conexión a Microsoft SQL Server y Azure SQL Database, desde una variedad de lenguajes de programación de cliente.
author: MightyPen
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: article
ms.date: 06/18/2018
ms.author: genemi
ms.openlocfilehash: 7f759dbe9022cff557461d900a35b3ccc91d2c4b
ms.sourcegitcommit: 0f452eca5cf0be621ded80fb105ba7e8df7ac528
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2019
ms.locfileid: "57007578"
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Módulos de conexión para bases de datos SQL de Microsoft

En este artículo proporciona vínculos de descarga de módulos de conexión o *controladores* que los programas cliente pueden usar para interactuar con [Microsoft SQL Server](../relational-databases/database-features.md)y con su gemelo en la nube [Azure Base de datos SQL](https://docs.microsoft.com/azure/sql-database/). Los controladores están disponibles para una variedad de lenguajes de programación, que se ejecutan en los sistemas operativos siguientes:

- Linux
- MacOS
- Windows

#### <a name="oop-to-relational-mismatch"></a>Error de coincidencia de OOP a relacional

*Relacional*: programas cliente que se escriben en un lenguaje de (OOP) de programación orientada a objetos suelen utilizan controladores SQL que devuelven datos consultados en un formato que sea más relacional que orientada a objetos. C# mediante ADO.NET es un ejemplo. La programación orientada a objetos relacionales incompatibilidad de formato a veces hace que el código de programación orientada a objetos es más difícil de escribir y comprender.

*ORM*: otros controladores o marcos de devuelven los datos consultados en el formato OOP, evitar la falta de coincidencia. Estos controladores funcionan por se espera que las clases se han definido para que coincida con las columnas de datos de tablas SQL. El controlador, a continuación, realiza el *asignación objeto-relacional* (ORM) para devolver los datos consultados como una instancia de una clase. Entity Framework (EF de Microsoft) para C# e hibernación para Java, son dos ejemplos.

El presente artículo dedica secciones independientes para estos dos tipos de controladores de conexión.

<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>Controladores para acceso relacional


<!--
Each given Microsoft Download Center page should be enhanced
with a link to the next NEWER version page, on the day that the
original page is no longer the latest because the newer page is being added.
But this policy is not agreed on or observed,
putting the links in the following table at risk for being outdated.

PHP driver in Github.com also uses this FWLink:  https://go.microsoft.com/fwlink/?LinkID=518036 ,
although the FWLink is less precise than is https://github.com/Microsoft/msphpsql/tree/dev#install-unix .
-->

| Idioma | Descargue el controlador SQL |
| :------- | :---------------------- |
| C# | [ADO.NET](https://www.microsoft.com/net/download/)<br /><br />[.NET core, para Linux Ubuntu](https://www.microsoft.com/net/core#Ubuntu)<br />[.NET core, para MacOS](https://www.microsoft.com/net/core#macos)<br />[.NET core, para Windows](https://www.microsoft.com/net/core) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/download-oledb-driver-for-sql-server.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Controlador de Node.js, las instrucciones de instalación](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | [PHP](./php/download-drivers-php-sql-server.md) |
| Python | [pyodbc, instrucciones de instalación](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[Descargar ODBC](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Controlador de Ruby, las instrucciones de instalación](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Página de descarga de Ruby](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br /> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>Controladores para el acceso a ORM


En la tabla siguiente se muestra ejemplos de marcos de asignación relacional de objetos (ORM) que las aplicaciones cliente utilizan para conectarse a bases de datos SQL de Microsoft.


| Idioma | Descarga del controlador ORM |
| :------- | :------------------ |
| C# | [Entity Framework Core](https://docs.microsoft.com/ef/core/)<br />[Entity Framework (6.x o posterior)](https://docs.microsoft.com/ef/) |
| Java | [Hibernar ORM](https://hibernate.org/orm)|
| PHP | [Elocuente ORM, incluido en la instalación de Laravel](https://laravel.com/docs/) |
| Node.js | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | [Django](https://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) |


<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>Páginas Web de una aplicación compilada
[https://aka.ms/sqldev](https://aka.ms/sqldev) le lleva a un conjunto de *una aplicación compilada* las páginas Web. Las páginas Web proporcionan información sobre diversas combinaciones de lenguaje de programación, sistema operativo y el controlador de conexión de SQL. Entre la información proporcionada por las páginas Web de una aplicación compilada se encuentran los siguientes elementos:

- Más información sobre cómo empezar a trabajar desde el principio, para cada combinación de idioma del sistema operativo + controlador.
    - Instrucciones para instalar a los controladores más recientes de conexión de SQL.
- Ejemplos de código para cada uno de los siguientes elementos:
    - Ejemplos de código objeto-relacional.
    - Ejemplos de código ORM.
    - Demostraciones de índice de almacén de columnas para un rendimiento mucho más rápido.

#### <a name="first-page-of-build-an-app-webpages"></a>Primera página, de las páginas Web de una aplicación compilada
![Páginas Web de una aplicación compilada, primera captura de pantalla de página][image-ref-163-buildanapp-webpages-first-page]

#### <a name="menu-for-java---ubuntu-of-build-an-app-webpages"></a>Menú para Java: Ubuntu, de las páginas Web de una aplicación compilada
![Páginas Web de una aplicación compilada, menú Ubuntu de Java][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

&nbsp;

## <a name="related-links"></a>Vínculos relacionados
- [Ejemplos de código para conectarse a Azure SQL Database en la nube, con Java y otros lenguajes](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java).

<!-- Image references -->

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
