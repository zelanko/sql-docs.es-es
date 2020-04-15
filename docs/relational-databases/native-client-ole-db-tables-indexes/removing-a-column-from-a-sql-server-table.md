---
title: Eliminación de una columna de una tabla de SQL Server | Microsoft Docs
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
ms.openlocfilehash: 97b20e285749c7a3dba2ecf36ccb6556d93b5903
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280057"
---
# <a name="removing-a-column-from-a-sql-server-table"></a>Quitar una columna de una tabla de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone la función **ITableDefinition::DropColumn.** Esto permite que los consumidores puedan quitar una columna de una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
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
  
  
