---
title: "Propiedades de sesión: proveedor de SQL Server Native Client OLE DB | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-data-source-objects
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 2498fbad-b3db-4bea-8fc6-fef5317d3eba
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3d8e6261cc1b58cc209f29d1613e215c2e1adea9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="session-properties---sql-server-native-client-ole-db-provider"></a>Propiedades de sesión: proveedor de SQL Server Native Client OLE DB
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client interpreta las propiedades de la sesión de OLE DB como sigue.  
  
|Id. de propiedad|Description|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client admite todos los niveles de aislamiento de transacciones de confirmación automática con la excepción del nivel DBPROPVAL_TI_CHAOS.|  
  
 En la propiedad específica del proveedor establecida en DBPROPSET_SQLSERVERSESSION, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client define la siguiente propiedad de sesión adicional.  
  
|Id. de propiedad|Description|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|Tipo: VT_BOOL<br /><br /> L/E lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: identificadores entre comillas permitidos en restricción CATALOG.<br /><br /> VARIANT_TRUE: identificadores entre comillas reconocidos para una restricción CATALOG en conjuntos de filas de esquema que proporcionan compatibilidad con consultas distribuidas.<br /><br /> VARIANT_FALSE: identificadores entre comillas no reconocidos para una restricción CATALOG en conjuntos de filas de esquema que proporcionan compatibilidad con consultas distribuidas.<br /><br /> Para obtener más información acerca de conjuntos de filas de esquema que proporcionan compatibilidad con consultas distribuidas, consulte [permitir compatibilidad con consultas distribuidas en conjuntos de filas de esquema](../../relational-databases/native-client/ole-db/schema-rowsets-distributed-query-support.md).|  
|SSPROP_ALLOWNATIVEVARIANT|Tipo: VT_BOOL<br /><br /> L/E: de lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: determina si los datos se capturan como DBTYPE_VARIANT o DBTYPE_SQLVARIANT.<br /><br /> VARIANT_TRUE: el tipo de columna se devuelve como DBTYPE_SQLVARIANT, en cuyo caso el búfer contendrá la estructura SSVARIANT.<br /><br /> VARIANT_FALSE: el tipo de columna se devuelve como DBTYPE_VARIANT y el búfer contendrá la estructura VARIANT.|  
|SSPROP_ASYNCH_BULKCOPY|Para usar el modo asincrónico, establezca la propiedad de sesión SSPROP_ASYNCH_BULKCOPY específica del proveedor en VARIANT_TRUE antes de llamar al método BCPExec. Esta propiedad se encuentra disponible en el conjunto de propiedades DBPROPSET_SQLSERVERSESSION.|  
  
## <a name="see-also"></a>Vea también  
 [Objetos de origen de datos &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
