---
title: BLOB y objetos OLE | Documentos de Microsoft
description: BLOB y objetos OLE
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-blobs
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- OLE DB Driver for SQL Server, BLOBs
- large data, OLE objects
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2b3e367533e8e3c4ad4fcedbc9c15d49ecd19518
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="blobs-and-ole-objects"></a>BLOB y objetos OLE
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador OLE DB para SQL Server expone la **ISequentialStream** interfaz para admitir el acceso del consumidor a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **ntext**, **texto**, **imagen** , **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, y los objetos como binarios grandes (BLOB) de tipos de datos xml. El **lectura** método **ISequentialStream** permite al consumidor recuperar muchos datos en fragmentos manejables.  
  
 Para obtener un ejemplo que muestra esta característica, consulte [establecer datos grandes & #40; OLE DB & #41;](../../oledb/ole-db-how-to/set-large-data-ole-db.md).  
  
 Puede usar el controlador OLE DB para SQL Server implementa consumidor **IStorage** interfaz cuando el consumidor proporciona el puntero de interfaz en un descriptor de acceso enlazado para la modificación de datos.  
  
 Para tipos de datos de valor grande, el controlador OLE DB para SQL Server comprueba las suposiciones de tamaño de tipo **IRowset** e interfaces DDL. Las columnas que tienen **varchar**, **nvarchar**, y **varbinary** tipos de datos y el tamaño máximo está establecido en ilimitado se representarán como ISLONG mediante los conjuntos de filas de esquema y mediante interfaces que devuelven tipos de datos de columna.  
  
 El controlador OLE DB para SQL Server expone la **varchar (max)**, **varbinary (max)** y **nvarchar (max)** tipos como DBTYPE_STR, DBTYPE_BYTES y DBTYPE_WSTR, respectivamente.  
  
 Para trabajar con estos tipos, una aplicación dispone de las opciones siguientes:  
  
-   Enlazar como el tipo (DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR). Si el búfer no es grande suficientemente se producirá un truncamiento, exactamente igual que en estos tipos en las versiones anteriores (aunque existen valores mayores).  
  
-   Enlazar como el tipo y también especificar DBTYPE_BYREF.  
  
-   Enlazar como DBTYPE_IUNKNOWN y usar la transmisión por secuencias.  
  
 Si se enlaza a DBTYPE_IUNKNOWN, se utiliza la funcionalidad de flujo de ISequentialStream. El controlador OLE DB para SQL Server es compatible con los parámetros de salida de enlace como DBTYPE_IUNKNOWN para tipos de datos de valor grande. Esto sirve para admitir escenarios donde un procedimiento almacenado devuelve estos tipos de datos como valores devueltos, que se devolverán como DBTYPE_IUNKNOWN al cliente.  
  
## <a name="storage-object-limitations"></a>Limitaciones de los objetos de almacenamiento  
  
-   El controlador OLE DB para SQL Server puede admitir solo un objeto único almacenamiento abierto. Intenta abrir más de un objeto de almacenamiento (para obtener una referencia en más de un **ISequentialStream** puntero de interfaz) devuelven DBSTATUS_E_CANTCREATE.  
  
-   En el controlador OLE DB para SQL Server, el valor predeterminado de la propiedad DBPROP_BLOCKINGSTORAGEOBJECTS de solo lectura es VARIANT_TRUE. Por lo tanto, si un objeto de almacenamiento está activo, algunos métodos (distintos de los métodos en los objetos de almacenamiento) se producirá un error con E_UNEXPECTED.  
  
-   La longitud de los datos presentados por un objeto de almacenamiento implementado por el consumidor debe realizarse conocida para el controlador OLE DB para SQL Server cuando se crea el descriptor de acceso de la fila que hace referencia al objeto de almacenamiento. El consumidor debe enlazar un indicador de longitud de la estructura DBBINDING que se utiliza para la creación del descriptor de acceso.  
  
-   Si una fila contiene más de un valor de datos grande y DBPROP_ACCESSORDER no es DBPROPVAL_AO_RANDOM, el consumidor debe usar un controlador OLE DB para el conjunto de filas compatible con cursores de SQL Server para recuperar datos de fila o procesar todos los valores de datos de gran tamaño antes de recuperar otros valores de fila. Si DBPROP_ACCESSORDER es DBPROPVAL_AO_RANDOM, el controlador OLE DB para SQL Server almacena en caché todos los tipos de datos xml como objetos binarios grandes (BLOB) para que son accesibles en cualquier orden.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Obtener datos de gran tamaño](../../oledb/ole-db-blobs/getting-large-data.md)  
  
-   [Establecer datos de gran tamaño](../../oledb/ole-db-blobs/setting-large-data.md)  
  
-   [Compatibilidad con transmisión por secuencias de parámetros de salida BLOB](../../oledb/ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para la programación de SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)        
 [Uso de tipos de valores grandes](../../oledb/features/using-large-value-types.md)  
  
  
