---
title: BLOB y objetos OLE | Microsoft Docs
description: BLOB y objetos OLE
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- OLE DB Driver for SQL Server, BLOBs
- large data, OLE objects
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 70d3ffccfc9613434b09335944e445a2705b95c3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67988673"
---
# <a name="blobs-and-ole-objects"></a>BLOB y objetos OLE
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server expone la interfaz **ISequentialStream** para admitir el acceso del consumidor a tipos de datos xml y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ntext **,** text **,** image **,** varchar(max) **,** nvarchar(max)**y**varbinary(max)**de** como objetos binarios grandes (BLOB). El método **Read** de **ISequentialStream** permite al consumidor recuperar muchos datos en fragmentos fáciles de administrar.  
  
 Para obtener un ejemplo que muestra esta característica, consulte [Establecimiento de datos grandes &#40;OLE DB&#41;](../../oledb/ole-db-how-to/set-large-data-ole-db.md).  
  
 El controlador OLE DB para SQL Server puede usar una interfaz **IStorage** implementada por el consumidor cuando este proporciona el puntero de interfaz en un descriptor de acceso enlazado para la modificación de datos.  
  
 Para los tipos de datos de valor grande, el controlador OLE DB para SQL Server comprueba las suposiciones de tamaño de los tipos en las interfaces **IRowset** y DDL. Las columnas que tienen tipos de datos **varchar**, **nvarchar** y **varbinary**, y cuyo tamaño máximo está establecido en ilimitado, se representarán como ISLONG en los conjuntos de filas de esquema y las interfaces que devuelven tipos de datos de columna.  
  
 El controlador OLE DB para SQL Server expone los tipos **varchar(max)** , **varbinary(max)** y **nvarchar(max)** como DBTYPE_STR, DBTYPE_BYTES y DBTYPE_WSTR, respectivamente.  
  
 Para trabajar con estos tipos, una aplicación dispone de las opciones siguientes:  
  
-   Enlazar como el tipo (DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR). Si el búfer no es lo suficientemente grande, se producirá un truncamiento, exactamente igual que ocurría con estos tipos en las versiones anteriores (aunque ahora hay valores mayores disponibles).  
  
-   Enlazar como el tipo y también especificar DBTYPE_BYREF.  
  
-   Enlazar como DBTYPE_IUNKNOWN y usar la transmisión por secuencias.  
  
 Si se enlaza a DBTYPE_IUNKNOWN, se utiliza la funcionalidad de flujo de ISequentialStream. OLE DB Driver for SQL Server admite parámetros de salida de enlace como DBTYPE_IUNKNOWN para tipos de datos de valores grandes. Esto es para admitir escenarios en los que un procedimiento almacenado devuelve estos tipos de datos como valores devueltos, que se devolverán como DBTYPE_IUNKNOWN al cliente.  
  
## <a name="storage-object-limitations"></a>Limitaciones de los objetos de almacenamiento  
  
-   OLE DB Driver for SQL Server solamente puede admitir un único objeto de almacenamiento abierto. Cuando se intenta abrir más de un objeto de almacenamiento (para obtener una referencia en más de un puntero de interfaz **ISequentialStream**), se recibe DBSTATUS_E_CANTCREATE.  
  
-   En el controlador OLE DB para SQL Server, el valor predeterminado de la propiedad DBPROP_BLOCKINGSTORAGEOBJECTS de solo lectura es VARIANT_TRUE. Por tanto, si un objeto de almacenamiento está activo, algunos métodos (salvo aquellos que están en los objetos de almacenamiento) obtendrán un error con E_UNEXPECTED.  
  
-   Se debe dar a conocer al controlador OLE DB para SQL Server la longitud de los datos presentados por un objeto de almacenamiento implementado por el consumidor cuando se crea el descriptor de acceso a filas que hace referencia al objeto de almacenamiento. El consumidor debe enlazar un indicador de longitud de la estructura DBBINDING que se utiliza para la creación del descriptor de acceso.  
  
-   Si una fila contiene más de un valor de datos grande y DBPROP_ACCESSORDER no es DBPROPVAL_AO_RANDOM, el consumidor debe usar un conjunto de filas compatible con cursores del controlador OLE DB para SQL Server a fin de recuperar datos de filas o procesar todos los valores de datos grandes antes de recuperar otros valores de fila. Si DBPROP_ACCESSORDER es DBPROPVAL_AO_RANDOM, el controlador OLE DB para SQL Server almacena en caché todos los tipos de datos xml como objetos binarios grandes (BLOB) para que se pueda tener acceso a ellos en cualquier orden.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Obtener datos grandes](../../oledb/ole-db-blobs/getting-large-data.md)  
  
-   [Definir datos grandes](../../oledb/ole-db-blobs/setting-large-data.md)  
  
-   [Compatibilidad con la transmisión por secuencias de parámetros de salida BLOB](../../oledb/ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>Consulte también  
 [Programación del controlador OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)        
 [Usar tipos de valor grande](../../oledb/features/using-large-value-types.md)  
  
  
