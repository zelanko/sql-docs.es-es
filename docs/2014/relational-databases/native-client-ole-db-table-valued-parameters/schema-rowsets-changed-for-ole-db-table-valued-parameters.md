---
title: Conjuntos de filas de esquema cambiado para los parámetros con valores de tabla OLE DB | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- table-valued parameters (OLE DB), schema rowsets changed for (OLE DB)
ms.assetid: 581e3ead-53db-44da-8718-f3fc4b5108f1
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b3769c8279cb439e1fa232b8973e29f117a88e8f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111549"
---
# <a name="schema-rowsets-changed-for-ole-db-table-valued-parameters"></a>Conjuntos de filas de esquema cambiados para los parámetros con valores de tabla de OLE DB
  A continuación figuran los conjuntos de filas de esquema que se han cambiado o agregado para admitir los parámetros con valores de tabla.  
  
|Conjunto de filas de esquema|Descripción|  
|-------------------|-----------------|  
|DBSCHEMA_PROCEDURE_PARAMETERS|Se han agregado dos nuevas columnas al final del conjunto de filas denominadas SS_TYPE_CATALOG_NAME y SS_TYPE_SCHEMANAME. Estas columnas se podrían volver a usar para tipos futuros. Las columnas TYPE_NAME y LOCAL_TYPE_NAME contendrán el nombre del parámetro con valores de tabla de tipo TABLE. La columna DATA_TYPE tendrá el valor DBTYPE_TABLE = 143 para los parámetros con valores de tabla.|  
|DBSCHEMA_TABLE_TYPES|Se ha agregado este conjunto de filas para admitir los parámetros con valores de tabla. Es idéntico a DBSCHEMA_TABLES, salvo que únicamente devuelve los metadatos para los tipos de tabla, en lugar de para las tablas, las vistas o los sinónimos. La columna TABLE_TYPE tendrá el valor 'TABLE TYPE'.|  
|DBSCHEMA_TABLE_TYPE_PRIMARY_KEYS|Se ha agregado este conjunto de filas para admitir los parámetros con valores de tabla. Es idéntico a DBSCHEMA_PRIMARY_KEYS, salvo que únicamente devuelve los metadatos de las claves principales para los tipos de tabla, en lugar de para las tablas.|  
|DBSCHEMA_TABLE_TYPE_COLUMNS|Se ha agregado este conjunto de filas para admitir los parámetros con valores de tabla. Es idéntico a DBSCHEMA_COLUMNS, salvo que únicamente devuelve los metadatos de columna para los tipos de tabla, en lugar de para las tablas, las vistas o los sinónimos.|  
  
## <a name="see-also"></a>Vea también  
 [Parámetros con valores de tabla &#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [Usar parámetros con valores de tabla &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  