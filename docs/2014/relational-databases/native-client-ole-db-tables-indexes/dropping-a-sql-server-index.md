---
title: Quitar un índice de SQL Server | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
ms.assetid: add3ba14-10b1-4723-b7c0-3e83689e9fdd
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 38e103cd19950846dd9c88d0b4bdc0d5d385ba1f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107643"
---
# <a name="dropping-a-sql-server-index"></a>Quitar un índice de SQL Server
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone la **IIndexDefinition:: DropIndex** función. Esto permite que los consumidores puedan quitar un índice de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone algunas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restricciones PRIMARY KEY y UNIQUE como índices. Pueden modificar el propietario de la tabla, el propietario de la base de datos y algunos miembros del rol administrativo un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla, quitar una restricción. De forma predeterminada, solo el propietario de la tabla puede quitar un índice existente. Por lo tanto, **DropIndex** finalizó correctamente o no depende no solo de derechos de acceso del usuario de la aplicación sino también en el tipo de índice indicado.  
  
 Los consumidores especifican el nombre de tabla como una cadena de caracteres Unicode en el *pwszName* miembro de la *uName* union en la *pTableID* parámetro. El *eKind* miembro de *pTableID* debe ser DBKIND_NAME.  
  
 Los consumidores especifican el nombre del índice como una cadena de caracteres Unicode en el *pwszName* miembro de la *uName* union en la *pIndexID* parámetro. El *eKind* miembro de *pIndexID* debe ser DBKIND_NAME. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no admite la característica de OLE DB de quitar todos los índices en una tabla cuando *pIndexID* es null. Si *pIndexID* es null, se devuelve E_INVALIDARG.  
  
## <a name="see-also"></a>Vea también  
 [Tablas e índices](tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
  
