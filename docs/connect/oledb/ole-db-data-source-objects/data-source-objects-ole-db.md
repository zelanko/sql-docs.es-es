---
title: Origen de datos de objetos (OLE DB) | Documentos de Microsoft
description: Objetos de origen de datos (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], data source objects
- OLE DB Driver for SQL Server, data source objects
- MSOLEDBSQL, data source objects
- OLE DB Driver for SQL Server, data source objects
- OLE DB data source objects [OLE DB Driver for SQL Server]
- data source objects [OLE DB]
- CLSID
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 05e9653ad107d31042ff75416e85754129709fff
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-objects-ole-db"></a>Objetos de origen de datos (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Controlador de OLE DB para SQL Server utiliza el término origen de datos para el conjunto de interfaces de OLE DB que se utiliza para establecer un vínculo a un almacén de datos, como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Crear una instancia del objeto de origen de datos del proveedor es la primera tarea de un controlador de OLE DB para el consumidor de SQL Server.  
  
 Todos los proveedores OLE DB declaran un identificador de clase (CLSID) para sí mismo. El CLSID para el controlador OLE DB para SQL Server es el CLSID_MSOLEDBSQL de GUID de C o C++ (el símbolo MSOLEDBSQL_CLSID se resolverá como el valor correcto progid en el archivo msoledbsql.h que se hace referencia). Con el CLSID, el consumidor utiliza OLE **CoCreateInstance** función para fabricar una instancia del objeto de origen de datos.  
  
 Controlador de OLE DB para SQL Server es un servidor en proceso. Se crean instancias de controlador de OLE DB para los objetos de SQL Server mediante la macro CLSCTX_INPROC_SERVER para indicar el contexto ejecutable.  
  
 El controlador OLE DB para el objeto de origen de datos de SQL Server expone las interfaces de inicialización de OLE DB que permiten al consumidor para conectarse a uno existente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bases de datos.  
  
 Todas las conexiones realizadas a través del controlador de OLE DB para SQL Server establece automáticamente estas opciones:  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 Este ejemplo utiliza la macro de identificador de clase para crear un controlador de OLE DB para el objeto de origen de datos de SQL Server y obtención una referencia a su **IDBInitialize** interfaz.  
  
```  
IDBInitialize*   pIDBInitialize;  
HRESULT          hr;  
  
hr = CoCreateInstance(CLSID_MSOLEDBSQL, NULL, CLSCTX_INPROC_SERVER,  
    IID_IDBInitialize, (void**) &pIDBInitialize);  
  
if (SUCCEEDED(hr))  
{  
    //  Perform necessary processing with the interface.  
    pIDBInitialize->Uninitialize();  
    pIDBInitialize->Release();  
}  
else  
{  
    // Display error from CoCreateInstance.  
}  
```  
  
 Con la creación correcta de una instancia de un controlador de OLE DB para el objeto de origen de datos de SQL Server, la aplicación de consumidor puede continuar Inicializando el origen de datos y crear sesiones. Las sesiones OLE DB presentan las interfaces que permiten manipulación y acceso a datos.  
  
 El controlador OLE DB para SQL Server realiza su primera conexión a una instancia especificada de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como parte de una inicialización de origen de datos se realice correctamente. La conexión se mantiene mientras se mantiene una referencia en cualquier interfaz de inicialización de origen de datos, o hasta que el **IDBInitialize:: UnInitialize** se llama al método.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Propiedades del origen de datos & #40; OLE DB & #41;](../../oledb/ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [Propiedades de información de origen de datos](../../oledb/ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [Propiedades de inicialización y autorización](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [Sesiones](../../oledb/ole-db-data-source-objects/sessions.md)  
  
-   [Propiedades de sesión: controlador OLE DB para SQL Server](../../oledb/ole-db-data-source-objects/session-properties-oledb-driver-for-sql-server.md)  
  
-   [Objetos de origen de datos almacenados](../../oledb/ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>Vea también  
 [Programación del controlador OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
