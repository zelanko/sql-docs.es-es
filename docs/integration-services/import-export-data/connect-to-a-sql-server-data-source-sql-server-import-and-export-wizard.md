---
title: Conectarse a un origen de datos de SQL Server (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 386cedbb-fae5-45ce-9363-c4a417f80a2f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 938a6d8ba779d1cef37b5fab767e609d00b4f022
ms.sourcegitcommit: aaa42f26c68abc2de10eb58444fe6b490c174eab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2019
ms.locfileid: "74308006"
---
# <a name="connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard"></a>Conectarse a un origen de datos de SQL Server (Asistente para importación y exportación de SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


En este tema se muestra cómo conectarse a un origen de datos de **Microsoft SQL Server** desde la página **Elegir un origen de datos** o **Elegir un destino** del Asistente para importación y exportación de SQL Server. Hay varios proveedores de datos que puede usar para conectarse a SQL Server.

> [!TIP]
> Si está en una red con varios servidores, probablemente sea más fácil escribir el nombre del servidor que expandir la lista desplegable de servidores. Si hace clic en la lista desplegable, puede tardar mucho tiempo en consultar la red para obtener todos los servidores disponibles y los resultados podrían no incluir el servidor deseado.

## <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>Conectarse a SQL Server con el Proveedor de datos de .NET Framework para SQL Server 
Después de seleccionar el **proveedor de datos de .NET Framework para SQL Server** en la página **Elegir un origen de datos** o **Elegir un destino** del asistente, la página muestra una lista agrupada de opciones del proveedor. Muchas de ellas aparecen con nombres y valores de configuración extraños. Afortunadamente, para conectarse a cualquier base de datos empresarial, normalmente solo tendrá que proporcionar unos pocos datos. Así que puede ignorar los valores predeterminados de las demás opciones.

> [!NOTE]
> Las opciones de conexión de este proveedor de datos son las mismas sin importar que SQL Server sea el origen o el destino. Es decir, las opciones que ve son las mismas en las páginas **Elegir un origen de datos** y **Elegir un destino** del asistente.

|Información requerida|Propiedad de Proveedor de datos de .NET Framework para SQL Server|
|---|---|
|Authentication|**NotSpecified** predeterminado como "seguridad integrada" o seleccione otro modo de autenticación. No se admite la autenticación interactiva de Active Directory. |
|Nombre de servidor|**Data Source** (Origen de datos)|
|Información de autenticación (inicio de sesión)|**Seguridad integrada**; o bien **Id. de usuario** y **Contraseña**<br/>Si quiere ver una lista desplegable de las bases de datos en el servidor, primero debe proporcionar información de inicio de sesión válida.|
|Nombre de la base de datos|**Catálogo original**|

![Conectarse a SQL con el proveedor de .NET](../../integration-services/import-export-data/media/connect-to-sql-with-net-provider.jpg)

### <a name="options-to-specify-net-framework-data-provider-for-sql-server"></a>Opciones que deben especificarse (Proveedor de datos de .NET Framework para SQL Server)

> [!NOTE]
> Las opciones de conexión de este proveedor de datos son las mismas sin importar que SQL Server sea el origen o el destino. Es decir, las opciones que ve son las mismas en las páginas **Elegir un origen de datos** y **Elegir un destino** del asistente.

**Data Source** (Origen de datos)  
 Escriba el nombre o la dirección IP del servidor de origen o destino, o bien seleccione un servidor de la lista desplegable.  
 
 Para especificar un puerto TCP no estándar, escriba una coma después del nombre del servidor o la dirección IP y, a continuación, escriba el número de puerto.
 
 **Catálogo original**  
 Escriba el nombre de la base de datos de origen o destino, o bien seleccione una base de datos de la lista desplegable.  
  
 **Seguridad integrada**  
 Especifique **True** para establecer la conexión mediante la autenticación integrada de Windows (opción recomendada) o **False** para conectarse mediante la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si especifica **False**, debe especificar un Id. de usuario y una contraseña. El valor predeterminado es **False**.  
  
 **Id. de usuario**  
 Escriba un nombre de usuario si usa la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Contraseña**  
 Escriba la contraseña si usa la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

## <a name="connect-to-sql-server-with-the-odbc-driver-for-sql-server"></a>Conectarse a SQL Server con el controlador ODBC para SQL Server 
Los controladores ODBC no aparecen en la lista desplegable de los orígenes de datos. Para conectarse con un controlador ODBC, empiece seleccionando el **proveedor de datos de .NET Framework para ODBC** como origen de datos. Este proveedor actúa como un contenedor para el controlador ODBC.

> [!TIP]
> **Obtenga el controlador más reciente**. Descargue [Microsoft ODBC Driver 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53339).

Esta es la pantalla genérica que se ve inmediatamente después de seleccionar el proveedor de datos de .NET Framework para ODBC.

![Conectarse antes a SQL con ODBC](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-sql-server"></a>Opciones que hay que especificar (controlador ODBC para SQL Server)

> [!NOTE]
> Las opciones de conexión de este controlador ODBC son las mismas sin importar si SQL Server es el origen o el destino. Es decir, las opciones que ve son las mismas en las páginas **Elegir un origen de datos** y **Elegir un destino** del asistente.

Para conectarse a SQL Server con el controlador ODBC más reciente, ensamble una cadena de conexión que incluya las siguientes opciones y sus valores. El formato de una cadena de conexión completa aparece inmediatamente después de la lista de opciones.

> [!TIP]
> Obtenga ayuda para ensamblar una cadena de conexión que funcione correctamente. O bien, en lugar de proporcionar una cadena de conexión, puede proporcionar un DSN (nombre de origen de datos) existente o crear uno nuevo. Para obtener más información acerca de estas opciones, consulte [Conectarse a un origen de datos ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Controlador**  
Nombre del controlador ODBC. El nombre es diferente para las distintas versiones del controlador.

**Server**  
Nombre del servidor de SQL Server.

**Base de datos**  
El nombre de la base de datos.  

**Trusted_Connection**; o bien, **Uid** y **Pwd**  
Especifique **Trusted_Connection=Yes** para conectarse con la autenticación integrada de Windows; o bien, especifique **Uid** (id. de usuario) y **Pwd** (contraseña) para conectarse con la autenticación de SQL Server.

### <a name="connection-string-format"></a>Formato de la cadena de conexión
Este es el formato de una cadena de conexión que usa la autenticación integrada de Windows.

    `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;trusted_connection=Yes;`

Este es el formato de una cadena de conexión que usa la autenticación de SQL Server en lugar de la autenticación integrada de Windows.

     `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;uid=<user id>;pwd=<password>;`

### <a name="enter-the-connection-string"></a>Escribir la cadena de conexión
Escriba la cadena de conexión en el campo **ConnectionString** o escriba el nombre DSN en el campo **DSN**, que se encuentra en la página **Elegir un origen de datos** o **Elegir un destino**. Después de escribir la cadena de conexión, el asistente la analiza y muestra las propiedades individuales y sus valores en la lista.

En el siguiente ejemplo se emplea esta cadena de conexión.

    `Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;`

Esta es la pantalla que verá después de escribir la cadena de conexión.

![Conectarse antes a SQL con ODBC](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="connect-to-sql-server-with-the-microsoft-ole-db-provider-for-sql-server-or-sql-server-native-client"></a>Conectarse a SQL Server con el Proveedor OLE DB de Microsoft para SQL Server o SQL Server Native Client

> [!IMPORTANT]
> El Proveedor OLE DB de Microsoft para SQL Server y SQL Server Native Client no se admiten en versiones de SQL Server posteriores a SQL Server 2012. Use el controlador ODBC en su lugar. Para obtener más información sobre la transición al controlador ODBC, vea las entradas de blog siguientes.
>   -   [Microsoft se alinea con ODBC para el acceso a datos relacionales nativos](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)
>   -   [Presentación de los nuevos controladores Microsoft ODBC Driver for SQL Server](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/)

## <a name="other-data-providers-and-more-info"></a>Otros proveedores de datos y más información
Para obtener más información sobre cómo conectarse a SQL Server con un proveedor de datos que no aparezca en esta lista, consulte [SQL Server connection strings (Cadenas de conexión de SQL Server)](https://www.connectionstrings.com/sql-server/). En este sitio de terceros también encontrará más información sobre los proveedores de datos y los parámetros de conexión que se describen en esta página.

## <a name="see-also"></a>Consulte también
[Choose a Data Source](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md) (Selección de un origen de datos)  
[Choose a Destination](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md) (Selección de un destino)

