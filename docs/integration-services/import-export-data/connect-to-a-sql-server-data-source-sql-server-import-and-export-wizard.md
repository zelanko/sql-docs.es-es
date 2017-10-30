---
title: Conectarse a un origen de datos SQL Server (SQL Server importar y exportar) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 386cedbb-fae5-45ce-9363-c4a417f80a2f
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 17910c8e30dee98f39e977896fb67774b54a798d
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard"></a>Conectarse a un origen de datos SQL Server (SQL Server importar y exportar)
Este tema muestra cómo conectarse a un **Microsoft SQL Server** del origen de datos de la **elegir un origen de datos** o **elegir un destino** página de la importación de SQL Server y el Asistente para exportación. Hay varios proveedores de datos que puede usar para conectarse a SQL Server.

> [!TIP]
> Si está en una red con varios servidores, probablemente sea más fácil escribir el nombre del servidor en lugar de expandir la lista desplegable de servidores. Si hace clic en la lista desplegable, puede tardar mucho tiempo para consultar todos los servidores disponibles en la red y los resultados no pueden incluir incluso el servidor que desee.

## <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>Conectarse a SQL Server con el Proveedor de datos de .NET Framework para SQL Server 
Después de seleccionar **proveedor de datos de .NET Framework para SQL Server** en el **elegir un origen de datos** o **elegir un destino** página del asistente, la página muestra una lista agrupada de opciones para el proveedor. Muchas de ellas son hostiles nombres y valores familiarizados. Afortunadamente, para conectarse a cualquier base de datos de empresa, normalmente tendrá que proporcionar sólo algunas partes de información. Puede pasar por alto los valores predeterminados para las demás opciones.

> [!NOTE]
> Las opciones de conexión para este proveedor de datos son los mismos si SQL Server es el origen o el destino. Es decir, las opciones que ve son los mismos en ambos el **elegir un origen de datos** y **elegir un destino** páginas del asistente.

|Obtener la información necesaria|.NET framework Data Provider para la propiedad de SQL Server|
|---|---|
|Nombre del servidor|**Origen de datos**|
|Información de autenticación (inicio de sesión)|**La seguridad integrada de**; o bien, **Id. de usuario** y **contraseña**<br/>Si desea ver una lista desplegable de bases de datos en el servidor, primero debe proporcionar información de inicio de sesión válido.|
|Nombre de la base de datos|**Catálogo original**|

![Conectarse a SQL con el proveedor de .NET](../../integration-services/import-export-data/media/connect-to-sql-with-net-provider.jpg)

### <a name="options-to-specify-net-framework-data-provider-for-sql-server"></a>Opciones para especificar (proveedor de datos de .NET Framework para SQL Server)

> [!NOTE]
> Las opciones de conexión para este proveedor de datos son los mismos si SQL Server es el origen o el destino. Es decir, las opciones que ve son los mismos en ambos el **elegir un origen de datos** y **elegir un destino** páginas del asistente.

**Origen de datos**  
 Escriba el nombre o dirección IP del servidor de origen o destino, o seleccione un servidor en la lista desplegable.  
 
 Para especificar un puerto TCP no estándar, escriba una coma después del nombre del servidor o dirección IP y, a continuación, escriba el número de puerto.
 
 **Catálogo original**  
 Escriba el nombre de la base de datos de origen o destino, o seleccione una base de datos de la lista desplegable.  
  
 **Seguridad integrada**  
 Especifique **True** para conectar con la autenticación integrada de Windows (recomendada), o **False** para conectar con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación. Si especifica **False**, debe especificar un Id. de usuario y una contraseña. El valor predeterminado es **False**.  
  
 **Id. de usuario**  
 Escriba un nombre de usuario si usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación.  
  
 **Contraseña**  
 Escriba la contraseña si usas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación.  

## <a name="connect-to-sql-server-with-the-odbc-driver-for-sql-server"></a>Conectarse a SQL Server con el controlador ODBC para SQL Server 
Controladores ODBC no aparezcan en la lista desplegable de orígenes de datos. Para conectar con un controlador ODBC, empiece seleccionando la **proveedor de datos de .NET Framework para ODBC** como origen de datos. Este proveedor actúa como un contenedor para el controlador ODBC.

