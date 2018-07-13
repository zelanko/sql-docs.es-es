---
title: Crear un conjunto de filas con IOpenRowset | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30ba5a4d1cbe326be567a3be18cd7a76371f7e49
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417944"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>Crear un conjunto de filas con IOpenRowset
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client admite el **IOpenRowset:: OpenRowset** método con las siguientes restricciones:  
  
-   Una tabla base o vista debe especificarse en una base de datos (DBID) Id. de estructura que el *pTableID* parámetro señala.  
  
-   El DBID *eKind* miembro debe indicar DBKIND_NAME.  
  
-   El DBID *uName* miembro debe especificar el nombre de una tabla base existente o una vista como una cadena de caracteres Unicode.  
  
-   El *pIndexID* parámetro de **OpenRowset** debe ser NULL.  
  
 El conjunto de resultados de **IOpenRowset:: OpenRowset** contiene un único conjunto de filas. Se admiten conjuntos de resultados que contienen un único conjunto de filas por [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores. La compatibilidad de cursor permite que el programador utilice mecanismos de simultaneidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas](rowsets.md)  
  
  
