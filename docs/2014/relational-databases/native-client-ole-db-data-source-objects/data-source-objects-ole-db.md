---
title: Objetos (OLE DB) del origen de datos | Microsoft Docs
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
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48084303"
---
# <a name="data-source-objects-ole-db"></a>Objetos de origen de datos (OLE DB)
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
  
-   [Propiedades del origen de datos &#40;OLE DB&#41;](data-source-properties-ole-db.md)  
  
-   [Propiedades de información de origen de datos](data-source-information-properties.md)  
  
-   [Propiedades de inicialización y autorización](initialization-and-authorization-properties.md)  
  
-   [Sesiones](sessions.md)  
  
-   [Propiedades de sesión](session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [Objetos de origen de datos persistentes](persisted-data-source-objects.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
