---
description: Quitar una columna de una tabla de SQL Server (proveedor de OLE DB de Native Client)
title: Quitar una columna de SQL Server tabla (proveedor de OLE DB de Native Client)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- removing columns
- DropColumn function
- SQL Server Native Client OLE DB provider, columns
ms.assetid: 210811b7-cbd6-421e-bc6e-df9482236768
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8957f58ddd0c3bc134f81f93391bb06d4c62a23f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499021"
---
# <a name="removing-a-column-from-a-sql-server-table-native-client-ole-db-provider"></a>Quitar una columna de una tabla de SQL Server (proveedor de OLE DB de Native Client)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client expone la función **ITableDefinition::D ropcolumn** . Esto permite que los consumidores puedan quitar una columna de una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Los consumidores especifican el nombre de la tabla como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en el parámetro *pTableID*. El miembro *eKind* de *pTableID* debe ser DBKIND_NAME.  
  
 El consumidor indica un nombre de columna en el miembro *pwszName* de la unión *uName* en el parámetro *pColumnID*. El nombre de la columna es una cadena de caracteres Unicode. El miembro *eKind* de *pColumnID* debe ser DBKIND_NAME.  
  
## <a name="example"></a>Ejemplo  
  
### <a name="code"></a>Código  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Tablas e índices](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
