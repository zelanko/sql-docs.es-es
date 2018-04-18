---
title: Propiedades (OLE DB) del origen de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 6e14fefc-4e0b-4847-a833-4cf0abe65d50
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5de3fb544bf12333ad58702c8191edb86c90d35c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="data-source-properties-ole-db"></a>Propiedades de orígenes de datos (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client implementa las propiedades del origen de datos como se indica a continuación.  
  
|Id. de propiedad|Description|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|L/E: Lectura y escritura. Valor predeterminado: Ninguno<br /><br /> Descripción: El valor de DBPROP_CURRENTCATALOG indica la base de datos actual para un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sesión del proveedor OLE DB de Native Client. Establecer el valor de propiedad tiene el mismo efecto que establecer la base de datos actual mediante el uso de la [!INCLUDE[tsql](../../includes/tsql-md.md)] USE *base de datos* instrucción.<br /><br /> A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], si se llama a [sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md) y especifique el nombre de la base de datos en minúscula, incluso si la base de datos se creó originalmente con un nombre en grafía mixta, DBPROP_CURRENTCATALOG devolverá el nombre en minúsculas. Con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], DBPROP_CURRENTCATALOG devolverá el nombre en la grafía mixta (mayúsculas y minúsculas) esperada.|  
|DBPROP_MULTIPLECONNECTIONS|L/E: Lectura/escritura. Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: Si la conexión está ejecutando un comando que no genera un conjunto de filas o genera un conjunto de filas que no es un cursor de servidor y el usuario ejecuta otro comando, se creará una nueva conexión para ejecutar el nuevo comando si DBPROP_MULTIPLECONNECTIONS es VARIANT_TRUE.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no creará otra conexión si DBPROP_MULTIPLECONNECTION es VARIANT_FALSE o si una transacción está activa en la conexión. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve DB_E_OBJECTOPEN si DBPROP_MULTIPLECONNECTIONS es VARIANT_FALSE y devuelve E_FAIL si hay una transacción activa. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administra las transacciones y el bloqueo para cada conexión. Si se genera una segunda conexión, los comandos en las conexiones independientes no comparten los bloqueos. Para asegurarse de que un comando no bloquea otro comando, mantenga los bloqueos en las filas solicitadas por el otro comando. Esto también es válido cuando se crean varias sesiones.<br /><br /> Cada sesión tiene una conexión independiente.|  
  
 En la propiedad específica del proveedor establezca DBPROPSET_SQLSERVERDATASOURCE, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client define las siguientes propiedades de origen de datos adicionales.  
  
|Id. de propiedad|Description|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|L/E: Lectura/escritura. Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: Para habilitar la copia masiva de la memoria, la propiedad SSPROP_ENABLEFASTLOAD debe establecerse en VARIANT_TRUE. Con esta propiedad establecida en el origen de datos, la sesión recién creada permite el acceso del consumidor a la [IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) interfaz.<br /><br /> Si la propiedad se establece en VARIANT_TRUE, **IRowsetFastLoad** interfaz está disponible a través de **IOpenRowset:: OpenRowset** solicitando la **IID_IRowsetFastLoad** interfaz o al establecer **SSPROP_IRowsetFastLoad** en VARIANT_TRUE.|  
|SSPROP_ENABLEBULKCOPY|L/E: Lectura/escritura. Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: Para habilitar la copia masiva desde archivos, la propiedad SSPROP_ENABLEBULKCOPY debe establecerse en VARIANT_TRUE. Con esta propiedad establecida en el origen de datos, el acceso del consumidor a la interfaz IBCPSession está disponible en el mismo nivel que Sessions.<br /><br /> SSPROP_IRowsetFastLoad también debe establecerse en VARIANT_TRUE.|  
  
## <a name="see-also"></a>Vea también  
 [Objetos de origen de datos & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
