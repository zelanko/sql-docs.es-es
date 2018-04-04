---
title: Quitar un índice de SQL Server | Documentos de Microsoft
description: Quitar un índice de sql server mediante el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 60e7198d6c6ab18f84640cd0531cd9d0bac63a90
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="dropping-a-sql-server-index"></a>Quitar un índice de SQL Server

  El controlador OLE DB para SQL Server expone la **IIndexDefinition:: DropIndex** función. Esto permite que los consumidores puedan quitar un índice de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabla.  
  
 El controlador OLE DB para SQL Server expone algunas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] restricciones PRIMARY KEY y UNIQUE como índices. Pueden modificar el propietario de la tabla, el propietario de la base de datos y algunos miembros del rol administrativo un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabla, quitar una restricción. De forma predeterminada, solo el propietario de la tabla puede quitar un índice existente. Por lo tanto, **DropIndex** finalizó correctamente o no depende no solo de derechos de acceso del usuario de la aplicación sino también en el tipo de índice indicado.  
  
 Los consumidores especifican el nombre de tabla como una cadena de caracteres Unicode en el *pwszName* miembro de la *uName* union en la *pTableID* parámetro. El *eKind* miembro de *pTableID* debe ser DBKIND_NAME.  
  
 Los consumidores especifican el nombre del índice como una cadena de caracteres Unicode en el *pwszName* miembro de la *uName* union en la *pIndexID* parámetro. El *eKind* miembro de *pIndexID* debe ser DBKIND_NAME. El controlador OLE DB para SQL Server no admite la característica de OLE DB de quitar todos los índices en una tabla cuando *pIndexID* es null. Si *pIndexID* es null, se devuelve E_INVALIDARG.  
  
## <a name="see-also"></a>Vea también  
 [Tablas e índices](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-index-transact-sql.md)  
  
  
