---
title: Objetos de origen de datos (OLE DB) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d8bb984c789f759eb764ad580f971ab71c9fc946
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297699"
---
# <a name="data-source-objects-ole-db"></a>Objetos de origen de datos (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client utiliza el término origen de datos para el conjunto de interfaces [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]OLE DB utilizadas para establecer un vínculo a un almacén de datos, como . Crear una instancia del objeto de origen de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del proveedor es la primera tarea de un consumidor de Native Client.  
  
 Todos los proveedores OLE DB declaran un identificador de clase (CLSID) para sí mismo. El CLSID [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el proveedor OLE DB de Native Client es el GUID de C/C+CLSID_SQLNCLI10 (el símbolo SQLNCLI_CLSID se resolverá en el progid correcto en el archivo sqlncli.h al que hace referencia). Con el CLSID, el consumidor usa la función de OLE **CoCreateInstance** para fabricar una instancia del objeto de origen de datos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client es un servidor en proceso. Las instancias de objetos de proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se crean mediante la macro CLSCTX_INPROC_SERVER para indicar el contexto ejecutable.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de origen de datos del proveedor OLE DB de Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] expone las interfaces de inicialización OLE DB que permiten al consumidor conectarse a bases de datos existentes.  
  
 Cada conexión realizada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través del proveedor OLE DB de Native Client establece estas opciones automáticamente:  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 En este ejemplo se utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la macro de identificador de clase para crear un objeto de origen de datos de proveedor OLE DB de Native Client y obtener una referencia a su interfaz **IDBInitialize.**  
  
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
  
 Con la creación correcta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de una instancia de un objeto de origen de datos de proveedor OLE DB de Native Client, la aplicación consumidora puede continuar inicializando el origen de datos y creando sesiones. Las sesiones OLE DB presentan las interfaces que permiten manipulación y acceso a datos.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client realiza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] su primera conexión a una instancia especificada como parte de una inicialización correcta del origen de datos. Se mantiene la conexión siempre que se mantenga una referencia en cualquier interfaz de inicialización de origen de datos, o hasta que se llame al método **IDBInitialize::Uninitialize**.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Propiedades del origen de datos &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [Propiedades de información de orígenes de datos](../../relational-databases/native-client-ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [Propiedades de inicialización y autorización](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [Sesiones](../../relational-databases/native-client-ole-db-data-source-objects/sessions.md)  
  
-   [Propiedades de la sesión: proveedor de SQL Server Native Client OLE DB](../../relational-databases/native-client-ole-db-data-source-objects/session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [Objetos de origen de datos persistentes](../../relational-databases/native-client-ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
