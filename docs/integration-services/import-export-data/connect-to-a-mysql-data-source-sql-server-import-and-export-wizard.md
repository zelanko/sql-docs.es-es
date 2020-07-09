---
title: Conectarse a un origen de datos MySQL (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3d7c5a38-18d3-4cc9-a241-04422cb250d3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fdec318d9fdc895470c7dde94e254c2cc164f079
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85768083"
---
# <a name="connect-to-a-mysql-data-source-sql-server-import-and-export-wizard"></a>Conectarse a un origen de datos MySQL (Asistente para importación y exportación de SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


En este tema se muestra cómo conectarse a un origen de datos **MySQL** desde la página **Elegir un origen de datos** o **Elegir un destino** del asistente para importación y exportación de SQL Server. Hay varios proveedores de datos que puede usar para conectarse a MySQL.

> [!IMPORTANT]
> Los requisitos detallados y los requisitos previos para conectarse a una base de datos MySQL no se indicarán en este artículo de Microsoft. En este artículo se da por supuesto que ya tiene instalado el software de cliente MySQL y que puede conectarse correctamente a la base de datos de destino MySQL. Para obtener más información, consulte la documentación de MySQL o el administrador de base de datos MySQL.

## <a name="get-the-mysql-connectors"></a>Obtener los conectores de MySQL
Descargue los proveedores y los controladores que se describen en este tema desde la página [Conectores de MySQL](https://dev.mysql.com/downloads/connector/).

## <a name="connect-to-mysql-with-the-net-framework-data-provider-for-mysql"></a>Conectarse a MySQL con el proveedor de datos de .NET Framework para MySQL
Después de seleccionar el **proveedor de datos de .NET Framework para MySQL** en la página **Elegir un origen de datos** o **Elegir un destino** del asistente, la página muestra una lista agrupada de opciones del proveedor. Muchas de ellas aparecen con nombres y valores de configuración extraños. Afortunadamente, solo tendrá que proporcionar cierta información. Así que puede ignorar los valores predeterminados de las demás opciones.

> [!NOTE]
> Las opciones de conexión de este proveedor de datos son las mismas independientemente de si MySQL es el origen o el destino. Es decir, las opciones que ve son las mismas en las páginas **Elegir un origen de datos** y **Elegir un destino** del asistente.

|Información requerida|Proveedor de datos de .NET Framework para la propiedad MySQL|
|---|---|
|Nombre de servidor|**Server**|
|Nombre de la base de datos|**Base de datos**|
|Información de autenticación (inicio de sesión)|**Id. de usuario** y **contraseña**|
|||

No tiene que escribir la cadena de conexión en el campo **ConnectionString** de la lista. Después de escribir los valores individuales del nombre del servidor de MySQL (**Server**) y obtener la información de inicio de sesión, el asistente ensambla la cadena de conexión de las propiedades individuales y sus valores. 

![Conectarse a MySQL con el proveedor. NET, 1 de 2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-1-of-2.png)

![Conectarse a MySQL con el proveedor. NET, 2 de 2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-2-of-2.png)

## <a name="connect-to-mysql-with-the-mysql-odbc-driver"></a>Conectarse a MySQL con el controlador ODBC de MySQL
Los controladores ODBC no aparecen en la lista desplegable de los orígenes de datos. Para conectarse con un controlador ODBC, empiece seleccionando el **proveedor de datos de .NET Framework para ODBC** como origen de datos en la página **Elegir un origen de datos** o **Elegir un destino**. Este proveedor actúa como un contenedor para el controlador ODBC.

Esta es la pantalla genérica que se ve inmediatamente después de seleccionar el proveedor de datos de .NET Framework para ODBC.

![Conectarse antes a SQL con ODBC](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-mysql-odbc-driver"></a>Opciones que hay que especificar (controlador ODBC de MySQL)

> [!NOTE]
> Las opciones de conexión de este proveedor de datos y el controlador ODBC son las mismas independientemente de si MySQL es el origen o el destino. Es decir, las opciones que ve son las mismas en las páginas **Elegir un origen de datos** y **Elegir un destino** del asistente.

Para conectarse a MySQL con el controlador ODBC de MySQL, ensamble una cadena de conexión que incluya las siguientes opciones y sus valores. El formato de una cadena de conexión completa aparece inmediatamente después de la lista de opciones.

> [!TIP]
> Obtenga ayuda para ensamblar una cadena de conexión que funcione correctamente. O bien, en lugar de proporcionar una cadena de conexión, puede proporcionar un DSN (nombre de origen de datos) existente o crear uno nuevo. Para obtener más información acerca de estas opciones, consulte [Conectarse a un origen de datos ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Controlador**  
Nombre del controlador ODBC.

**Server**  
Nombre del servidor de MySQL. 

**Base de datos**  
Nombre de la base de datos de MySQL.

**UID** y **PWD**   
Son el id. de usuario y la contraseña para conectarse.

### <a name="connection-string-format"></a>Formato de la cadena de conexión
Este es el formato de una cadena de conexión típica.

```console
Driver={MySQL ODBC 5.3 Unicode Driver};Server=<server>;Database=<database>;UID=<user id>;PWD=<password>
```

### <a name="enter-the-connection-string"></a>Escribir la cadena de conexión
Escriba la cadena de conexión en el campo **ConnectionString** o escriba el nombre DSN en el campo **DSN**, que se encuentra en la página **Elegir un origen de datos** o **Elegir un destino**. Después de escribir la cadena de conexión, el asistente la analiza y muestra las propiedades individuales y sus valores en la lista.

En el siguiente ejemplo se emplea esta cadena de conexión.

```console
Driver={MySQL ODBC 5.3 Unicode Driver};Server=127.0.0.1;Database=world;UID=root;PWD=********
```

Esta es la pantalla que verá después de escribir la cadena de conexión.

![Conectarse a MySQL con ODBC](../../integration-services/import-export-data/media/connect-to-mysql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>Otros proveedores de datos y más información
Para obtener más información sobre cómo conectarse a MySQL con un proveedor de datos que no aparezca en esta lista, consulte [MySQL connection strings (Cadenas de conexión de MySQL)](https://www.connectionstrings.com/mysql/). En este sitio de terceros también encontrará más información sobre los proveedores de datos y los parámetros de conexión que se describen en esta página.

## <a name="see-also"></a>Consulte también
[Choose a Data Source](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md) (Selección de un origen de datos)  
[Choose a Destination](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md) (Selección de un destino)

