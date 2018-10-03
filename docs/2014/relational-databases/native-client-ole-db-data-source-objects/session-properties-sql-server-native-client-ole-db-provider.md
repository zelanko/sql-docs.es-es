---
title: Propiedades de la sesión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 2498fbad-b3db-4bea-8fc6-fef5317d3eba
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 19ce2c6ca7b36a5d2147e7efda657fb2433aef25
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48158705"
---
# <a name="session-properties"></a>Propiedades de sesión
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client interpreta las propiedades de sesión de OLE DB como se indica a continuación.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client admite todos los niveles de aislamiento de transacciones de confirmación automática con la excepción del nivel DBPROPVAL_TI_CHAOS.|  
  
 En la propiedad específica del proveedor establecida en DBPROPSET_SQLSERVERSESSION, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client define las siguientes propiedades de sesión adicional.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|Tipo: VT_BOOL<br /><br /> L/E: lectura y escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: identificadores entre comillas permitidos en restricción CATALOG.<br /><br /> VARIANT_TRUE: identificadores entre comillas reconocidos para una restricción CATALOG en conjuntos de filas de esquema que proporcionan compatibilidad con consultas distribuidas.<br /><br /> VARIANT_FALSE: identificadores entre comillas no reconocidos para una restricción CATALOG en conjuntos de filas de esquema que proporcionan compatibilidad con consultas distribuidas.<br /><br /> Para obtener más información sobre los conjuntos de filas de esquema que proporcionan compatibilidad con consultas distribuidas, vea [Compatibilidad con consultas distribuidas en conjuntos de filas de esquema](../native-client/ole-db/schema-rowsets-distributed-query-support.md).|  
|SSPROP_ALLOWNATIVEVARIANT|Tipo: VT_BOOL<br /><br /> L/E: de lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: determina si los datos se capturan como DBTYPE_VARIANT o DBTYPE_SQLVARIANT.<br /><br /> VARIANT_TRUE: el tipo de columna se devuelve como DBTYPE_SQLVARIANT, en cuyo caso el búfer contendrá la estructura SSVARIANT.<br /><br /> VARIANT_FALSE: el tipo de columna se devuelve como DBTYPE_VARIANT y el búfer contendrá la estructura VARIANT.|  
|SSPROP_ASYNCH_BULKCOPY|Para usar el modo asincrónico, establezca la propiedad de sesión SSPROP_ASYNCH_BULKCOPY específica del proveedor en VARIANT_TRUE antes de llamar al método BCPExec. Esta propiedad se encuentra disponible en el conjunto de propiedades DBPROPSET_SQLSERVERSESSION.|  
  
## <a name="see-also"></a>Vea también  
 [Objetos de origen de datos &#40;OLE DB&#41;](data-source-objects-ole-db.md)  
  
  
