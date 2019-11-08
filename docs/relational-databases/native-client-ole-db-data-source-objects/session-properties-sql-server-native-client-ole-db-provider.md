---
title: Propiedades de sesión-proveedor de OLE DB de SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 2498fbad-b3db-4bea-8fc6-fef5317d3eba
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0b7ad59b25060ca58224400135acafb50b0b79d3
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73774318"
---
# <a name="session-properties---sql-server-native-client-ole-db-provider"></a>Propiedades de la sesión: proveedor de SQL Server Native Client OLE DB
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client interpreta OLE DB propiedades de sesión como se indica a continuación.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|El proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite todos los niveles de aislamiento de transacción de confirmación automática con la excepción del nivel de caos DBPROPVAL_TI_CHAOS.|  
  
 En el conjunto de propiedades específico del proveedor DBPROPSET_SQLSERVERSESSION, el proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define la siguiente propiedad de sesión adicional.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|Tipo: VT_BOOL<br /><br /> L/E: lectura y escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: identificadores entre comillas permitidos en restricción CATALOG.<br /><br /> VARIANT_TRUE: identificadores entre comillas reconocidos para una restricción CATALOG en conjuntos de filas de esquema que proporcionan compatibilidad con consultas distribuidas.<br /><br /> VARIANT_FALSE: identificadores entre comillas no reconocidos para una restricción CATALOG en conjuntos de filas de esquema que proporcionan compatibilidad con consultas distribuidas.<br /><br /> Para obtener más información sobre los conjuntos de filas de esquema que proporcionan compatibilidad con consultas distribuidas, vea [Compatibilidad con consultas distribuidas en conjuntos de filas de esquema](../../relational-databases/native-client/ole-db/schema-rowsets-distributed-query-support.md).|  
|SSPROP_ALLOWNATIVEVARIANT|Tipo: VT_BOOL<br /><br /> L/E: de lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: determina si los datos se capturan como DBTYPE_VARIANT o DBTYPE_SQLVARIANT.<br /><br /> VARIANT_TRUE: el tipo de columna se devuelve como DBTYPE_SQLVARIANT, en cuyo caso el búfer contendrá la estructura SSVARIANT.<br /><br /> VARIANT_FALSE: el tipo de columna se devuelve como DBTYPE_VARIANT y el búfer contendrá la estructura VARIANT.|  
|SSPROP_ASYNCH_BULKCOPY|Para usar el modo asincrónico, establezca la propiedad de sesión SSPROP_ASYNCH_BULKCOPY específica del proveedor en VARIANT_TRUE antes de llamar al método BCPExec. Esta propiedad se encuentra disponible en el conjunto de propiedades DBPROPSET_SQLSERVERSESSION.|  
  
## <a name="see-also"></a>Vea también  
 [Objetos &#40;de origen de datos OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
