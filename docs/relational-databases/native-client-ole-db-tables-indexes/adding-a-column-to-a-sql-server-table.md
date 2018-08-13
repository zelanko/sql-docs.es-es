---
title: Agregar una columna a una tabla de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- AddColumn function
- SQL Server Native Client OLE DB provider, columns
- adding columns
ms.assetid: 22bae18a-bc9d-4617-8660-ed8b17a468d4
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 1db5e1e6181c9c7ece64be68ff40f5c9f31113f5
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39565889"
---
# <a name="adding-a-column-to-a-sql-server-table"></a>Agregar una columna a una tabla de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone la **ITableDefinition:: AddColumn** función. Esto permite que los consumidores agreguen una columna a una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Cuando se agrega una columna a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor OLE DB de Native Client se restringe como sigue:  
  
-   Si DBPROP_COL_AUTOINCREMENT es VARIANT_TRUE, DBPROP_COL_NULLABLE debe ser VARIANT_FALSE.  
  
-   Si la columna se define mediante el tipo de datos **timestamp** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], DBPROP_COL_NULLABLE debe ser VARIANT_FALSE.  
  
-   Para cualquier otra definición de columna, DBPROP_COL_NULLABLE debe ser VARIANT_TRUE.  
  
 Los consumidores especifican el nombre de tabla como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en el parámetro *pTableID*. El miembro *eKind* de *pTableID* debe ser DBKIND_NAME.  
  
 El nuevo nombre de columna se especifica como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en el miembro *dbcid* del parámetro DBCOLUMNDESC *pColumnDesc*. El miembro *eKind* debe ser DBKIND_NAME.  
  
## <a name="see-also"></a>Vea también  
 [Tablas e índices](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
