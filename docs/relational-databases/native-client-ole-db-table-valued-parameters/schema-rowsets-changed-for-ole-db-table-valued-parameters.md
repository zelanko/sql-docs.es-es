---
title: "Conjuntos de filas de esquema cambiado para los parámetros con valores de tabla OLE DB | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- table-valued parameters (OLE DB), schema rowsets changed for (OLE DB)
ms.assetid: 581e3ead-53db-44da-8718-f3fc4b5108f1
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c3ec3496be31125f86ff672845421391b3995fe5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="schema-rowsets-changed-for-ole-db-table-valued-parameters"></a>Conjuntos de filas de esquema cambiados para los parámetros con valores de tabla de OLE DB
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  A continuación figuran los conjuntos de filas de esquema que se han cambiado o agregado para admitir los parámetros con valores de tabla.  
  
|Conjunto de filas de esquema|Description|  
|-------------------|-----------------|  
|DBSCHEMA_PROCEDURE_PARAMETERS|Se han agregado dos nuevas columnas al final del conjunto de filas denominadas SS_TYPE_CATALOG_NAME y SS_TYPE_SCHEMANAME. Estas columnas se podrían volver a usar para tipos futuros. Las columnas TYPE_NAME y LOCAL_TYPE_NAME contendrán el nombre del parámetro con valores de tabla de tipo TABLE. La columna DATA_TYPE tendrá el valor DBTYPE_TABLE = 143 para los parámetros con valores de tabla.|  
|DBSCHEMA_TABLE_TYPES|Se ha agregado este conjunto de filas para admitir los parámetros con valores de tabla. Es idéntico a DBSCHEMA_TABLES, salvo que únicamente devuelve los metadatos para los tipos de tabla, en lugar de para las tablas, las vistas o los sinónimos. La columna TABLE_TYPE tendrá el valor 'TABLE TYPE'.|  
|DBSCHEMA_TABLE_TYPE_PRIMARY_KEYS|Se ha agregado este conjunto de filas para admitir los parámetros con valores de tabla. Es idéntico a DBSCHEMA_PRIMARY_KEYS, salvo que únicamente devuelve los metadatos de las claves principales para los tipos de tabla, en lugar de para las tablas.|  
|DBSCHEMA_TABLE_TYPE_COLUMNS|Se ha agregado este conjunto de filas para admitir los parámetros con valores de tabla. Es idéntico a DBSCHEMA_COLUMNS, salvo que únicamente devuelve los metadatos de columna para los tipos de tabla, en lugar de para las tablas, las vistas o los sinónimos.|  
  
## <a name="see-also"></a>Vea también  
 [Con valores de tabla parámetros &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar con valores de tabla parámetros &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
