---
title: Con el controlador OLE DB para SQL Server encabezado y archivos de biblioteca | Documentos de Microsoft
description: Utilizando el controlador OLE DB para los archivos de encabezado y biblioteca de SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: d958d4b1f12f5a109c5727832eb764fd2b497d70
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>Usar el controlador OLE DB para SQL Server encabezado y archivos de biblioteca
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para el encabezado de SQL Server y los archivos de biblioteca se instalan cuando se selecciona el controlador OLE DB para la opción de SDK de SQL Server durante el proceso de instalación. Al desarrollar una aplicación, es importante copiar e instalar todos los archivos necesarios para el desarrollo en el entorno de desarrollo. Para obtener más información sobre la instalación y redistribución de controlador de OLE DB para SQL Server, vea [instalar controlador OLE DB para SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md).  
  
 El controlador OLE DB para el encabezado de SQL Server y los archivos de biblioteca se instalan en la siguiente ubicación:  
  
 *% PROGRAM FILES %* \Microsoft SQL Server\Client SDK\OLEDB\180\SDK  
  
 El controlador OLE DB para el archivo de encabezado de SQL Server (msoledbsql.h) puede utilizarse para agregar el controlador OLE DB para la funcionalidad de acceso de datos de SQL Server a sus aplicaciones personalizadas. El controlador OLE DB para el archivo de encabezado de SQL Server contiene todas las definiciones, atributos, propiedades y interfaces necesarias para aprovechar las ventajas de las nuevas características introdujeron en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Además del controlador OLE DB para el archivo de encabezado de SQL Server, también hay un archivo de biblioteca de msoledbsql.lib que es la biblioteca de exportación para [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) funcionalidad.  
  
 El controlador OLE DB para el archivo de encabezado de SQL Server es compatible con el archivo de encabezado de sqloledb.h usado con Microsoft Data Access Components (MDAC), pero no contiene CLSID para SQLOLEDB (el proveedor OLE DB para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluido con MDAC) o de símbolos para Funcionalidad XML (lo que no es compatible con controlador de OLE DB para SQL Server).    
  
 Las aplicaciones de OLE DB que utiliza el controlador OLE DB para SQL Server sólo tiene que hacer referencia a msoledbsql.h. Si una aplicación utiliza MDAC (SQLOLEDB) y el controlador OLE DB para SQL Server, puede hacer referencia a sqloledb.h y msoledbsql.h, pero la referencia a sqloledb.h debe aparecer en primer lugar.  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>Usar el controlador OLE DB para el archivo de encabezado SQL Server  
 Para usar el controlador OLE DB para el archivo de encabezado de SQL Server, debe usar un **incluyen** instrucción en el código de programación de C o C++. Las secciones siguientes describen cómo hacer esto a las aplicaciones OLE DB.  
  
> [!NOTE]  
>  El controlador OLE DB para los archivos de encabezado y biblioteca de SQL Server sólo pueden compilar utilizando Visual Studio C++ 2012 o posterior.  
  
### <a name="ole-db"></a>OLE DB  
 Para usar el controlador OLE DB para el archivo de encabezado de SQL Server en una aplicación OLE DB, con las siguientes líneas de código de programación:  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  Si la aplicación tiene un **incluyen** instrucción para sqloledb.h, la **incluyen** instrucción para msoledbsql.h debe venir después de ella.  
  
 Al crear una conexión a un origen de datos mediante el controlador OLE DB para SQL Server, use "MSOLEDBSQL" como la cadena de nombre de proveedor.  

  
## <a name="component-names-and-properties-by-version"></a>Nombres de componente y propiedades por versión  

|Propiedad|Controlador OLE DB para SQL Server|MDAC|  
|--------|----------------------------|----|   
|PROGID de OLE DB|MSOLEDBSQL|SQLOLEDB|  
|Nombre de archivo de encabezado de OLE DB|msoledbsql.h|Sqloledb.h|  
|DLL del proveedor OLE DB|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>Vinculación estática y funciones BCP  
 Cuando una aplicación utiliza funciones BCP, es importante que la aplicación especifique en la cadena de conexión el controlador de la misma versión que se envió con el archivo de encabezados y la biblioteca utilizada para compilar la aplicación.  
  
 Para obtener más información, vea realizar [realizar operaciones de copia masiva](../../oledb/features/performing-bulk-copy-operations.md).  
  
## <a name="see-also"></a>Vea también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
