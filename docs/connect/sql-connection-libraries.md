---
title: Bibliotecas de conexiones para bases de datos de Microsoft SQL | Microsoft Docs
description: Proporciona vínculos de descarga para los módulos que permiten la conexión a Microsoft SQL Server y Azure SQL Database, desde diversos lenguajes de programación de cliente.
author: MightyPen
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: article
ms.date: 06/18/2018
ms.author: genemi
ms.openlocfilehash: 71254b937c4c0173af9e1549efb98a0b42f65e02
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632814"
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Módulos de conexión para las bases de datos de Microsoft SQL

En este artículo se proporcionan vínculos de descarga a *los* módulos de conexión o controladores que los programas cliente pueden usar para interactuar con [Microsoft SQL Server](../relational-databases/database-features.md)y con su gemela en el [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/)en la nube. Hay controladores disponibles para diversos lenguajes de programación, que se ejecutan en los siguientes sistemas operativos:

- Linux
- MacOS
- Windows

#### <a name="oop-to-relational-mismatch"></a>Programación de OOP a relacional

*Relacional*: los programas cliente que se escriben en un lenguaje de programación orientada a objetos (OOP) suelen usar controladores SQL que devuelven datos consultados en un formato más relacional que el objeto orientado a objetos. C#el uso de ADO.NET es un ejemplo. En ocasiones, la desigualdad de formatos relacionales y OOP hace que el código OOP sea más difícil de escribir y comprender.

*ORM*: otros controladores o marcos de trabajo devuelven datos consultados en el formato OOP y evitan la falta de coincidencia. Estos controladores funcionan esperando que las clases se hayan definido para que coincidan con las columnas de datos de tablas SQL concretas. A continuación, el controlador realiza la *asignación relacional de objetos* (ORM) para devolver los datos consultados como una instancia de una clase. Entity Framework de Microsoft (EF) para C#, e hibernación para Java, son dos ejemplos.

En el presente artículo se detienen secciones independientes para estos dos tipos de controladores de conexión.

<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>Controladores para el acceso relacional


<!--
Each given Microsoft Download Center page should be enhanced
with a link to the next NEWER version page, on the day that the
original page is no longer the latest because the newer page is being added.
But this policy is not agreed on or observed,
putting the links in the following table at risk for being outdated.

PHP driver in Github.com also uses this FWLink:  https://go.microsoft.com/fwlink/?LinkID=518036 ,
although the FWLink is less precise than is https://github.com/Microsoft/msphpsql/tree/dev#install-unix .
-->

| Idioma | Descargar el controlador de SQL |
| :------- | :---------------------- |
| C# | [ADO.NET](https://www.microsoft.com/net/download/)<br />[Microsoft.Data.SqlClient](https://www.nuget.org/packages/Microsoft.Data.SqlClient/)<br /><br />[.NET Core, para Linux-Ubuntu](https://www.microsoft.com/net/core#Ubuntu)<br />[.NET Core, para MacOS](https://www.microsoft.com/net/core#macos)<br />[.NET Core, para Windows](https://www.microsoft.com/net/core) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/download-oledb-driver-for-sql-server.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Controlador de node. js, instrucciones de instalación](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | [PHP](./php/download-drivers-php-sql-server.md) |
| Python | [pyodbc, instrucciones de instalación](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[Descargar ODBC](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Controlador de Ruby, instrucciones de instalación](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Página de descarga de Ruby](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br /> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>Controladores para el acceso ORM


En la tabla siguiente se muestran ejemplos de marcos de trabajo de asignación relacional de objetos (ORM) que las aplicaciones cliente utilizan para conectarse a las bases de datos de Microsoft SQL.


| Idioma | Descarga del controlador ORM |
| :------- | :------------------ |
| C# | [Entity Framework Core](https://docs.microsoft.com/ef/core/)<br />[Entity Framework (6. x o posterior)](https://docs.microsoft.com/ef/) |
| Java | [Hibernate ORM](https://hibernate.org/orm)|
| PHP | [Eloquent ORM, incluido en Laravel install](https://laravel.com/docs/) |
| Node.js | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | [Django](https://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) |


<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>Páginas web de compilación a aplicación
[https://aka.ms/sqldev](https://aka.ms/sqldev) le lleva a un conjunto de páginas web de *compilación a aplicación* . Las páginas web proporcionan información sobre numerosas combinaciones de lenguaje de programación, sistema operativo y controlador de conexión SQL. Entre la información proporcionada por las páginas web de compilación-a-aplicación se encuentran los siguientes elementos:

- Detalles sobre cómo empezar desde el principio, para cada combinación de idioma + sistema operativo + controlador.
    - Instrucciones para instalar los controladores de conexión de SQL más recientes.
- Ejemplos de código para cada uno de los siguientes elementos:
    - Ejemplos de código relacional de objetos.
    - Ejemplos de código ORM.
    - Demostraciones de índices de almacén de columnas para un rendimiento mucho más rápido.

#### <a name="first-page-of-build-an-app-webpages"></a>Primera página, de páginas web de compilación a aplicación
![Compilar: Página Web de una aplicación, captura de pantalla de la primera página][image-ref-163-buildanapp-webpages-first-page]

#### <a name="menu-for-java---ubuntu-of-build-an-app-webpages"></a>Menú para Java-Ubuntu, de páginas web de compilación a aplicación
![Compilar: páginas web de la aplicación, menú Ubuntu de Java][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

&nbsp;

## <a name="related-links"></a>Vínculos relacionados
- [Ejemplos de código para conectarse a Azure SQL Database en la nube, con Java y otros lenguajes](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java).

<!-- Image references -->

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
