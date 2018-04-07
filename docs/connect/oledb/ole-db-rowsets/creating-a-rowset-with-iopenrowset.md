---
title: Crear un conjunto de filas con IOpenRowset | Documentos de Microsoft
description: Crear un conjunto de filas con IOpenRowset, interfaz de controlador de OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, creating
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 95a564131d37f8486c0a5b923187354f9d3efa86
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="creating-a-rowset-with-iopenrowset"></a>Crear un conjunto de filas con IOpenRowset
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador OLE DB para SQL Server admite la **IOpenRowset:: OpenRowset** método con las restricciones siguientes:  
  
-   Una tabla base o vista debe especificarse en una base de datos (DBID) de Id. de la estructura que la *pTableID* parámetro señala.  
  
-   El DBID *eKind* miembro debe indicar DBKIND_NAME.  
  
-   El DBID *uName* miembro debe especificar el nombre de una tabla base existente o una vista como una cadena de caracteres Unicode.  
  
-   El *pIndexID* parámetro de **OpenRowset** debe ser NULL.  
  
 El conjunto de resultados de **IOpenRowset:: OpenRowset** contiene un único conjunto de filas. Conjuntos de resultados que contienen un único conjunto de filas pueden ser compatibles con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] los cursores. La compatibilidad de cursor permite que el programador utilice mecanismos de simultaneidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
