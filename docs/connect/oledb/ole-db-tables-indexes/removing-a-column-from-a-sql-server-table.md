---
title: Quitar una columna de una tabla de SQL Server | Documentos de Microsoft
description: Quitar una columna de una tabla de SQL Server mediante el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- removing columns
- DropColumn function
- OLE DB Driver for SQL Server, columns
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 962e36bf135c6f01594652f4549b7e0216cd063f
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689088"
---
# <a name="removing-a-column-from-a-sql-server-table"></a>Quitar una columna de una tabla de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server expone la **ITableDefinition:: Dropcolumn** función. Esto permite que los consumidores puedan quitar una columna de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabla.  
  
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
 [Tablas e índices](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
