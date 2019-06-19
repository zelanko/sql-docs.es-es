---
title: Quitar un índice SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
ms.assetid: add3ba14-10b1-4723-b7c0-3e83689e9fdd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eadcd1de5bfc3eea254bb134b963c2b4be094eaa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63283774"
---
# <a name="dropping-a-sql-server-index"></a>Quitar un índice de SQL Server
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone la **IIndexDefinition:: DropIndex** función. Esto permite que los consumidores quiten índices de las tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone algunas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restricciones PRIMARY KEY y UNIQUE como índices. El propietario de la tabla, el propietario de la base de datos y algunos miembros con roles administrativos pueden modificar las tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], quitando una restricción. De forma predeterminada, solo el propietario de la tabla puede quitar un índice existente. Por tanto, que **DropIndex** se realice correctamente o no depende no solo de los derechos de acceso del usuario de la aplicación sino también del tipo de índice indicado.  
  
 Los consumidores especifican el nombre de tabla como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en el parámetro *pTableID*. El miembro *eKind* de *pTableID* debe ser DBKIND_NAME.  
  
 Los consumidores especifican el nombre de índice como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en el parámetro *pIndexID*. El miembro *eKind* de *pIndexID* debe ser DBKIND_NAME. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no admite la característica de OLE DB de quitar todos los índices en una tabla cuando *pIndexID* es null. Si *pIndexID* es NULL, se devuelve E_INVALIDARG.  
  
## <a name="see-also"></a>Vea también  
 [Tablas e índices](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
  
