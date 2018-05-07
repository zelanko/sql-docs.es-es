---
title: Origen de datos de objetos (OLE DB) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], data source objects
- SQL Server Native Client, data source objects
- SQLNCLI, data source objects
- SQL Server Native Client OLE DB provider, data source objects
- OLE DB data source objects [SQL Server Native Client]
- data source objects [OLE DB]
- CLSID
ms.assetid: c1d4ed20-ad3b-4e33-a26b-38d7517237b7
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2c6d8057f9a85491a2936a78140e0da69299969f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-objects-ole-db"></a>Objetos de origen de datos (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client usa el término origen de datos para el conjunto de interfaces de OLE DB que se utiliza para establecer un vínculo a un almacén de datos, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Crear una instancia del objeto de origen de datos del proveedor es la primera tarea de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor Native Client.  
  
 Todos los proveedores OLE DB declaran un identificador de clase (CLSID) para sí mismo. ¡El CLSID de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB es el GUID de C C/C ++ CLSID_SQLNCLI10 (el símbolo SQLNCLI_CLSID se resolverá como el valor correcto progid en el archivo sqlncli.h que se hace referencia). Con el CLSID, el consumidor utiliza OLE **CoCreateInstance** función para fabricar una instancia del objeto de origen de datos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client es un servidor en proceso. Instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos de proveedor de OLE DB de Native Client se crean con la macro CLSCTX_INPROC_SERVER para indicar el contexto ejecutable.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de origen de datos de proveedor OLE DB de Native Client expone las interfaces de inicialización de OLE DB que permiten al consumidor para conectarse a uno existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos.  
  
 Todas las conexiones realizadas a través de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client establece estas opciones automáticamente:  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 Este ejemplo utiliza la macro de identificador de clase para crear un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de origen de datos del proveedor OLE DB de Native Client y obtener una referencia a su **IDBInitialize** interfaz.  
  
```  
IDBInitialize*   pIDBInitialize;  
HRESULT          hr;  
  
hr = CoCreateInstance(CLSID_SQLNCLI10, NULL, CLSCTX_INPROC_SERVER,  
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
  
 Con la creación correcta de una instancia de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de origen de datos de proveedor OLE DB de Native Client, la aplicación de consumidor puede continuar Inicializando el origen de datos y crear sesiones. Las sesiones OLE DB presentan las interfaces que permiten manipulación y acceso a datos.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client realiza su primera conexión a una instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como parte de una inicialización de origen de datos se realice correctamente. La conexión se mantiene mientras se mantiene una referencia en cualquier interfaz de inicialización de origen de datos, o hasta que el **IDBInitialize:: UnInitialize** se llama al método.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Propiedades del origen de datos & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [Propiedades de información de origen de datos](../../relational-databases/native-client-ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [Propiedades de inicialización y autorización](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [Sesiones](../../relational-databases/native-client-ole-db-data-source-objects/sessions.md)  
  
-   [Propiedades de la sesión: proveedor de SQL Server Native Client OLE DB](../../relational-databases/native-client-ole-db-data-source-objects/session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [Objetos de origen de datos almacenados](../../relational-databases/native-client-ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
