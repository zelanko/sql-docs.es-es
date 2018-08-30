---
title: Objetos (OLE DB) del origen de datos | Microsoft Docs
description: Objetos de origen de datos (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 07fbc1d5c0a1001326e3cf114fbb6f0b756553a3
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43032008"
---
# <a name="data-source-objects-ole-db"></a>Objetos de origen de datos (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server usa el término origen de datos para el conjunto de interfaces OLE DB usado para establecer un vínculo a un almacén de datos, como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Crear una instancia del objeto de origen de datos del proveedor es la primera tarea de un controlador de OLE DB para el consumidor de SQL Server.  
  
 Todos los proveedores OLE DB declaran un identificador de clase (CLSID) para sí mismo. El CLSID para el controlador OLE DB para SQL Server es el CLSID_MSOLEDBSQL de GUID de C o C++ (el símbolo MSOLEDBSQL_CLSID se resuelve como el valor correcto progid en el archivo msoledbsql.h que se hace referencia). Con el CLSID, el consumidor usa la función de OLE **CoCreateInstance** para fabricar una instancia del objeto de origen de datos.  
  
 Controlador OLE DB para SQL Server es un servidor en proceso. Las instancias de objetos del controlador OLE DB para SQL Server se crean mediante la macro CLSCTX_INPROC_SERVER para indicar el contexto ejecutable.  
  
 El objeto de origen de datos del controlador OLE DB para SQL Server expone las interfaces de inicialización de OLE DB que permiten al consumidor conectarse a las bases de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] existentes.  
  
 Todas las conexiones realizadas a través del controlador OLE DB para SQL Server establece automáticamente estas opciones:  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 En este ejemplo se usa la macro de identificador de clase para crear un objeto de origen de datos del controlador OLE DB para SQL Server y obtener una referencia a su interfaz **IDBInitialize**.  
  
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
  
 Con la creación correcta de una instancia de un objeto de origen de datos del controlador OLE DB para SQL Server, la aplicación de consumidor puede continuar inicializando el origen de datos y creando sesiones. Las sesiones OLE DB presentan las interfaces que permiten manipulación y acceso a datos.  
  
 El controlador OLE DB para SQL Server realiza su primera conexión a una instancia especificada de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como parte de una inicialización correcta del origen de datos. Se mantiene la conexión siempre que se mantenga una referencia en cualquier interfaz de inicialización de origen de datos, o hasta que se llame al método **IDBInitialize::Uninitialize**.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Propiedades del origen de datos &#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [Propiedades de información de origen de datos](../../oledb/ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [Propiedades de inicialización y autorización](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [Sesiones](../../oledb/ole-db-data-source-objects/sessions.md)  
  
-   [Propiedades de sesión: controlador OLE DB para SQL Server](../../oledb/ole-db-data-source-objects/session-properties-oledb-driver-for-sql-server.md)  
  
-   [Objetos de origen de datos persistentes](../../oledb/ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>Ver también  
 [Programación del controlador OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
