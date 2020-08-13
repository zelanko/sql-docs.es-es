---
title: Adición de una columna a una tabla de SQL Server (controlador OLE DB) | Microsoft Docs
description: Adición de una columna a una tabla de SQL Server con OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- AddColumn function
- OLE DB Driver for SQL Server, columns
- adding columns
author: pmasl
ms.author: pelopes
ms.openlocfilehash: ce22cc49060451e7d47a1f9452f1c10a134ae610
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86943147"
---
# <a name="adding-a-column-to-a-sql-server-table"></a>Agregar una columna a una tabla de SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server expone la función **ITableDefinition::AddColumn**. Esto permite que los consumidores agreguen una columna a una tabla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Al agregar una columna a una tabla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el consumidor de OLE DB Driver for SQL Server está restringido de la siguiente manera:  
  
-   Si DBPROP_COL_AUTOINCREMENT es VARIANT_TRUE, DBPROP_COL_NULLABLE debe ser VARIANT_FALSE.  
  
-   Si la columna se define mediante el tipo de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]timestamp**de**, DBPROP_COL_NULLABLE debe ser VARIANT_FALSE.  
  
-   Para cualquier otra definición de columna, DBPROP_COL_NULLABLE debe ser VARIANT_TRUE.  
  
 Los consumidores especifican el nombre de tabla como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en el parámetro *pTableID*. El miembro *eKind* de *pTableID* debe ser DBKIND_NAME.  
  
 El nuevo nombre de columna se especifica como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en el miembro *dbcid* del parámetro DBCOLUMNDESC *pColumnDesc*. El miembro *eKind* debe ser DBKIND_NAME.  
  
## <a name="see-also"></a>Consulte también  
 [Tablas e índices](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)  
  
  
