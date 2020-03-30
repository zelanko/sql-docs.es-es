---
title: Propiedades de orígenes de datos (OLE DB) | Microsoft Docs
description: Propiedades de orígenes de datos (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 13dd6afde96d42ac1fcc82b6fb24c721997b951d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015931"
---
# <a name="data-source-properties-ole-db"></a>Propiedades de orígenes de datos (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server implementa las propiedades del origen de datos del siguiente modo.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|L/E: Lectura y escritura. Valor predeterminado: Ninguno<br /><br /> Descripción: El valor de DBPROP_CURRENTCATALOG indica la base de datos actual para una sesión del controlador OLE DB para SQL Server. Establecer el valor de propiedad tiene el mismo efecto que establecer la base de datos actual mediante la instrucción USE [!INCLUDE[tsql](../../../includes/tsql-md.md)]database*de*.<br /><br /> A partir de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], si llama a [sp_defaultdb](../../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md) y especifica el nombre de la base de datos en letra minúscula, aunque la base de datos se hubiera creado inicialmente con un nombre en grafía mixta (mayúsculas y minúsculas), DBPROP_CURRENTCATALOG devolverá el nombre en letra minúscula. Con versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], DBPROP_CURRENTCATALOG devolverá el nombre en la grafía mixta (mayúsculas y minúsculas) esperada.|  
|DBPROP_MULTIPLECONNECTIONS|L/E: Lectura/escritura. Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: Si la conexión está ejecutando un comando que no genera un conjunto de filas o genera un conjunto de filas que no es un cursor de servidor y el usuario ejecuta otro comando, se creará una nueva conexión para ejecutar el nuevo comando si DBPROP_MULTIPLECONNECTIONS es VARIANT_TRUE.<br /><br /> El controlador OLE DB para SQL Server no creará otra conexión si DBPROP_MULTIPLECONNECTION es VARIANT_FALSE o si hay una transacción activa en la conexión. El controlador OLE DB para SQL Server devuelve DB_E_OBJECTOPEN si DBPROP_MULTIPLECONNECTIONS es VARIANT_FALSE y devuelve E_FAIL si hay una transacción activa. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] administra las transacciones y el bloqueo para cada conexión. Si se genera una segunda conexión, los comandos de cada una de las conexiones no comparten los bloqueos. Para asegurarse de que un comando no bloquea otro comando, mantenga los bloqueos en las filas solicitadas por el otro comando. Esto también es válido cuando se crean varias sesiones.<br /><br /> Cada sesión tiene una conexión independiente.|  
  
 En el conjunto de propiedades específicas del proveedor DBPROPSET_SQLSERVERDATASOURCE, el controlador OLE DB para SQL Server define las siguientes propiedades adicionales del origen de datos.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|L/E: Lectura/escritura. Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: Para habilitar la copia masiva de la memoria, la propiedad SSPROP_ENABLEFASTLOAD debe establecerse en VARIANT_TRUE. Con esta propiedad establecida en el origen de datos, la sesión recién creada permite el acceso del consumidor a la interfaz [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md).<br /><br /> Si la propiedad se establece en VARIANT_TRUE, la interfaz **IRowsetFastLoad** está disponible a través de **IOpenRowset::OpenRowset** al solicitar la interfaz **IID_IRowsetFastLoad** o establecer **SSPROP_IRowsetFastLoad** en VARIANT_TRUE.|  
|SSPROP_ENABLEBULKCOPY|L/E: Lectura/escritura. Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: Para habilitar la copia masiva desde archivos, la propiedad SSPROP_ENABLEBULKCOPY debe establecerse en VARIANT_TRUE. Con esta propiedad establecida en el origen de datos, el acceso del consumidor a la interfaz IBCPSession está disponible en el mismo nivel que Sessions.<br /><br /> SSPROP_IRowsetFastLoad también debe establecerse en VARIANT_TRUE.|  
  
## <a name="see-also"></a>Consulte también  
 [Objetos de origen de datos &#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
