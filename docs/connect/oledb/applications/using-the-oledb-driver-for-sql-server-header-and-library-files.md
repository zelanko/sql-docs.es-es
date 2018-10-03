---
title: Uso del controlador OLE DB para los archivos de encabezado y biblioteca de SQL Server | Microsoft Docs
description: Uso del controlador OLE DB para los archivos de encabezado y biblioteca de SQL Server
ms.custom: ''
ms.date: 06/12/2018
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
manager: craigg
ms.openlocfilehash: 9cd6a50bec611b7068b3f79f3867f9e2a6242a70
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47816043"
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>Uso del controlador OLE DB para los archivos de encabezado y biblioteca de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server archivos de encabezado y biblioteca se instalan cuando se selecciona el controlador OLE DB para la opción de SDK de SQL Server durante el proceso de instalación. Al desarrollar una aplicación, es importante copiar e instalar todos los archivos necesarios para el desarrollo en el entorno de desarrollo. Para obtener más información sobre cómo instalar y redistribuir el controlador OLE DB para SQL Server, vea [instalar controlador de OLE DB para SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md).  
  
 El controlador OLE DB para SQL Server archivos de encabezado y biblioteca se instalan en la siguiente ubicación:  
  
 *% PROGRAM FILES %* \Microsoft SQL Server\Client SDK\OLEDB\181\SDK  
  
 El controlador OLE DB para el archivo de encabezado de SQL Server (msoledbsql.h) puede utilizarse para agregar el controlador de OLE DB para la funcionalidad de acceso de datos de SQL Server a las aplicaciones personalizadas. El archivo de encabezado del controlador de OLE DB para SQL Server contiene todas las definiciones, atributos, propiedades e interfaces necesarios para aprovechar las nuevas características introducidas en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Además del controlador OLE DB para el archivo de encabezado de SQL Server, también hay un archivo de biblioteca msoledbsql.lib que es la biblioteca de exportación para [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) funcionalidad.  
  
 El archivo de encabezado del controlador de OLE DB para SQL Server es compatible con las versiones anteriores del archivo de encabezado sqloledb.h utilizados con Microsoft Data Access Components (MDAC), pero no contiene CLSID para SQLOLEDB (el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluido con MDAC) ni los símbolos de la funcionalidad XML (que el controlador de OLE DB para SQL Server no admite).    
  
 Las aplicaciones OLE DB que utiliza el controlador OLE DB para SQL Server solo se necesitan hacer referencia a msoledbsql.h. Si una aplicación utiliza MDAC (SQLOLEDB) y el proveedor OLE DB del controlador de OLE DB para SQL Server, puede hacer referencia a sqloledb.h y a msoledbsql.h, pero la referencia a sqloledb.h debe aparecer en primer lugar.  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>Uso del controlador OLE DB para el archivo de encabezado SQL Server  
 Para usar el controlador OLE DB para el archivo de encabezado de SQL Server, debe usar un **incluyen** instrucción dentro de su código de programación de C o C++. Las secciones siguientes describen cómo realizar esta aplicaciones OLE DB.  
  
> [!NOTE]  
>  El controlador OLE DB para los archivos de encabezado y biblioteca de SQL Server sólo puede ser compilado con C++ de Visual Studio 2012 o posterior.  
  
### <a name="ole-db"></a>OLE DB  
 Para usar el controlador OLE DB para el archivo de encabezado de SQL Server en una aplicación OLE DB mediante las siguientes líneas de código de programación:  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  Si la aplicación tiene un **incluyen** instrucción para sqloledb.h, la **incluyen** instrucción para msoledbsql.h debe venir después de ella.  
  
 Al crear una conexión a un origen de datos mediante el controlador de OLE DB para SQL Server, use "MSOLEDBSQL" como la cadena de nombre de proveedor.  

  
## <a name="component-names-and-properties-by-version"></a>Nombres de componente y propiedades por versión  

|Propiedad|Controlador OLE DB para SQL Server|MDAC|  
|--------|----------------------------|----|   
|PROGID de OLE DB|MSOLEDBSQL|SQLOLEDB|  
|Nombre de archivo de encabezado de OLE DB|msoledbsql.h|Sqloledb.h|  
|DLL del proveedor OLE DB|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>Vinculación estática y funciones BCP  
 Cuando una aplicación utiliza funciones BCP, es importante que la aplicación especifique en la cadena de conexión el controlador de la misma versión que se envió con el archivo de encabezados y la biblioteca utilizada para compilar la aplicación.  
  
 Para obtener más información, vea realizar [realizar operaciones de copia masiva](../../oledb/features/performing-bulk-copy-operations.md).  
  
## <a name="see-also"></a>Ver también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
