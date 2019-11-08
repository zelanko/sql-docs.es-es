---
title: Agregar una columna a una tabla SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 45048935e9d636a95af1c77eb8f7a88153d22106
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73788510"
---
# <a name="adding-a-column-to-a-sql-server-table"></a>Agregar una columna a una tabla de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client expone la función **ITableDefinition:: addColumn** . Esto permite que los consumidores agreguen una columna a una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Al agregar una columna a una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el consumidor del proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client está restringido de la siguiente manera:  
  
-   Si DBPROP_COL_AUTOINCREMENT es VARIANT_TRUE, DBPROP_COL_NULLABLE debe ser VARIANT_FALSE.  
  
-   Si la columna se define mediante el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]timestamp**de**, DBPROP_COL_NULLABLE debe ser VARIANT_FALSE.  
  
-   Para cualquier otra definición de columna, DBPROP_COL_NULLABLE debe ser VARIANT_TRUE.  
  
 Los consumidores especifican el nombre de tabla como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en el parámetro *pTableID*. El miembro *eKind* de *pTableID* debe ser DBKIND_NAME.  
  
 El nuevo nombre de columna se especifica como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en el miembro *dbcid* del parámetro DBCOLUMNDESC *pColumnDesc*. El miembro *eKind* debe ser DBKIND_NAME.  
  
## <a name="see-also"></a>Vea también  
 [Tablas e índices](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
