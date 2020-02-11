---
title: Crear un conjunto de filas con IOpenRowset | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4aa7b91b10c2ce266ad648bce0ba1c19946098c8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63183709"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>Crear un conjunto de filas con IOpenRowset
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client admite el método **IOpenRowset:: OPENROWSET** con las siguientes restricciones:  
  
-   Debe especificarse una tabla base o una vista en una estructura de identificador de base de datos (DBID) a la que apunte el parámetro *pTableID*.  
  
-   El miembro *eKind* de DBID debe indicar DBKIND_NAME.  
  
-   El miembro *uName* de DBID debe especificar el nombre de una tabla base existente o una vista como una cadena de caracteres Unicode.  
  
-   El parámetro *pIndexID* de **OpenRowset** debe ser NULL.  
  
 El conjunto de resultados de **IOpenRowset::OpenRowset** contiene un único conjunto de filas. Los conjuntos de resultados que contienen un único conjunto de filas [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden ser compatibles con los cursores. La compatibilidad de cursor permite que el programador utilice mecanismos de simultaneidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Conjuntos de filas](rowsets.md)  
  
  
