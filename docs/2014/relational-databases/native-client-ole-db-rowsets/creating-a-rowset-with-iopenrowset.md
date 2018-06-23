---
title: Crear un conjunto de filas con IOpenRowset | Documentos de Microsoft
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
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7cdce7632aa726d2992a0383d19691569ed57c0a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203936"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>Crear un conjunto de filas con IOpenRowset
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el proveedor OLE DB de Native Client la **IOpenRowset:: OpenRowset** método con las restricciones siguientes:  
  
-   Una tabla base o vista debe especificarse en una base de datos (DBID) de Id. de la estructura que la *pTableID* parámetro señala.  
  
-   El DBID *eKind* miembro debe indicar DBKIND_NAME.  
  
-   El DBID *uName* miembro debe especificar el nombre de una tabla base existente o una vista como una cadena de caracteres Unicode.  
  
-   El *pIndexID* parámetro de **OpenRowset** debe ser NULL.  
  
 El conjunto de resultados de **IOpenRowset:: OpenRowset** contiene un único conjunto de filas. Conjuntos de resultados que contienen un único conjunto de filas pueden ser compatibles con [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los cursores. La compatibilidad de cursor permite que el programador utilice mecanismos de simultaneidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas](rowsets.md)  
  
  