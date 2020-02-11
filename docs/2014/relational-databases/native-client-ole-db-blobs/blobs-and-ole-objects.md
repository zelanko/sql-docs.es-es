---
title: Blobs y objetos OLE | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- SQL Server Native Client OLE DB provider, BLOBs
- large data, OLE objects
ms.assetid: 767fa2f6-9cd2-436f-add5-e760bed29a58
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e459682da63bac8359fa8310233c234e456f4e5b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63195219"
---
# <a name="blobs-and-ole-objects"></a>BLOB y objetos OLE
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client expone la interfaz **ISequentialStream** para admitir el acceso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de consumidor a tipos de datos **ntext**, **Text**, **Image**, **VARCHAR (Max)**, **nvarchar (Max)**, **varbinary (Max)** y XML como objetos binarios grandes (BLOB). El método **Read** de **ISequentialStream** permite al consumidor recuperar muchos datos en fragmentos fáciles de administrar.  
  
 Para ver un ejemplo en el que se muestra esta característica, vea [set Large Data &#40;OLE DB&#41;](../native-client-ole-db-how-to/set-large-data-ole-db.md).  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client puede utilizar una interfaz **IStorage** implementada por el consumidor cuando el consumidor proporciona el puntero de interfaz en un descriptor de acceso enlazado para la modificación de datos.  
  
 En el caso de los tipos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos de valores grandes, el proveedor de OLE DB de Native Client comprueba las suposiciones de tamaño de tipo en las interfaces **IRowset** e DDL. Las columnas con tipos de datos **VARCHAR**, **nvarchar**y **varbinary** con un tamaño máximo establecido en Unlimited se representarán como ISLONG a través de los conjuntos de filas de esquema e interfaces que devuelven tipos de datos de columna.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client expone los tipos **VARCHAR (Max)**, **varbinary (Max)** y **nvarchar (max)** como DBTYPE_STR, DBTYPE_BYTES y DBTYPE_WSTR respectivamente.  
  
 Para trabajar con estos tipos, una aplicación tiene las siguientes opciones:  
  
-   Enlazar como el tipo (DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR). Si el búfer no es suficientemente grande, se producirá un truncamiento, exactamente igual que ocurría con estos tipos en las versiones anteriores (aunque ahora hay valores mayores).  
  
-   Enlazar como el tipo y también especificar DBTYPE_BYREF.  
  
-   Enlazar como DBTYPE_IUNKNOWN y usar la transmisión por secuencias.  
  
 Si se enlaza a DBTYPE_IUNKNOWN, se utiliza la funcionalidad de flujo de ISequentialStream. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client admite parámetros de salida de enlace como DBTYPE_IUNKNOWN para tipos de datos de valores grandes con el fin de facilitar escenarios en los que un procedimiento almacenado devuelve estos tipos de datos como valores devueltos que se expondrán como DBTYPE_IUNKNOWN al cliente.  
  
## <a name="storage-object-limitations"></a>Limitaciones de los objetos de almacenamiento  
  
-   El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client solo puede admitir un único objeto de almacenamiento abierto. Cuando se intenta abrir más de un objeto de almacenamiento (para obtener una referencia en más de un puntero de interfaz **ISequentialStream**), se recibe DBSTATUS_E_CANTCREATE.  
  
-   En el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client, se VARIANT_TRUE el valor predeterminado de la propiedad DBPROP_BLOCKINGSTORAGEOBJECTS de solo lectura. Esto indica que si un objeto de almacenamiento está activo, algunos métodos (salvo en los que están en los objetos de almacenamiento) sufrirán un error con E_UNEXPECTED.  
  
-   La longitud de los datos presentados por un objeto de almacenamiento implementado por el consumidor debe ser [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conocida por el proveedor de OLE DB de Native Client cuando se crea el descriptor de acceso de fila que hace referencia al objeto de almacenamiento. El consumidor debe enlazar un indicador de longitud de la estructura DBBINDING que se utiliza para la creación del descriptor de acceso.  
  
-   Si una fila contiene más de un valor de datos de gran tamaño y DBPROP_ACCESSORDER no es DBPROPVAL_AO_RANDOM, el consumidor debe usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un conjunto de filas compatible con cursores de proveedor de OLE DB de cliente nativo para recuperar los datos de fila o procesar todos los valores de datos grandes antes de recuperar otros valores de fila. Si DBPROP_ACCESSORDER es DBPROPVAL_AO_RANDOM, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client almacena en caché todos los tipos de datos XML como objetos binarios grandes (BLOB) para que se pueda tener acceso a ellos en cualquier orden.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Obtener datos grandes](getting-large-data.md)  
  
-   [Definir datos grandes](setting-large-data.md)  
  
-   [Compatibilidad con la transmisión por secuencias de parámetros de salida BLOB](streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)   
 [Usar tipos de valor grande](../native-client/features/using-large-value-types.md)  
  
  
