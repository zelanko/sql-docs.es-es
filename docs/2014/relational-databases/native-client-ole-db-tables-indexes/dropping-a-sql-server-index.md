---
title: Eliminación de un índice de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9be4e3607097c476f083c32eed9f13fecc0d3842
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704522"
---
# <a name="dropping-a-sql-server-index"></a>Quitar un índice de SQL Server
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client expone la función **IIndexDefinition::D ropindex** . Esto permite que los consumidores quiten índices de las tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client expone algunas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restricciones PRIMARY KEY y Unique como índices. El propietario de la tabla, el propietario de la base de datos y algunos miembros con roles administrativos pueden modificar las tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], quitando una restricción. De forma predeterminada, solo el propietario de la tabla puede quitar un índice existente. Por tanto, que **DropIndex** se realice correctamente o no depende no solo de los derechos de acceso del usuario de la aplicación sino también del tipo de índice indicado.  
  
 Los consumidores especifican el nombre de tabla como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en el parámetro *pTableID*. El miembro *eKind* de *pTableID* debe ser DBKIND_NAME.  
  
 Los consumidores especifican el nombre de índice como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en el parámetro *pIndexID*. El miembro *eKind* de *pIndexID* debe ser DBKIND_NAME. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client no admite la característica OLE DB de quitar todos los índices de una tabla cuando *pIndexID* es NULL. Si *pIndexID* es NULL, se devuelve E_INVALIDARG.  
  
## <a name="see-also"></a>Consulte también  
 [Tablas e índices](tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
  
