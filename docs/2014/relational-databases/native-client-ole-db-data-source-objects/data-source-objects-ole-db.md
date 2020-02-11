---
title: Objetos de origen de datos (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 6b602695720e0d6567e44e4fbe8fd06b6d496a6e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63130596"
---
# <a name="data-source-objects-ole-db"></a>Objetos de origen de datos (OLE DB)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client usa el término origen de datos para el conjunto de interfaces OLE DB utilizadas para establecer un vínculo a un almacén de datos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]como. Crear una instancia del objeto de origen de datos del proveedor es la primera tarea de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor de Native Client.  
  
 Todos los proveedores OLE DB declaran un identificador de clase (CLSID) para sí mismo. El CLSID del proveedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de OLE DB de Native Client es el GUID de C/C++ CLSID_SQLNCLI10 (el símbolo SQLNCLI_CLSID se resolverá en el ProgID correcto del archivo SQLNCLI. h al que haga referencia). Con el CLSID, el consumidor usa la función de OLE **CoCreateInstance** para fabricar una instancia del objeto de origen de datos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client es un servidor en proceso. Las instancias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de objetos de proveedor de OLE DB de Native Client se crean mediante la macro CLSCTX_INPROC_SERVER para indicar el contexto ejecutable.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de origen de datos del proveedor de OLE DB de Native Client expone las interfaces de inicialización OLE DB que permiten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al consumidor conectarse a las bases de datos existentes.  
  
 Cada conexión realizada a través [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del proveedor de OLE DB de Native Client establece estas opciones automáticamente:  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 En este ejemplo se usa la macro de identificador de clase [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para crear un objeto de origen de datos del proveedor de OLE DB de cliente nativo y obtener una referencia a su interfaz **IDBInitialize** .  
  
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
  
 Al crear correctamente una instancia de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de origen de datos del proveedor de OLE DB de Native Client, la aplicación de consumidor puede continuar inicializando el origen de datos y creando sesiones. Las sesiones OLE DB presentan las interfaces que permiten manipulación y acceso a datos.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client realiza su primera conexión a una instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada de como parte de una inicialización de origen de datos correcta. Se mantiene la conexión siempre que se mantenga una referencia en cualquier interfaz de inicialización de origen de datos, o hasta que se llame al método **IDBInitialize::Uninitialize**.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Propiedades de origen de datos &#40;OLE DB&#41;](data-source-properties-ole-db.md)  
  
-   [Propiedades de información de orígenes de datos](data-source-information-properties.md)  
  
-   [Propiedades de inicialización y autorización](initialization-and-authorization-properties.md)  
  
-   [Sesiones](sessions.md)  
  
-   [Propiedades de sesión](session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [Objetos de origen de datos persistentes](persisted-data-source-objects.md)  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
