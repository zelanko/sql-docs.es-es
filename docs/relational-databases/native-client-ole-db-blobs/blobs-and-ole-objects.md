---
title: BLOB y objetos OLE | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 88f363cc2e9e4d420f8edf80603b9a05a2417661
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43060801"
---
# <a name="blobs-and-ole-objects"></a>BLOB y objetos OLE
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone la **ISequentialStream** interfaz para admitir el acceso del consumidor a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ntext**, **texto**, **imagen**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, y los tipos de datos xml como objetos binarios grandes (BLOB ). El método **Read** de **ISequentialStream** permite al consumidor recuperar muchos datos en fragmentos fáciles de administrar.  
  
 Para obtener un ejemplo que muestra esta característica, consulte [del conjunto de datos grandes &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/set-large-data-ole-db.md).  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client puede utilizar un consumidor implementa **IStorage** interfaz cuando el consumidor proporciona el puntero de interfaz en un descriptor de acceso enlazado para la modificación de datos.  
  
 Para tipos de datos de valor grande, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client comprueba las suposiciones de tamaño de tipo **IRowset** e interfaces DDL. Las columnas con **varchar**, **nvarchar**, y **varbinary** tipos de datos con el tamaño máximo está establecido en ilimitado se representarán como ISLONG a través de los conjuntos de filas de esquema e interfaces devolver tipos de datos de columna.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone la **varchar (max)**, **varbinary (max)** y **nvarchar (max)** tipos como DBTYPE_STR, DBTYPE_BYTES y DBTYPE_ WSTR, respectivamente.  
  
 Para trabajar con estos tipos de una aplicación tiene las siguientes opciones:  
  
-   Enlazar como el tipo (DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR). Si el búfer no es suficientemente grande, se producirá un truncamiento, exactamente igual que ocurría con estos tipos en las versiones anteriores (aunque ahora hay valores mayores).  
  
-   Enlazar como el tipo y también especificar DBTYPE_BYREF.  
  
-   Enlazar como DBTYPE_IUNKNOWN y usar la transmisión por secuencias.  
  
 Si se enlaza a DBTYPE_IUNKNOWN, se utiliza la funcionalidad de flujo de ISequentialStream. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client admite parámetros de salida de enlace como DBTYPE_IUNKNOWN para tipos de datos de valor grande facilitar escenarios donde un procedimiento almacenado devuelve estos datos tipos como valores devueltos que serán expuestos como DBTYPE_IUNKNOWN en el cliente.  
  
## <a name="storage-object-limitations"></a>Limitaciones de los objetos de almacenamiento  
  
-   El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB puede admitir solo un objeto único almacenamiento abierto. Cuando se intenta abrir más de un objeto de almacenamiento (para obtener una referencia en más de un puntero de interfaz **ISequentialStream**), se recibe DBSTATUS_E_CANTCREATE.  
  
-   En el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client, el valor predeterminado de la propiedad DBPROP_BLOCKINGSTORAGEOBJECTS de solo lectura es VARIANT_TRUE. Esto indica que si un objeto de almacenamiento está activo, algunos métodos (salvo en los que están en los objetos de almacenamiento) sufrirán un error con E_UNEXPECTED.  
  
-   La longitud de los datos presentados por un objeto de almacenamiento implementado por el consumidor debe dar a conocer a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client cuando se crea el descriptor de acceso de la fila que hace referencia al objeto de almacenamiento. El consumidor debe enlazar un indicador de longitud de la estructura DBBINDING que se utiliza para la creación del descriptor de acceso.  
  
-   Si una fila contiene más de un valor de datos grande y DBPROP_ACCESSORDER no es DBPROPVAL_AO_RANDOM, el consumidor debe utilizar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjunto de filas OLE DB de Native Client proveedor compatible con cursores para recuperar datos de fila o procesar datos de gran tamaño de todos los valores antes de recuperar otros valores de fila. Si DBPROP_ACCESSORDER es DBPROPVAL_AO_RANDOM, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client almacena en caché todos los tipos de datos xml como objetos binarios grandes (BLOB) para que se puede acceder en cualquier orden.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Obtener datos grandes](../../relational-databases/native-client-ole-db-blobs/getting-large-data.md)  
  
-   [Definir datos grandes](../../relational-databases/native-client-ole-db-blobs/setting-large-data.md)  
  
-   [Compatibilidad con la transmisión por secuencias de parámetros de salida BLOB](../../relational-databases/native-client-ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [Usar tipos de valor grande](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  
