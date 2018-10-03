---
title: Agregar una columna a una tabla de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
ms.openlocfilehash: 32e78feae791788e0aad87079546ea8c7d49e734
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48214245"
---
# <a name="adding-a-column-to-a-sql-server-table"></a>Agregar una columna a una tabla de SQL Server
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone la **ITableDefinition:: AddColumn** función. Esto permite que los consumidores agreguen una columna a una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Cuando se agrega una columna a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor OLE DB de Native Client se restringe como sigue:  
  
-   Si DBPROP_COL_AUTOINCREMENT es VARIANT_TRUE, DBPROP_COL_NULLABLE debe ser VARIANT_FALSE.  
  
-   Si la columna se define mediante el tipo de datos **timestamp** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], DBPROP_COL_NULLABLE debe ser VARIANT_FALSE.  
  
-   Para cualquier otra definición de columna, DBPROP_COL_NULLABLE debe ser VARIANT_TRUE.  
  
 Los consumidores especifican el nombre de tabla como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en el parámetro *pTableID*. El miembro *eKind* de *pTableID* debe ser DBKIND_NAME.  
  
 El nuevo nombre de columna se especifica como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en el miembro *dbcid* del parámetro DBCOLUMNDESC *pColumnDesc*. El miembro *eKind* debe ser DBKIND_NAME.  
  
## <a name="see-also"></a>Vea también  
 [Tablas e índices](tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)  
  
  
