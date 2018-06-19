---
title: Conectar a un origen de datos de Oracle (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b0bd1f5a-34dd-4be3-9ac8-f9f87727781b
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3fe47762ce9aac0d8a077bf7843a62a9aaf6ca61
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35330079"
---
# <a name="connect-to-an-oracle-data-source-sql-server-import-and-export-wizard"></a>Conectarse a un origen de datos de Oracle (Asistente para importación y exportación de SQL Server)
En este tema se muestra cómo conectarse a un origen de datos **Oracle** desde la página **Elegir un origen de datos** o **Elegir un destino** del asistente para importación y exportación de SQL Server. Hay varios proveedores de datos que puede usar para conectarse a Oracle.

> [!IMPORTANT]
> Los requisitos detallados y los requisitos previos para conectarse a una base de datos de Oracle no se indicarán en este artículo de Microsoft. En este artículo se da por supuesto que ya tiene instalado el software de cliente Oracle y que puede conectarse correctamente a la base de datos de destino de Oracle. Para obtener más información, consulte la documentación de Oracle o el administrador de base de datos de Oracle.

## <a name="connect-to-oracle-with-the-net-framework-data-provider-for-oracle"></a>Conectarse a Oracle con el proveedor de datos de .NET Framework para Oracle
Después de seleccionar el **proveedor de datos de .NET Framework para Oracle** en la página **Elegir un origen de datos** o **Elegir un destino** del asistente, la página muestra una lista agrupada de opciones del proveedor. Muchas de ellas aparecen con nombres y valores de configuración extraños. Afortunadamente, solo tendrá que proporcionar dos o tres datos. Así que puede ignorar los valores predeterminados de las demás opciones.

> [!NOTE]
> Las opciones de conexión de este proveedor de datos son las mismas independientemente de si Oracle es el origen o el destino. Es decir, las opciones que ve son las mismas en las páginas **Elegir un origen de datos** y **Elegir un destino** del asistente.

|Información requerida|Proveedor de datos de .NET Framework de la propiedad de Oracle|
|---|---|
|Nombre del servidor|**Origen de datos**|
|Información de autenticación (inicio de sesión)|**Id. de usuario** y **contraseña** o **seguridad integrada**|

No tiene que escribir la cadena de conexión en el campo **ConnectionString** de la lista. Después de escribir los valores individuales del nombre del servidor de Oracle (**Origen de datos**) y obtener la información de inicio de sesión, el asistente ensambla la cadena de conexión de las propiedades individuales y sus valores. 

![Conectarse a Oracle con el proveedor de .NET](../../integration-services/import-export-data/media/connect-to-oracle-with-net-provider.jpg)

## <a name="connect-to-oracle-with-the-microsoft-odbc-driver-for-oracle"></a>Conectarse a Oracle con el controlador ODBC de Microsoft para Oracle
Los controladores ODBC no aparecen en la lista desplegable de los orígenes de datos. Para conectarse con un controlador ODBC, empiece seleccionando el **proveedor de datos de .NET Framework para ODBC** como origen de datos en la página **Elegir un origen de datos** o **Elegir un destino**. Este proveedor actúa como un contenedor para el controlador ODBC.

Esta es la pantalla genérica que se ve inmediatamente después de seleccionar el proveedor de datos de .NET Framework para ODBC.

![Conectarse antes a Oracle con ODBC](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-oracle"></a>Opciones que hay que especificar (controlador ODBC para Oracle)

> [!NOTE]
> Las opciones de conexión de este proveedor de datos y el controlador ODBC son las mismas independientemente de si Oracle es el origen o el destino. Es decir, las opciones que ve son las mismas en las páginas **Elegir un origen de datos** y **Elegir un destino** del asistente.

Para conectarse a Oracle con el controlador ODBC de Oracle, ensamble una cadena de conexión que incluya las siguientes opciones y sus valores. El formato de una cadena de conexión completa aparece inmediatamente después de la lista de opciones.

> [!TIP]
> Obtenga ayuda para ensamblar una cadena de conexión que funcione correctamente. O bien, en lugar de proporcionar una cadena de conexión, puede proporcionar un DSN (nombre de origen de datos) existente o crear uno nuevo. Para obtener más información acerca de estas opciones, consulte [Conectarse a un origen de datos ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Controlador**  
Es el nombre del controlador ODBC, **Microsoft ODBC para Oracle**.

**Server**  
Es el nombre del servidor de Oracle. 

**Uid** y **Pwd**   
Son el id. de usuario y la contraseña para conectarse.

### <a name="connection-string-format"></a>Formato de la cadena de conexión
Este es el formato de una cadena de conexión típica.

    ```
    Driver={Microsoft ODBC for Oracle};Server=myServerAddress;Uid=myUsername;Pwd=myPassword;
    ```

### <a name="enter-the-connection-string"></a>Escribir la cadena de conexión
Escriba la cadena de conexión en el campo **ConnectionString** o escriba el nombre DSN en el campo **DSN**, que se encuentra en la página **Elegir un origen de datos** o **Elegir un destino**. Después de escribir la cadena de conexión, el asistente la analiza y muestra las propiedades individuales y sus valores en la lista.

Esta es la pantalla que verá después de escribir la cadena de conexión.

![Conectarse a Oracle con ODBC](../../integration-services/import-export-data/media/connect-to-oracle-with-odbc.jpg)

## <a name="whats-my-oracle-server-name"></a>¿Cuál es mi nombre de servidor de Oracle?
Ejecute una de las siguientes consultas para obtener el nombre del servidor de Oracle.

`SELECT host_name FROM v$instance`

o Administrador de configuración de

`SELECT sys_context('USERENV','SERVER_HOST') FROM dual`

## <a name="other-data-providers-and-more-info"></a>Otros proveedores de datos y más información
Para obtener más información sobre cómo conectarse a Oracle con un proveedor de datos que no aparezca en esta lista, consulte [Oracle connection strings (Cadenas de conexión de Oracle)](https://www.connectionstrings.com/oracle/). En este sitio de terceros también encontrará más información sobre los proveedores de datos y los parámetros de conexión que se describen en esta página.

## <a name="see-also"></a>Vea también
[Choose a Data Source](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md) (Selección de un origen de datos)  
[Choose a Destination](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md) (Selección de un destino)

