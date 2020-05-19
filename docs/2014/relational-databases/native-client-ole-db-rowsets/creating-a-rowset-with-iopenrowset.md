---
title: Creación de un conjunto de filas con IOpenRowset | Microsoft Docs
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3d8865f6a6e38e9764b7aa2c67d069eeb6a4ec84
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704681"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>Crear un conjunto de filas con IOpenRowset
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client admite el método **IOpenRowset:: OPENROWSET** con las siguientes restricciones:  
  
-   Debe especificarse una tabla base o una vista en una estructura de identificador de base de datos (DBID) a la que apunte el parámetro *pTableID*.  
  
-   El miembro *eKind* de DBID debe indicar DBKIND_NAME.  
  
-   El miembro *uName* de DBID debe especificar el nombre de una tabla base existente o una vista como una cadena de caracteres Unicode.  
  
-   El parámetro *pIndexID* de **OpenRowset** debe ser NULL.  
  
 El conjunto de resultados de **IOpenRowset::OpenRowset** contiene un único conjunto de filas. Los conjuntos de resultados que contienen un único conjunto de filas pueden ser compatibles con los [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores. La compatibilidad de cursor permite que el programador utilice mecanismos de simultaneidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Conjuntos de filas](rowsets.md)  
  
  
