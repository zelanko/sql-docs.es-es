---
title: Conectarse a un origen de datos de Oracle (SQL Server importar y exportar) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b0bd1f5a-34dd-4be3-9ac8-f9f87727781b
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e589e7f7a0262d258342bf887ec84c57d57dc978
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-an-oracle-data-source-sql-server-import-and-export-wizard"></a>Conectarse a un origen de datos de Oracle (SQL Server importar y exportar)
Este tema muestra cómo conectarse a un **Oracle** del origen de datos de la **elegir un origen de datos** o **elegir un destino** página de la importación de SQL Server y el Asistente para exportación. Hay varios proveedores de datos que puede usar para conectar con Oracle.

> [!IMPORTANT]
> Los requisitos detallados y los requisitos previos para conectar a una base de datos de Oracle están fuera del ámbito de este artículo de Microsoft. En este artículo se da por supuesto que ya tiene instalado el software de cliente de Oracle y que puede ya conectarse correctamente a la base de datos de Oracle de destino. Para obtener más información, consulte la documentación de Oracle o el Administrador de base de datos de Oracle.

## <a name="connect-to-oracle-with-the-net-framework-data-provider-for-oracle"></a>Conectar con Oracle con .net Framework Data Provider para Oracle
Después de seleccionar **proveedor de datos de .NET Framework para Oracle** en el **elegir un origen de datos** o **elegir un destino** página del asistente, la página presenta una lista agrupada de opciones para el proveedor. Muchas de ellas son hostiles nombres y valores familiarizados. Afortunadamente, solo tendrá que proporcionar dos o tres partes de información. Puede pasar por alto los valores predeterminados para las demás opciones.

> [!NOTE]
> Las opciones de conexión para este proveedor de datos son los mismos si Oracle es el origen o el destino. Es decir, las opciones que ve son los mismos en ambos el **elegir un origen de datos** y **elegir un destino** páginas del asistente.

|Obtener la información necesaria|.NET framework Data Provider para la propiedad de Oracle|
|---|---|
|Nombre del servidor|**Origen de datos**|
|Información de autenticación (inicio de sesión)|**Id. de usuario** y **contraseña**; o bien, **la seguridad integrada**|

No tienes que escribir la cadena de conexión en el **ConnectionString** campo de la lista. Después de escribir valores individuales para el nombre del servidor de Oracle (**origen de datos**) y obtener información de inicio de sesión, el Asistente ensambla la cadena de conexión de las propiedades individuales y sus valores. 

![Conectar con Oracle con el proveedor de .NET](../../integration-services/import-export-data/media/connect-to-oracle-with-net-provider.jpg)

## <a name="connect-to-oracle-with-the-microsoft-odbc-driver-for-oracle"></a>Conectar con Oracle con el controlador ODBC de Microsoft para Oracle
Controladores ODBC no aparezcan en la lista desplegable de orígenes de datos. Para conectar con un controlador ODBC, empiece seleccionando la **proveedor de datos de .NET Framework para ODBC** como el origen de datos en el **elegir un origen de datos** o **elegir un destino** página. Este proveedor actúa como un contenedor para el controlador ODBC.

Esta es la pantalla genérica que se ve inmediatamente después de seleccionar el proveedor de datos de .NET Framework para ODBC.

![Conectar con Oracle con ODBC antes de](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-oracle"></a>Opciones para especificar (controlador de ODBC para Oracle)

> [!NOTE]
> Las opciones de conexión para este proveedor de datos y el controlador ODBC son los mismos si Oracle es el origen o el destino. Es decir, las opciones que ve son los mismos en ambos el **elegir un origen de datos** y **elegir un destino** páginas del asistente.

Para conectar con Oracle con el controlador ODBC para Oracle, ensamblar una cadena de conexión que incluye las siguientes opciones y sus valores. El formato de una cadena de conexión completa sigue inmediatamente a la lista de opciones.

> [!TIP]
> Obtener ayuda para ensamblar una cadena de conexión que está bien. O bien, en lugar de proporcionar una cadena de conexión, proporcionar un DSN (nombre de origen de datos) existente o crear uno nuevo. Para obtener más información acerca de estas opciones, consulte [conectar a un origen de datos ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Controlador**  
El nombre del controlador ODBC, **Microsoft ODBC para Oracle**.

**Server**  
El nombre del servidor de Oracle. 

**UID** y **Pwd**   
El Id. de usuario y la contraseña para conectarse.

### <a name="connection-string-format"></a>Formato de cadena de conexión
Este es el formato de cadena de conexión típica.

    ```
    Driver={Microsoft ODBC for Oracle};Server=myServerAddress;Uid=myUsername;Pwd=myPassword;
    ```

### <a name="enter-the-connection-string"></a>Escriba la cadena de conexión
Escriba la cadena de conexión en el **ConnectionString** campo o escriba el nombre DSN en el **Dsn** campo, en la **elegir un origen de datos** o **elegir un destino** página. Después de escribir la cadena de conexión, el asistente analiza la cadena y muestra las propiedades individuales y sus valores en la lista.

Esta es la pantalla que verá después de escribir la cadena de conexión.

![Conectar con Oracle con ODBC](../../integration-services/import-export-data/media/connect-to-oracle-with-odbc.jpg)

## <a name="whats-my-oracle-server-name"></a>¿Cuál es mi nombre de servidor de Oracle?
Ejecute una de las siguientes consultas para obtener el nombre del servidor Oracle.

`SELECT host_name FROM v$instance`

o bien

`SELECT sys_context('USERENV','SERVER_HOST') FROM dual`

## <a name="other-data-providers-and-more-info"></a>Otros proveedores de datos y obtener más información
Para obtener información acerca de cómo conectar con Oracle con un proveedor de datos que no aparece aquí, consulte [las cadenas de conexión de Oracle](https://www.connectionstrings.com/oracle/). Este sitio de terceros también contiene más información sobre los proveedores de datos y los parámetros de conexión descritos en esta página.

## <a name="see-also"></a>Vea también
[Elija un origen de datos](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Elegir un destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


