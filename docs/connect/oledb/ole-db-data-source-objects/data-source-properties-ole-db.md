---
title: Propiedades (OLE DB) del origen de datos | Documentos de Microsoft
description: Propiedades de origen de datos (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 1b426d49bd6a37167c16889f1e17c27ee72531c0
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2018
ms.locfileid: "35665505"
---
# <a name="data-source-properties-ole-db"></a>Propiedades de orígenes de datos (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server implementa propiedades del origen de datos como se indica a continuación.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|L/E: Lectura y escritura. Valor predeterminado: Ninguno<br /><br /> Descripción: El valor de DBPROP_CURRENTCATALOG indica la base de datos actual para un controlador de OLE DB para la sesión de SQL Server. Establecer el valor de propiedad tiene el mismo efecto que establecer la base de datos actual mediante el uso de la [!INCLUDE[tsql](../../../includes/tsql-md.md)] USE *base de datos* instrucción.<br /><br /> A partir de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], si se llama a [sp_defaultdb](../../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md) y especifique el nombre de la base de datos en minúscula, incluso si la base de datos se creó originalmente con un nombre en grafía mixta, DBPROP_CURRENTCATALOG devolverá el nombre en minúsculas. Con versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], DBPROP_CURRENTCATALOG devolverá el nombre en la grafía mixta (mayúsculas y minúsculas) esperada.|  
|DBPROP_MULTIPLECONNECTIONS|L/E: Lectura/escritura. Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: Si la conexión está ejecutando un comando que no genera un conjunto de filas o genera un conjunto de filas que no es un cursor de servidor y el usuario ejecuta otro comando, se creará una nueva conexión para ejecutar el nuevo comando si DBPROP_MULTIPLECONNECTIONS es VARIANT_TRUE.<br /><br /> El controlador OLE DB para SQL Server no creará otra conexión si DBPROP_MULTIPLECONNECTION es VARIANT_FALSE o si una transacción está activa en la conexión. El controlador OLE DB para SQL Server devuelve DB_E_OBJECTOPEN si DBPROP_MULTIPLECONNECTIONS es VARIANT_FALSE y devuelve E_FAIL si hay una transacción activa. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] administra las transacciones y el bloqueo para cada conexión. Si se genera una segunda conexión, los comandos en las conexiones independientes no comparten los bloqueos. Para asegurarse de que un comando no bloquea otro comando, mantenga los bloqueos en las filas solicitadas por el otro comando. Esto también es válido cuando se crean varias sesiones.<br /><br /> Cada sesión tiene una conexión independiente.|  
  
 En el conjunto de propiedades específicas del proveedor DBPROPSET_SQLSERVERDATASOURCE, el controlador OLE DB para SQL Server define las siguientes propiedades de origen de datos adicionales.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|L/E: Lectura/escritura. Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: Para habilitar la copia masiva de la memoria, la propiedad SSPROP_ENABLEFASTLOAD debe establecerse en VARIANT_TRUE. Con esta propiedad establecida en el origen de datos, la sesión recién creada permite el acceso del consumidor a la [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md) interfaz.<br /><br /> Si la propiedad se establece en VARIANT_TRUE, **IRowsetFastLoad** interfaz está disponible a través de **IOpenRowset:: OpenRowset** solicitando la **IID_IRowsetFastLoad** interfaz o al establecer **SSPROP_IRowsetFastLoad** en VARIANT_TRUE.|  
|SSPROP_ENABLEBULKCOPY|L/E: Lectura/escritura. Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: Para habilitar la copia masiva desde archivos, la propiedad SSPROP_ENABLEBULKCOPY debe establecerse en VARIANT_TRUE. Con esta propiedad establecida en el origen de datos, el acceso del consumidor a la interfaz IBCPSession está disponible en el mismo nivel que Sessions.<br /><br /> SSPROP_IRowsetFastLoad también debe establecerse en VARIANT_TRUE.|  
  
## <a name="see-also"></a>Vea también  
 [Objetos de origen de datos &#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
