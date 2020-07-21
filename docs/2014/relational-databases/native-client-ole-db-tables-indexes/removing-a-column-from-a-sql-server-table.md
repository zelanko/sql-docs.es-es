---
title: Eliminación de una columna de una tabla de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- removing columns
- DropColumn function
- SQL Server Native Client OLE DB provider, columns
ms.assetid: 210811b7-cbd6-421e-bc6e-df9482236768
author: rothja
ms.author: jroth
ms.openlocfilehash: d416514ed627556b1716fba2ee4be8861fdabad2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85017853"
---
# <a name="removing-a-column-from-a-sql-server-table"></a>Quitar una columna de una tabla de SQL Server
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
 [Tablas e índices](tables-and-indexes.md)  
  
  
