---
title: Uso del controlador OLE DB para los archivos de encabezado y biblioteca de SQL Server | Microsoft Docs
description: Uso del controlador OLE DB para los archivos de encabezado y biblioteca de SQL Server
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- header files [OLE DB Driver for SQL Server]
- MSOLEDBSQL, header files
- OLE DB, header files
- library files [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, header files
- data access [OLE DB Driver for SQL Server], header files
- data access [OLE DB Driver for SQL Server], library files
- OLE DB Driver for SQL Server, library files
- MSOLEDBSQL, library files
author: pmasl
ms.author: pelopes
ms.openlocfilehash: ecb2b323a9acb84c2c7a53b28653e81ef65ea23b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86006990"
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>Uso del controlador OLE DB para los archivos de encabezado y biblioteca de SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Los archivos de encabezado y biblioteca de OLE DB Driver for SQL Server se instalan cuando se selecciona la opción del SDK de OLE DB Driver for SQL Server durante el proceso de instalación. Al desarrollar una aplicación, es importante copiar e instalar todos los archivos necesarios para el desarrollo en el entorno de desarrollo. Para más información acerca de la instalación y redistribución de OLE DB Driver for SQL Server, consulte [Instalación del controlador OLE DB Driver for SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md).  
  
 Los archivos de encabezado y de biblioteca de OLE DB Driver for SQL Server se instalan en la ubicación siguiente:  
  
 *%PROGRAM FILES%* \Microsoft SQL Server\Client SDK\OLEDB\182\SDK  
  
 El archivo de encabezado de OLE DB Driver for SQL Server (msoledbsql.h) se puede usar para agregar la funcionalidad de acceso a datos de OLE DB Driver for SQL Server a las aplicaciones personalizadas. El archivo de encabezado del controlador de OLE DB para SQL Server contiene todas las definiciones, atributos, propiedades e interfaces necesarios para aprovechar las nuevas características introducidas en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Además del archivo de encabezado de OLE DB Driver for SQL Server, también hay un archivo de biblioteca msoledbsql.lib, que es la biblioteca de exportación para la funcionalidad [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md).  
  
 El archivo de encabezado del controlador de OLE DB para SQL Server es compatible con las versiones anteriores del archivo de encabezado sqloledb.h utilizados con Microsoft Data Access Components (MDAC), pero no contiene CLSID para SQLOLEDB (el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluido con MDAC) ni los símbolos de la funcionalidad XML (que el controlador de OLE DB para SQL Server no admite).    
  
 Las aplicaciones OLE DB que usan OLE DB Driver for SQL Server solo necesitan hacer referencia a msoledbsql.h. Si una aplicación utiliza MDAC (SQLOLEDB) y el proveedor OLE DB del controlador de OLE DB para SQL Server, puede hacer referencia a sqloledb.h y a msoledbsql.h, pero la referencia a sqloledb.h debe aparecer en primer lugar.  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>Uso del archivo de encabezado de OLE DB Driver for SQL Server  
 Para usar el archivo de encabezado de OLE DB Driver for SQL Server, debe utilizar una instrucción **include** en el código de programación en C/C++. En las secciones siguientes se describe cómo solucionar problemas de aplicaciones de OLE DB.  
  
> [!NOTE]  
>  Los archivos de encabezado y de biblioteca de OLE DB Driver for SQL Server solo se pueden compilar utilizando Visual Studio C++ 2012 o posterior.  
  
### <a name="ole-db"></a>OLE DB  
 Para utilizar el archivo de encabezado de OLE DB Driver for SQL Server en una aplicación OLE DB, con las líneas siguientes de código de programación:  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  Si la aplicación tiene una instrucción **include** para sqloledb.h, la instrucción **include** para sqlncli.h debe venir detrás de esta.  
  
 Al crear una conexión a un origen de datos mediante OLE DB Driver for SQL Server, utilice "MSOLEDBSQL" como la cadena de nombre de proveedor.  

  
## <a name="component-names-and-properties-by-version"></a>Nombres de componente y propiedades por versión  

|Propiedad|Controlador OLE DB para SQL Server|MDAC|  
|--------|----------------------------|----|   
|PROGID de OLE DB|MSOLEDBSQL|SQLOLEDB|  
|Nombre de archivo de encabezado de OLE DB|msoledbsql.h|Sqloledb.h|  
|DLL del proveedor OLE DB|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>Vinculación estática y funciones BCP  
 Cuando una aplicación utiliza funciones BCP, es importante que la aplicación especifique en la cadena de conexión el controlador de la misma versión que se envió con el archivo de encabezados y la biblioteca utilizada para compilar la aplicación.  
  
 Para más información, consulte [Realización de operaciones de copia masiva](../../oledb/features/performing-bulk-copy-operations.md).  
  
## <a name="see-also"></a>Consulte también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
