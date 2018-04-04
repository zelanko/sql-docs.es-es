---
title: 'Propiedades de sesión: controlador OLE DB para SQL Server | Documentos de Microsoft'
description: Propiedades de las sesiones - controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- OLE DB Driver for SQL Server, sessions
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ffe6f6a0c2a8c7100bb458b2e939b7e50f3a888a
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="session-properties---ole-db-driver-for-sql-server"></a>Propiedades de sesión: controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador OLE DB para SQL Server interpreta las propiedades de la sesión de OLE DB como sigue.  
  
|Id. de propiedad|Description|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|El controlador OLE DB para SQL Server admite todos los niveles de aislamiento de transacciones de confirmación automática con la excepción del nivel DBPROPVAL_TI_CHAOS.|  
  
 En el conjunto de propiedades específicas del proveedor DBPROPSET_SQLSERVERSESSION, el controlador OLE DB para SQL Server define la siguiente propiedad de sesión adicional.  
  
|Id. de propiedad|Description|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|Tipo: VT_BOOL<br /><br /> L/E lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: identificadores entre comillas permitidos en restricción CATALOG.<br /><br /> VARIANT_TRUE: identificadores entre comillas reconocidos para una restricción CATALOG en conjuntos de filas de esquema que proporcionan compatibilidad con consultas distribuidas.<br /><br /> VARIANT_FALSE: identificadores entre comillas no reconocidos para una restricción CATALOG en conjuntos de filas de esquema que proporcionan compatibilidad con consultas distribuidas.<br /><br /> Para obtener más información acerca de conjuntos de filas de esquema que proporcionan compatibilidad con consultas distribuidas, consulte [permitir compatibilidad con consultas distribuidas en conjuntos de filas de esquema](../../oledb/ole-db/schema-rowsets-distributed-query-support.md).|  
|SSPROP_ALLOWNATIVEVARIANT|Tipo: VT_BOOL<br /><br /> L/E: de lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: determina si los datos se capturan como DBTYPE_VARIANT o DBTYPE_SQLVARIANT.<br /><br /> VARIANT_TRUE: el tipo de columna se devuelve como DBTYPE_SQLVARIANT, en cuyo caso el búfer contendrá la estructura SSVARIANT.<br /><br /> VARIANT_FALSE: el tipo de columna se devuelve como DBTYPE_VARIANT y el búfer contendrá la estructura VARIANT.|  
|SSPROP_ASYNCH_BULKCOPY|Para usar el modo asincrónico, establezca la propiedad de sesión SSPROP_ASYNCH_BULKCOPY específica del proveedor en VARIANT_TRUE antes de llamar al método BCPExec. Esta propiedad se encuentra disponible en el conjunto de propiedades DBPROPSET_SQLSERVERSESSION.|  
  
## <a name="see-also"></a>Vea también  
 [Objetos de origen de datos &#40; OLE DB &#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
