---
title: Origen de datos de objetos (OLE DB) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
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
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9f89825aaca32b542a6788fc9ef849975695f275
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196910"
---
# <a name="data-source-objects-ole-db"></a>Objetos de origen de datos (OLE DB)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client usa el término origen de datos para el conjunto de interfaces de OLE DB que se utiliza para establecer un vínculo a un almacén de datos, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Crear una instancia del objeto de origen de datos del proveedor es la primera tarea de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor Native Client.  
  
 Todos los proveedores OLE DB declaran un identificador de clase (CLSID) para sí mismo. ¡El CLSID de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB es el GUID de C C/C ++ CLSID_SQLNCLI10 (el símbolo SQLNCLI_CLSID se resolverá como el valor correcto progid en el archivo sqlncli.h que se hace referencia). Con el CLSID, el consumidor utiliza OLE **CoCreateInstance** función para fabricar una instancia del objeto de origen de datos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client es un servidor en proceso. Instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos de proveedor de OLE DB de Native Client se crean con la macro CLSCTX_INPROC_SERVER para indicar el contexto ejecutable.  
  
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
  
-   [Propiedades del origen de datos &#40;OLE DB&#41;](data-source-properties-ole-db.md)  
  
-   [Propiedades de información de origen de datos](data-source-information-properties.md)  
  
-   [Propiedades de inicialización y autorización](initialization-and-authorization-properties.md)  
  
-   [Sesiones](sessions.md)  
  
-   [Propiedades de la sesión](session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [Objetos de origen de datos persistentes](persisted-data-source-objects.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  