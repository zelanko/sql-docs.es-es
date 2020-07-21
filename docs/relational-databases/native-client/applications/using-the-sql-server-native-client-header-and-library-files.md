---
title: Archivos de encabezado y de biblioteca
description: Aprenda a usar los archivos de encabezado y biblioteca de SQL Server Native Client para desarrollar una aplicación. Copie los archivos necesarios en el entorno de desarrollo.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- header files [SQL Server Native Client]
- SQLNCLI, header files
- OLE DB, header files
- library files [SQL Server Native Client]
- SQL Server Native Client, header files
- data access [SQL Server Native Client], header files
- SQL Server Native Client ODBC driver,header files
- data access [SQL Server Native Client], library files
- SQL Server Native Client, library files
- ODBC applications, header files
- SQLNCLI, library files
ms.assetid: 69889a98-7740-4667-aecd-adfc0b37f6f0
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 53d67e4a6758ad4932c578e08afad0f58b1890d4
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86002357"
---
# <a name="using-the-sql-server-native-client-header-and-library-files"></a>Utilizar los archivos de encabezado y de biblioteca de SQL Server Native Client
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Los archivos de encabezado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y de biblioteca se instalan con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Al desarrollar una aplicación, es importante copiar e instalar todos los archivos necesarios para el desarrollo en el entorno de desarrollo. Para obtener más información acerca de cómo instalar y redistribuir [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, consulte [instalación de SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md).  
  
 Los archivos de encabezado y de biblioteca de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se instalan en la ubicación siguiente:  
  
 *% Archivos de programa%* \Microsoft SQL Server\110\SDK  
  
 El archivo de encabezado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (sqlncli.h) se puede utilizar para agregar la funcionalidad de acceso a datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a las aplicaciones personalizadas. El archivo de encabezado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client contiene todas las definiciones, atributos, propiedades e interfaces necesarios para aprovechar las nuevas características introducidas en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Además del archivo de encabezado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, hay también un archivo de biblioteca  sqlncli11.lib que es la biblioteca de exportación para la funcionalidad de Programa de copia masiva (BCP) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para ODBC.  
  
 El archivo de encabezado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client es compatible con las versiones anteriores de los archivos de encabezado odbcss.h y sqloledb.h utilizados con Microsoft Data Access Components (MDAC), pero no contiene CLSID para SQLOLEDB (el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluido con MDAC) ni los símbolos de la funcionalidad XML (que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no admite).  
  
 Las aplicaciones ODBC no pueden hacer referencia al encabezado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (sqlncli.h) y odbcss.h en el mismo programa. Aun cuando no utilice ninguna de las características introducidas en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], el archivo de encabezado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client funcionará en lugar del odbcss.h anterior.  
  
 Las aplicaciones OLE DB que usan el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client solamente tienen que hacer referencia a sqlncli.h. Si una aplicación utiliza MDAC (SQLOLEDB) y el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, puede hacer referencia a sqloledb.h y a sqlncli.h, pero la referencia a sqloledb.h debe aparecer en primer lugar.  
  
## <a name="using-the-sql-server-native-client-header-file"></a>Usar el archivo de encabezado de SQL Server Native Client  
 Para usar el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] archivo de encabezado de Native Client, debe usar una instrucción **include** en el código de programación de C/C++. En las secciones siguientes se describe cómo hacer esto para las aplicaciones OLE DB y ODBC.  
  
> [!NOTE]  
>  Los archivos de encabezado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y de biblioteca solo se pueden compilar utilizando Visual Studio C++ 2002 o posterior.  
  
### <a name="ole-db"></a>OLE DB  
 Para utilizar el archivo de encabezado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client en una aplicación OLE DB, utilizando las líneas siguientes de código de programación:  
  
```  
#define _SQLNCLI_OLEDB_  
include "sqlncli.h";  
```  
  