> [!TIP]
> **Obtenga el controlador más reciente**. Descargue el [Microsoft ODBC Driver 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53339).

Esta es la pantalla genérica que se ve inmediatamente después de seleccionar el proveedor de datos de .NET Framework para ODBC.

![Conectarse a SQL con ODBC antes de](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-sql-server"></a>Opciones para especificar (controlador ODBC para SQL Server)

> [!NOTE]
> Las opciones de conexión para el controlador ODBC son los mismos si SQL Server es el origen o el destino. Es decir, las opciones que ve son los mismos en ambos el **elegir un origen de datos** y **elegir un destino** páginas del asistente.

Para conectarse a SQL Server con el controlador ODBC más reciente, ensamblar una cadena de conexión que incluye las siguientes opciones y sus valores. El formato de una cadena de conexión completa sigue inmediatamente a la lista de opciones.

> [!TIP]
> Obtener ayuda para ensamblar una cadena de conexión que está bien. O bien, en lugar de proporcionar una cadena de conexión, proporcionar un DSN (nombre de origen de datos) existente o crear uno nuevo. Para obtener más información acerca de estas opciones, consulte [conectar a un origen de datos ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Controlador**  
El nombre del controlador ODBC. El nombre es diferente para distintas versiones del controlador.

**Server**  
El nombre de SQL Server.

**Base de datos**  
El nombre de la base de datos.  

**Trusted_Connection**; o bien, **Uid** y **Pwd**  
Especifique **Trusted_Connection = Yes** para conectarse con la autenticación integrada de Windows; o bien, especifique **Uid** (Id. de usuario) y **Pwd** (contraseña) para conectarse con la autenticación de SQL Server.

### <a name="connection-string-format"></a>Formato de cadena de conexión
Este es el formato de una cadena de conexión que usa la autenticación integrada de Windows.

    `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;trusted_connection=Yes;`

Este es el formato de una cadena de conexión que utiliza autenticación de SQL Server en lugar de la autenticación integrada de Windows.

     `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;uid=<user id>;pwd=<password>;`

### <a name="enter-the-connection-string"></a>Escriba la cadena de conexión
Escriba la cadena de conexión en el **ConnectionString** campo o escriba el nombre DSN en el **Dsn** campo, en la **elegir un origen de datos** o **elegir un destino** página. Después de escribir la cadena de conexión, el asistente analiza la cadena y muestra las propiedades individuales y sus valores en la lista.

En el ejemplo siguiente se utiliza esta cadena de conexión.

    `Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;`

Esta es la pantalla que verá después de escribir la cadena de conexión.

![Conectarse a SQL con ODBC después de](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="connect-to-sql-server-with-the-microsoft-ole-db-provider-for-sql-server-or-sql-server-native-client"></a>Conectarse a SQL Server con el proveedor Microsoft OLE DB para SQL Server o SQL Server Native Client

> [!IMPORTANT]
> El proveedor Microsoft OLE DB para SQL Server y SQL Server Native Client no se admiten en versiones de SQL Server después de SQL Server 2012. Utilice el controlador ODBC en su lugar. Para obtener más información sobre la transición para el controlador ODBC, vea las entradas de blog siguientes.
>   -   [Microsoft se alinea con ODBC para el acceso de datos relacionales nativos](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)
>   -   [Introducción a los nuevos controladores ODBC de Microsoft para SQL Server](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/)

## <a name="other-data-providers-and-more-info"></a>Otros proveedores de datos y obtener más información
Para obtener información sobre cómo conectarse a SQL Server con un proveedor de datos que no aparece aquí, consulte [las cadenas de conexión de SQL Server](https://www.connectionstrings.com/sql-server/). Este sitio de terceros también contiene más información sobre los proveedores de datos y los parámetros de conexión descritos en esta página.

## <a name="see-also"></a>Vea también
[Elija un origen de datos](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Elegir un destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


