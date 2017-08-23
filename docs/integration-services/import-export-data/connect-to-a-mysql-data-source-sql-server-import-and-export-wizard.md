---
title: Conectarse a un origen de datos de MySQL (SQL Server importar y exportar) | Documentos de Microsoft
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3d7c5a38-18d3-4cc9-a241-04422cb250d3
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3df56fcda5b39c2895de83feac4f302686b1adf3
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-mysql-data-source-sql-server-import-and-export-wizard"></a>Conectarse a un origen de datos de MySQL (importación de SQL Server y Asistente para exportación)
Este tema muestra cómo conectarse a un **MySQL** del origen de datos de la **elegir un origen de datos** o **elegir un destino** página de la importación de SQL Server y el Asistente para exportación. Hay varios proveedores de datos que puede usar para conectarse a MySQL.

> [!IMPORTANT]
> Los requisitos detallados y los requisitos previos para conectarse a una base de datos de MySQL quedan fuera del ámbito de este artículo de Microsoft. En este artículo se da por supuesto que ya tiene instalado el software de cliente de MySQL y que puede ya conectarse correctamente a la base de datos de MySQL de destino. Para obtener más información, consulte la documentación de MySQL o el Administrador de base de datos de MySQL.

## <a name="get-the-mysql-connectors"></a>Obtenga los conectores de MySQL
Descargar los proveedores y controladores que se describe en este tema de la [conectores de MySQL](https://dev.mysql.com/downloads/connector/) página.

## <a name="connect-to-mysql-with-the-net-framework-data-provider-for-mysql"></a>Conectarse a MySQL con .net Framework Data Provider para MySQL
Después de seleccionar **.NET Framework Data Provider para MySQL** en el **elegir un origen de datos** o **elegir un destino** página del asistente, la página presenta una lista agrupada de opciones para el proveedor. Muchas de ellas son hostiles nombres y valores familiarizados. Afortunadamente, solo tendrá que proporcionar cierta información. Puede pasar por alto los valores predeterminados para las demás opciones.

> [!NOTE]
> Las opciones de conexión para este proveedor de datos son los mismos si MySQL es el origen o el destino. Es decir, las opciones que ve son los mismos en ambos el **elegir un origen de datos** y **elegir un destino** páginas del asistente.

|Obtener la información necesaria|.NET framework Data Provider para la propiedad de MySQL|
|---|---|
|Nombre del servidor|**Server**|
|Nombre de la base de datos|**Base de datos**|
|Información de autenticación (inicio de sesión)|**Id. de usuario** y **contraseña**|

No tienes que escribir la cadena de conexión en el **ConnectionString** campo de la lista. Después de escribir valores individuales para el nombre del servidor MySQL (**Server**) y obtener información de inicio de sesión, el Asistente ensambla la cadena de conexión de las propiedades individuales y sus valores. 

![Conectarse a MySQL con el proveedor. NET, 1 de 2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-1-of-2.png)

![Conectarse a MySQL con el proveedor. NET, 2 de 2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-2-of-2.png)

## <a name="connect-to-mysql-with-the-mysql-odbc-driver"></a>Conectarse a MySQL con el controlador ODBC de MySQL
Controladores ODBC no aparezcan en la lista desplegable de orígenes de datos. Para conectar con un controlador ODBC, empiece seleccionando la **proveedor de datos de .NET Framework para ODBC** como el origen de datos en el **elegir un origen de datos** o **elegir un destino** página. Este proveedor actúa como un contenedor para el controlador ODBC.

Esta es la pantalla genérica que se ve inmediatamente después de seleccionar el proveedor de datos de .NET Framework para ODBC.

![Conectarse a SQL con ODBC antes de](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-mysql-odbc-driver"></a>Opciones para especificar (controlador de ODBC de MySQL)

> [!NOTE]
> Las opciones de conexión para este proveedor de datos y el controlador ODBC son los mismos si MySQL es el origen o el destino. Es decir, las opciones que ve son los mismos en ambos el **elegir un origen de datos** y **elegir un destino** páginas del asistente.

Para conectarse a MySQL con el controlador ODBC de MySQL, ensamblar una cadena de conexión que incluye las siguientes opciones y sus valores. El formato de una cadena de conexión completa sigue inmediatamente a la lista de opciones.

> [!TIP]
> Obtener ayuda para ensamblar una cadena de conexión que está bien. O bien, en lugar de proporcionar una cadena de conexión, proporcionar un DSN (nombre de origen de datos) existente o crear uno nuevo. Para obtener más información acerca de estas opciones, consulte [conectar a un origen de datos ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Controlador**  
El nombre del controlador ODBC.

**Server**  
El nombre del servidor MySQL. 

**Base de datos**  
El nombre de la base de datos de MySQL.

**UID** y **PWD**   
El Id. de usuario y la contraseña para conectarse.

### <a name="connection-string-format"></a>Formato de cadena de conexión
Este es el formato de cadena de conexión típica.

    Driver={MySQL ODBC 5.3 Unicode Driver};Server=<server>;Database=<database>;UID=<user id>;PWD=<password>

### <a name="enter-the-connection-string"></a>Escriba la cadena de conexión
Escriba la cadena de conexión en el **ConnectionString** campo o escriba el nombre DSN en el **Dsn** campo, en la **elegir un origen de datos** o **elegir un destino** página. Después de escribir la cadena de conexión, el asistente analiza la cadena y muestra las propiedades individuales y sus valores en la lista.

En el ejemplo siguiente se utiliza esta cadena de conexión.

    Driver={MySQL ODBC 5.3 Unicode Driver};Server=127.0.0.1;Database=world;UID=root;PWD=********

Esta es la pantalla que verá después de escribir la cadena de conexión.

![Conectarse a MySQL con ODBC](../../integration-services/import-export-data/media/connect-to-mysql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>Otros proveedores de datos y obtener más información
Para obtener información acerca de cómo conectar con MySQL con un proveedor de datos que no aparece aquí, consulte [las cadenas de conexión de MySQL](https://www.connectionstrings.com/mysql/). Este sitio de terceros también contiene más información sobre los proveedores de datos y los parámetros de conexión descritos en esta página.

## <a name="see-also"></a>Vea también
[Elija un origen de datos](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Elegir un destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


