---
title: Objetos (OLE DB) del origen de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3b5d65c5df2d1ebc1e2b0435e02bd9668f3feb18
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47627173"
---
# <a name="data-source-objects-ole-db"></a>Objetos de origen de datos (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client usa el término origen de datos para el conjunto de interfaces OLE DB usado para establecer un vínculo a un almacén de datos, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Crear una instancia del objeto de origen de datos del proveedor es la primera tarea de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor Native Client.  
  
 Todos los proveedores OLE DB declaran un identificador de clase (CLSID) para sí mismo. El CLSID para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB es la CLSID_SQLNCLI10 de GUID de C o C++ (el símbolo SQLNCLI_CLSID se resolverá en el valor correcto progid en el archivo sqlncli.h al que se hace referencia). Con el CLSID, el consumidor usa la función de OLE **CoCreateInstance** para fabricar una instancia del objeto de origen de datos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client es un servidor en proceso. Las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos del proveedor OLE DB de Native Client se crean mediante la macro CLSCTX_INPROC_SERVER para indicar el contexto ejecutable.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de origen de datos de proveedor OLE DB de Native Client expone las interfaces de inicialización de OLE DB que permiten al consumidor para conectarse a uno existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos.  
  
 Todas las conexiones realizadas a través de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client establece estas opciones automáticamente:  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 Este ejemplo usa la macro del identificador de clase para crear un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de origen de datos del proveedor OLE DB de Native Client y obtener una referencia a su **IDBInitialize** interfaz.  
  
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
  
 Con la creación correcta de una instancia de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de origen de datos del proveedor OLE DB de Native Client, la aplicación de consumidor puede continuar Inicializando el origen de datos y creando sesiones. Las sesiones OLE DB presentan las interfaces que permiten manipulación y acceso a datos.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client realiza su primera conexión a una instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como parte de una inicialización de origen de datos correcta. Se mantiene la conexión siempre que se mantenga una referencia en cualquier interfaz de inicialización de origen de datos, o hasta que se llame al método **IDBInitialize::Uninitialize**.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Propiedades del origen de datos &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [Propiedades de información de origen de datos](../../relational-databases/native-client-ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [Propiedades de inicialización y autorización](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [Sesiones](../../relational-databases/native-client-ole-db-data-source-objects/sessions.md)  
  
-   [Propiedades de la sesión: proveedor de SQL Server Native Client OLE DB](../../relational-databases/native-client-ole-db-data-source-objects/session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [Objetos de origen de datos persistentes](../../relational-databases/native-client-ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
