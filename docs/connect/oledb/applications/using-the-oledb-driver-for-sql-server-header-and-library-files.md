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
ms.openlocfilehash: 93b906a0604772fe224b1e63eaf6eed9eb8af983
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989235"
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>Uso del controlador OLE DB para los archivos de encabezado y biblioteca de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador de OLE DB para los archivos de encabezado y biblioteca de SQL Server se instalan cuando se selecciona la opción OLE DB driver for SQL Server SDK durante el proceso de instalación. Al desarrollar una aplicación, es importante copiar e instalar todos los archivos necesarios para el desarrollo en el entorno de desarrollo. Para obtener más información sobre la instalación y redistribución de OLE DB controlador para SQL Server, consulte [instalación de OLE DB driver para SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md).  
  
 El controlador de OLE DB para los archivos de encabezado y biblioteca de SQL Server se instala en la siguiente ubicación:  
  
 *% Archivos de programa%* \Microsoft SQL Server\Client SDK\OLEDB\182\SDK  
  
 El controlador de OLE DB para SQL Server archivo de encabezado (msoledbsql. h) se puede usar para agregar OLE DB controlador para la funcionalidad de acceso a datos de SQL Server a las aplicaciones personalizadas. El archivo de encabezado del controlador de OLE DB para SQL Server contiene todas las definiciones, atributos, propiedades e interfaces necesarios para aprovechar las nuevas características introducidas en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Además del controlador de OLE DB para SQL Server archivo de encabezado, también hay un archivo de biblioteca msoledbsql. lib, que es la biblioteca de exportación para la funcionalidad de [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) .  
  
 El archivo de encabezado del controlador de OLE DB para SQL Server es compatible con las versiones anteriores del archivo de encabezado sqloledb.h utilizados con Microsoft Data Access Components (MDAC), pero no contiene CLSID para SQLOLEDB (el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluido con MDAC) ni los símbolos de la funcionalidad XML (que el controlador de OLE DB para SQL Server no admite).    
  
 OLE DB las aplicaciones que usan el controlador de OLE DB para SQL Server solo necesitan hacer referencia a msoledbsql. h. Si una aplicación utiliza MDAC (SQLOLEDB) y el proveedor OLE DB del controlador de OLE DB para SQL Server, puede hacer referencia a sqloledb.h y a msoledbsql.h, pero la referencia a sqloledb.h debe aparecer en primer lugar.  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>Usar el controlador de OLE DB para SQL Server archivo de encabezado  
 Para usar el controlador de OLE DB para SQL Server archivo de encabezado, debe usar una instrucción **include** en el códigoC++ de C/Programming. En las secciones siguientes se describe cómo hacerlo en OLE DB aplicaciones.  
  
> [!NOTE]  
>  El controlador de OLE DB para los archivos de encabezado y biblioteca de SQL Server solo se puede C++ compilar con Visual Studio 2012 o posterior.  
  
### <a name="ole-db"></a>OLE DB  
 Para usar el controlador de OLE DB para SQL Server archivo de encabezado en una aplicación OLE DB, use las siguientes líneas de código de programación:  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  Si la aplicación tiene una instrucción **include** para SQLOLEDB. h, la instrucción **include** para msoledbsql. h debe aparecer después de ella.  
  
 Al crear una conexión a un origen de datos a través de OLE DB controlador para SQL Server, utilice "MSOLEDBSQL" como la cadena de nombre de proveedor.  

  
## <a name="component-names-and-properties-by-version"></a>Nombres de componente y propiedades por versión  

|Propiedad|Controlador OLE DB para SQL Server|MDAC|  
|--------|----------------------------|----|   
|PROGID de OLE DB|MSOLEDBSQL|SQLOLEDB|  
|Nombre de archivo de encabezado de OLE DB|msoledbsql.h|Sqloledb.h|  
|DLL del proveedor OLE DB|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>Vinculación estática y funciones BCP  
 Cuando una aplicación utiliza funciones BCP, es importante que la aplicación especifique en la cadena de conexión el controlador de la misma versión que se envió con el archivo de encabezados y la biblioteca utilizada para compilar la aplicación.  
  
 Para obtener más información, vea realizar [operaciones de copia masiva](../../oledb/features/performing-bulk-copy-operations.md).  
  
## <a name="see-also"></a>Consulte también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
