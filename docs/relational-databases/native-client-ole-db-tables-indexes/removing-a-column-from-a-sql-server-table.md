---
title: Quitar una columna de una tabla de SQL Server | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- removing columns
- DropColumn function
- SQL Server Native Client OLE DB provider, columns
ms.assetid: 210811b7-cbd6-421e-bc6e-df9482236768
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 36a20b13542646612fc3c0200ca09a93821a910f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="removing-a-column-from-a-sql-server-table"></a>Quitar una columna de una tabla de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone la **ITableDefinition:: Dropcolumn** función. Esto permite que los consumidores puedan quitar una columna de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla.  
  
 Los consumidores especifican el nombre de tabla como una cadena de caracteres Unicode en el *pwszName*miembro de la *uName* union en la *pTableID* parámetro. El *eKind*miembro de *pTableID* debe ser DBKIND_NAME.  
  
 El consumidor indica un nombre de columna en la *pwszName*miembro de la *uName* union en la *pColumnID* parámetro. El nombre de la columna es una cadena de caracteres Unicode. El *eKind* miembro de *pColumnID* debe ser DBKIND_NAME.  
  
## <a name="example"></a>Ejemplo  
  
### <a name="code"></a>código  
  
```  
DBID TableID;  
DBID ColumnID;  
HRESULT hr;  
  
TableID.eKind = DBKIND_NAME;  
TableID.uName.pwszName = L"MyTableName";  
  
ColumnID.eKind = DBKIND_NAME;  
ColumnID.uName.pwszName = L"MyColumnName";  
  
hr = m_pITableDefinition->DropColumn(&TableID, &ColumnID);  
```  
  
## <a name="see-also"></a>Vea también  
 [Tablas e índices](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