> [!NOTE]  
>  Se debe omitir la primera línea de código mostrada anterior si la aplicación utiliza las API de ODBC y de OLE DB. Además, si la aplicación tiene una instrucción **include** para SQLOLEDB. h, la instrucción **include** de SQLNCLI. h debe aparecer después de ella.  
  
 Al crear una conexión a un origen de datos mediante [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, utilice "SQLNCLI11" como la cadena de nombre de proveedor.  
  
### <a name="odbc"></a>ODBC  
 Para utilizar el archivo de encabezado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client en una aplicación ODBC, utilizando las líneas siguientes de código de programación:  
  
```  
#define _SQLNCLI_ODBC_  
include "sqlncli.h";  
```  
  
> [!NOTE]  
>  La primera línea de código mostrada anteriormente se debe omitir si la aplicación usa tanto OLE DB como las API de ODBC. Además, si la aplicación tiene una instrucción `#include` para odbcss.h, se debe quitar.  
  
 Al crear una conexión a un origen de datos mediante [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, utilice "SQL Server Native Client 11.0" como la cadena de nombre de controlador.  
  
## <a name="component-names-and-properties-by-version"></a>Nombres de componente y propiedades por versión  
  
|Propiedad|SQL Server Native Client<br /><br /> SQL Server 2005|SQL Server Native Client 10.0<br /><br /> SQL Server 2008|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]|MDAC|  
|--------------|--------------------------------------------------|-------------------------------------------------------|---------------------------------------------------------------|----------|  
|Nombre de controlador ODBC|SQL Native Client|SQL Server Native Client 10.0|SQL Server Native Client 11.0|SQL Server|  
|Nombre de archivo de encabezado de ODBC|Sqlncli.h|Sqlncli.h|Sqlncli.h|Odbcss.h|  
|DLL del controlador ODBC|Sqlncli.dll|Sqlncl10.dll|Sqlncl11.dll|sqlsrv32.dll|  
|Archivo .lib de ODBC para las API de BCP|Sqlncli.lib|Sqlncli10.lib|Sqlncli11.lib|Odbcbcp.lib|  
|DLL de ODBC para las API de BCP|Sqlncli.dll|Sqlncli10.dll|Sqlncli11.dll|Odbcbcp.dll|  
|PROGID de OLE DB|SQLNCLI|SQLNCLI10|SQLNCLI11|SQLOLEDB|  
|Nombre de archivo de encabezado de OLE DB|Sqlncli.h|Sqlncli.h|Sqlncli.h|Sqloledb.h|  
|DLL del proveedor OLE DB|Sqlncli.dll|Sqlncli10.dll|Sqlncli11.dll|Sqloledb.dll|  
  
 sqlncli.h admite varias versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a través de la macro SQLNCLI_VER. De forma predeterminada, SQLNCLI_VER tiene como valor predeterminado la última versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Para generar una aplicación que utiliza sqlncli10.dll en lugar de sqlncli11.dll, establezca SQLNCLI_VER en 10.  
  
## <a name="static-linking-and-bcp-functions"></a>Vinculación estática y funciones BCP  
 Cuando una aplicación utiliza funciones BCP, es importante que la aplicación especifique en la cadena de conexión el controlador de la misma versión que se envió con el archivo de encabezados y la biblioteca utilizada para compilar la aplicación.  
  
 Por ejemplo, si compila una aplicación con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, el archivo de biblioteca asociado (sqlncli11.lib) y el archivo de encabezados (sqlncli.h) que están en \Archivos de programa\Microsoft SQL Server\110\SDK, asegúrese de especificar (utilizando ODBC como ejemplo) “DRIVER={SQL Server Native Client 10.1}” en la cadena de conexión.  
  
 Para más información, consulte [Realización de operaciones de copia masiva](../../../relational-databases/native-client/features/performing-bulk-copy-operations.md).  
  
## <a name="see-also"></a>Consulte también  
 [Generar aplicaciones con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
